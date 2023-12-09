# How To Install the Apache Web Server on Ubuntu 22.04

---

1.  **Step 1: Installing Apache**
    Update our local package index so that we have access to the most recent package listings. Afterwards, we can install Apache.

    ```bash
    sudo apt update
    sudo apt install apache2
    sudo systemctl status apache2
    sudo systemctl enable apache2
    ```

2.  **Step 2: Verify Apache Installation.**

    ```
    http://server_ip_address
    http://127.0.0.1/
    ```

3.  **Step 3: Setting Up Server Application Root.**
    ```bash
    sudo mkdir -p /var/www/shovoua.com
    ```
4.  **Step 4: Create a shovoua.com index.html Page**
    ```
    sudo vim /var/www/shovoua.com/index.html
    ```
    ```
    <html>
             <head>
                 <title>Welcome to Your Test Server!</title>
             </head>
             <body>
                 <h1>Success! The `shovoua.com` server is working!</h1>
             </body>
     </html>
    ```
5.  **Step 5: Create a Server Block Virtual Hosts**
    ```
    sudo vim /etc/apache2/sites-available/shovoua.com.conf
    ```

    ```

    <VirtualHost \*:80>
        ServerAdmin webmaster@localhost
        ServerName shovoua.com
        ServerAlias www.shovoua.com
        DocumentRoot /var/www/shovoua/

        # Customizing ErrorLog and CustomLog
        ErrorLog /var/log/apache2/shovoua.log
        CustomLog /var/log/apache2/shovoua.log combined
    </VirtualHost>
    ```
    ````
        # The ServerName directive sets the request scheme, hostname and port that
        # the server uses to identify itself. This is used when creating
        # redirection URLs. In the context of virtual hosts, the ServerName
        # specifies what hostname must appear in the request's Host: header to
        # match this virtual host. For the default virtual host (this file) this
        # value is not decisive as it is used as a last resort host regardless.
        # However, you must set it for any further virtual host explicitly.
        #ServerName www.example.com

        ServerAdmin webmaster@localhost
        DocumentRoot /var/www/html

        # Available loglevels: trace8, ..., trace1, debug, info, notice, warn,
        # error, crit, alert, emerg.
        # It is also possible to configure the loglevel for particular
        # modules, e.g.
        #LogLevel info ssl:warn

        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined

        # For most configuration files from conf-available/, which are
        # enabled or disabled at a global level, it is possible to
        # include a line for only one particular virtual host. For example the
        # following line enables the CGI configuration for this host only
        # after it has been globally disabled with "a2disconf".
        #Include conf-available/serve-cgi-bin.conf
    ````
### Note: For local setup must be follow `No-9` step.

6.  **Steps 6: Enable the File and Reload Apache.** Enable the file by creating a link from it to the sites-enabled directory, which Apache reads from during startup.

    ```bash
    sudo a2ensite shovoua.com.conf
    sudo systemctl reload apache2
    ```

7.  **Steps 7: Test and Restart Apache**. Test to make sure that there are no syntax errors in any of your Apache files and restart the server.

    ```bash
    sudo apache2ctl configtest
    sudo apachectl -k graceful
    sudo systemctl restart apache2
    ```

8.  **Steps 7: Additional Configuration**

    - Insert A & CNAME records in your domain and Server Public IP
    - Adjusting your Firewall
    - Other Apache2 custom configurations; this is a very basic configuration.

9. **ServerName in hosts file (Optional):**
    - For run local env it's must be needed.
    ```
    sudo vim /etc/hosts
    ```
    - Add test domain in your host file.
    ```
    127.0.0.1   shovoua.xyz www.shovoua.xyz
    ```

  **All Done!!!!!!!!! 🚀💥**
