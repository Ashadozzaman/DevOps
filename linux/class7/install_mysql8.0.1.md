# How To Install MySQL on Ubuntu 22.04

### Intrduction
MySQL is an open-source database management system, commonly installed as part of the popular LAMP (Linux, Apache, MySQL, PHP/Python/Perl) stack. It implements the relational model and uses Structured Query Language (better known as SQL) to manage its data.

This tutorial will go over how to install MySQL version 8.0 on an Ubuntu 22.04 server. By completing it, you will have a working relational database that you can use to build your next website or application.

### Step 1 — Installing MySQL
On Ubuntu 22.04, you can install MySQL using the APT package repository. At the time of this writing, the version of MySQL available in the default Ubuntu repository is version 8.0.28.
To install it, update the package index on your server if you’ve not done so recently:
```
sudo apt update
```
Then install the mysql-server package:
```
sudo apt install mysql-server
```
Ensure that the server is running using the `systemctl start `command:
```
sudo systemctl start mysql.service
```
These commands will install and start MySQL, but will not prompt you to set a password or make any other configuration changes. Because this leaves your installation of MySQL insecure, we will address this next.

### Step 2 — Configuring MySQL

For fresh installations of MySQL, you’ll want to run the database management system’s included security script. This script changes some of the less secure default options for things like disallowing remote root logins and removing sample users.

Warning: As of July 2022, an error will occur when you run the `mysql_secure_installation` script without some further configuration. The reason is that this script will attempt to set a password for the installation’s root MySQL account but, by default on Ubuntu installations, this account is not configured to connect using a password.

Prior to July 2022, this script would silently fail after attempting to set the root account password and continue on with the rest of the prompts. However, as of this writing the script will return the following error after you enter and confirm a password:

```
Output
 ... Failed! Error: SET PASSWORD has no significance for user 'root'@'localhost' as the authentication method used doesn't store authentication data in the MySQL server. Please consider using ALTER USER instead if you want to change authentication parameters.

New password:
```
This will lead the script into a recursive loop which you can only get out of by closing your terminal window.

Because the `mysql_secure_installation` script performs a number of other actions that are useful for keeping your MySQL installation secure, it’s still recommended that you run it before you begin using MySQL to manage your data. To avoid entering this recursive loop, though, you’ll need to first adjust how your root MySQL user authenticates.

First, open up the MySQL prompt:
```
sudo mysql
```
- Access to Mysql

Then run the following `ALTER USER` command to change the `root` user’s authentication method to one that uses a `password`. The following example changes the authentication method to `mysql_native_password`:

```
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
```
- Successflly set password

After making this change, exit the MySQL prompt:
```
exit
```
Following that, you can run the `mysql_secure_installation` script without issue.Run the security script with `sudo`.
```
sudo mysql_secure_installation
```

This will take you through a series of prompts where you can make some changes to your MySQL installation’s security options. The first prompt will ask whether you’d like to set up the Validate Password Plugin, which can be used to test the password strength of new MySQL users before deeming them valid.

If you elect to set up the Validate Password Plugin, any MySQL user you create that authenticates with a password will be required to have a password that satisfies the policy you select:

```
Output
Securing the MySQL server deployment.

Connecting to MySQL using a blank password.

VALIDATE PASSWORD COMPONENT can be used to test passwords
and improve security. It checks the strength of password
and allows the users to set only those passwords which are
secure enough. Would you like to setup VALIDATE PASSWORD component?

Press y|Y for Yes, any other key for No: Y

There are three levels of password validation policy:

LOW    Length >= 8
MEDIUM Length >= 8, numeric, mixed case, and special characters
STRONG Length >= 8, numeric, mixed case, special characters and dictionary                  file

Please enter 0 = LOW, 1 = MEDIUM and 2 = STRONG:
 2

Note: If you use 2,3 need strong password.
```
Regardless of whether you choose to set up the Validate Password Plugin, the next prompt will be to set a password for the MySQL root user. Enter and then confirm a secure password of your choice:
```
Output
Please set the password for root here.


New password:

Re-enter new password:
```
Note that even though you’ve set a password for the root MySQL user, this user is not currently configured to authenticate with a password when connecting to the MySQL shell.

