# MySQL enforces a password policy to enhance security. 

To change the password policy for the MySQL root user, you need to modify the password validation plugin and adjust the policy settings. Here are the steps.

## Connect to MySQL:
```
sudo mysql -u root -p
```
## Check Current Password Policy

To check the current password policy settings, run the following query:
```
SHOW VARIABLES LIKE 'validate_password%';
```
This query will display information about the validate_password plugin and its settings.

## Modify Password Policy
To modify the password policy, you can use the `SET GLOBAL` command. For example, if you want to set a lower length requirement, you can do the following:-
```
SET GLOBAL validate_password.length = 8;
```
Adjust other settings as needed, such as `validate_password_policy` for policy strength.
```
SET GLOBAL validate_password_policy = LOW; //medium
```
## Update User Password
```
ALTER USER 'root'@'localhost' IDENTIFIED BY 'new_password';
```
Replace `new_password` with your desired password.

Note: After making these changes, you should be able to set a new password for the MySQL root user without encountering the password policy error.

Remember to consider security best practices when adjusting password policies and ensure that your passwords are strong and meet your organization's security requirements.


## All Done 🚀💥
