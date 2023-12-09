# How To Install Nginx webserver on Ubuntu 20.04 & 22.04

Once Nginx is installed, you can access the default welcome page by navigating to your server's IP address or domain in a web browser. If you want to serve your own website, you can place your files in the `/var/www/html` directory.

Remember to adjust firewall settings if needed to allow traffic on port 80 (HTTP) or 443 (HTTPS) if you plan to set up SSL.
1. Step 1: Open a terminal and update the package list to ensure you have the latest information about available packages.
    ```
	sudo apt update
    ```
2. Step 2: Use the following command to install Nginx.
    ```
	sudo apt install nginx
    ```
3. Step 3: Start Nginx: Once the installation is complete, start the Nginx service.
    ```
	sudo systemctl status nginx
    ```
4. Step 4: Enable Autostart: Enable Nginx to start on boot   
    ```
	sudo systemctl enable nginx
    ```
5. Step 5: Check Status: You can check the status to ensure everything is working as expected.
    ```
    sudo systemctl status nginx
    ```
6. Step 6: Basic Configuration: Nginx will now be running on server. The default web root is typically `/var/www/html`. Place website files in this directory. If need to modify the default Nginx configuration, you can edit the configuration file.
    ```
    sudo vim /etc/nginx/sites-available/default
    ```
7. Step 7: After Change anything need restart server
    ```
    sudo systemctl restart nginx
    ```
## It's All about default configure, bellow show custome configure
1. Step 1: Some Important Note For Live Server Configure:-
    - Must be change default port
    - Always try to ingore `root` user for login, create new user for configure. 

2. Step 2: Setting Up Server application root.\
`sudo mkdir -p /var/www/ashadozzaman.com`

3. Step 3: Create a sample index.html page using `vim` or your favorite editor and write some HTML tag.\
`vim /var/www/ashadozzaman.com/index.html`
	```
	<html>
	    <head>
	        <title>Welcome to Test Server!</title>
	    </head>
	    <body>
	        <h1>Success!  Yor Nginz server is working good!</h1>
	    </body>
	</html>
	```
4. Steps 4: Create a server block with the correct directives. Instead of modifying the default configuration file directly.\
` sudo vim /etc/nginx/sites-available/ashadozzaman.com`
	```
	### Add this into ashadozzaman.com
	#
	server {
		 listen 80;
		 listen [::]:80;
		 
		 root /var/www/ashadozzaman.com;

		 # Add index.php to the list if you are using PHP

		 index index.html index.htm index.php;

		 server_name ashadozzaman.com www.ashadozzaman.com;

		 access_log /var/log/nginx/ashadozzaman.com.access.log;
		 error_log /var/log/nginx/ashadozzaman.com.error.log;

		 location ~ \.php$ {
			include snippets/fastcgi-php.conf;
			fastcgi_pass unix:/var/run/php/php8.1-fpm.sock;
		 }
		 location / {
			#limit_conn concurrent 5;
			#limit_req zone=mylimit burst=5 nodelay;
			try_files $uri $uri/ /index.php?$args;
		 }
		  
		 #Client Side Cashing Configuration
		 location ~* \.(js|jpg|jpeg|gif|png|css|tgz|gz|rar|bz2|doc|pdf|ppt|tar|wav|bmp|rtf|swf|ico|flv|txt|woff|woff2|svg)$ {
            expires 90d;
            add_header Pragma public;
            add_header Cache-Control public;
            add_header Vary Accept-Encoding;
		 }
		 location @/ {
		    rewrite ^/(.+)$ /index.php?_route_=$1 last;
		 }
		 # Block a single IP address
		 #deny 103.120.35.2;
		 location ~ /\.env {
		    deny all;
		 }
		 location ~ /\. {
		    deny all;
		 }
	}

	```
5. Steps 5: Enable the file by creating a link from it to the `sites-enabled` directory, which Nginx reads from during startup.\
\
	`sudo ln -s /etc/nginx/sites-available/ashadozzaman.com /etc/nginx/sites-enabled/`

6. Steps 6: Test to make sure that there are no syntax errors in any of your Nginx files and restart server.
	```
	sudo nginx -t
	sudo nginx -s reload
	sudo systemctl restart nginx
	```
7. Steps 7: 

	- Insert A & CNAME record in your **domain** and Server **Public IP**
	- Adjusting your Firewall
	- Adjust Other Nginx custom configuration, this is very basic configuration.

#### Advance configaretion Loading...🚀