If you used the Validate Password Plugin, you’ll receive feedback on the strength of your new password. Then the script will ask if you want to continue with the password you just entered or if you want to enter a new one. Assuming you’re satisfied with the strength of the password you just entered, enter Y to continue the script:

```
Output
Estimated strength of the password: 100
Do you wish to continue with the password provided?(Press y|Y for Yes, any other key for No) : Y
```

From there, you can press `Y` and then `ENTER` to accept the defaults for all the subsequent questions. This will remove some anonymous users and the test database, disable remote root logins, and load these new rules so that MySQL immediately respects the changes you have made.

### Note: Once the security script completes, you can then reopen MySQL and change the root user’s authentication method back to the default, auth_socket. To authenticate as the root MySQL user using a password, run this command:

```
mysql -u root -p
```
Then go back to using the default authentication method using this command:
```
ALTER USER 'root'@'localhost' IDENTIFIED WITH auth_socket;
```
This will mean that you can once again connect to MySQL as your root user using the sudo mysql command.

Once the script completes, your MySQL installation will be secured. You can now move on to creating a dedicated database user with the MySQL client.

## Step 3 — Creating a Dedicated MySQL User and Granting Privileges

Upon installation, MySQL creates a root user account which you can use to manage your database. This user has full privileges over the MySQL server, meaning it has complete control over every database, table, user, and so on. Because of this, it’s best to avoid using this account outside of administrative functions. This step outlines how to use the root MySQL user to create a new user account and grant it privileges.

In Ubuntu systems running MySQL 5.7 (and later versions), the root MySQL user is set to authenticate using the auth_socket plugin by default rather than with a password. This plugin requires that the name of the operating system user that invokes the MySQL client matches the name of the MySQL user specified in the command, so you must invoke mysql with sudo privileges to gain access to the root MySQL user:

```
sudo mysql
```
Note: If you installed MySQL with another tutorial and enabled password authentication for root, you will need to use a different command to access the MySQL shell. The following will run your MySQL client with regular user privileges, and you will only gain administrator privileges within the database by authenticating:

```
mysql -u root -p
```

Once you have access to the MySQL prompt, you can create a new user with a CREATE USER statement. These follow this general syntax:

```
CREATE USER 'ashadozzaman'@'localhost' IDENTIFIED WITH authentication_plugin BY 'password';
```

Note: If you face error like:-
```
ERROR 1524 (HY000): Plugin 'authentication_plugin' is not loaded
```

### Check Available Plugins
```
SHOW PLUGINS;
```

After `CREATE USER`, you specify a username. This is immediately followed by an `@` sign and then the hostname from which this user will connect. If you only plan to access this user locally from your Ubuntu server, you can specify `localhost`. Wrapping both the username and host in single quotes isn’t always necessary, but doing so can help to prevent errors.

You have several options when it comes to choosing your user’s authentication plugin. The `auth_socket` plugin mentioned previously can be convenient, as it provides strong security without requiring valid users to enter a password to access the database. But it also prevents remote connections, which can complicate things when external programs need to interact with MySQL.

As an alternative, you can leave out the WITH `authentication_plugin` portion of the syntax entirely to have the user authenticate with MySQL’s default plugin, `caching_sha2_password`. The MySQL documentation recommends this plugin for users who want to log in with a password due to its strong security features.

Run the following command to create a user that authenticates with `caching_sha2_password`. Be sure to change `ashadozzaman` to your preferred username and `password` to a strong password of your choosing.

```
CREATE USER 'ashadozzaman'@'localhost' IDENTIFIED BY 'password';
```
`Note`: There is a known issue with some versions of PHP that causes problems with `caching_sha2_password`. If you plan to use this database with a PHP application — phpMyAdmin, for example — you may want to create a user that will authenticate with the older, though still secure, `mysql_native_password` plugin instead.
```
CREATE USER 'ashadozzaman'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
```
If you aren’t sure, you can always create a user that authenticates with `caching_sha2_plugin` and then `ALTER` it later on with this command.
```
ALTER USER 'ashadozzaman'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
```

***After creating your new user, you can grant them the appropriate privileges. The general syntax for granting user privileges is as follows:***

```
GRANT PRIVILEGE ON database.table TO 'username'@'host';
```
The `PRIVILEGE` value in this example syntax defines what actions the user is allowed to perform on the specified `database` and `table`. You can grant multiple privileges to the same user in one command by separating each with a comma. You can also grant a user privileges globally by entering asterisks (*) in place of the database and table names. In SQL, asterisks are special characters used to represent “all” databases or tables.

To illustrate, the following command grants a user global privileges to `CREATE`, `ALTER`, and `DROP` databases, tables, and users, as well as the power to INSERT, UPDATE, and DELETE data from any table on the server. It also grants the user the ability to query data with `SELECT`, `create` foreign keys with the `REFERENCES` keyword, and perform FLUSH operations with the RELOAD privilege. However, you should only grant users the permissions they need, so feel free to adjust your own user’s privileges as necessary.

You can find the full list of available privileges in the official MySQL documentation.

Run this `GRANT` statement, replacing `ashadozzaman` with your own MySQL user’s name, to `grant` these privileges to your user:

```
GRANT CREATE, ALTER, DROP, INSERT, UPDATE, INDEX, DELETE, SELECT, REFERENCES, RELOAD on *.* TO 'ashadozzaman'@'localhost' WITH GRANT OPTION;
```
Note that this statement also includes `WITH GRANT OPTION`. This will allow your MySQL user to grant any permissions that it has to other users on the system.

Warning: Some users may want to grant their MySQL user the ALL PRIVILEGES privilege, which will provide them with broad superuser privileges akin to the root user’s privileges, like so:
```
GRANT ALL PRIVILEGES ON *.* TO 'ashadozzaman'@'localhost' WITH GRANT OPTION;
```
Such broad privileges should not be granted lightly, as anyone with access to this MySQL user will have complete control over every database on the server.

Following this, it’s good practice to run the `FLUSH PRIVILEGES` command. This will free up any memory that the server cached as a result of the preceding CREATE `USER` and `GRANT` statements:
```
FLUSH PRIVILEGES;
exit
```
In the future, to log in as your new MySQL user, you’d use a command like the following:
```
mysql -u ashadozzaman -p
```
The `-p `flag will cause the MySQL client to prompt you for your MySQL user’s password in order to authenticate.

#### Finally, let’s test the MySQL installation.

## Step 4 — Testing MySQL
```
systemctl status mysql.service
```
- Output  Should running
- If MySQL isn’t running, you can start it with `sudo systemctl start mysql`.

For an additional check, you can try connecting to the database using the `mysqladmin` tool, which is a client that lets you run administrative commands. For example, this command says to connect as a MySQL user named `ashadozzman` (-u `ashadozzman`), prompt for a password (-p), and return the version. Be sure to change `ashadozzman` to the name of your dedicated MySQL user, and enter that user’s password when prompted:

```
sudo mysqladmin -p -u ashadozzaman version
```
``
Output
mysqladmin  Ver 8.0.28-0ubuntu4 for Linux on x86_64 ((Ubuntu))
Copyright (c) 2000, 2022, Oracle and/or its affiliates.
``

## Step 4 - Install MySQL Workbench
Now, we are all set to proceed with the MySQL Workbench installation on Ubuntu 22.04. To initiate the installation process, execute the below-provided command
```
sudo snap install mysql-workbench-community
```
After Complete process, click on the “Show Apps” icon, search for the “MySQL Workbench” in the search menu, and click on the desired app to launch it
## Conclusion
You now have a basic MySQL setup installed on your server. Here are a few examples of next steps you can take:

[Set up a LAMP stack](https://www.digitalocean.com/community/tutorials/how-to-install-linux-apache-mysql-php-lamp-stack-on-ubuntu-22-04) 

[Manage your MySQL installation with phpMyAdmin](https://www.digitalocean.com/community/tutorials/how-to-install-and-secure-phpmyadmin-on-ubuntu-22-04)

# **All Done!!!!!!!!! 🚀💥**







