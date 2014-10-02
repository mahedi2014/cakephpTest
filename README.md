cakephpTest
===========
Cake php basic configuration
================================
####Set configuration
-Make a folder under /app/ as name 'tmp' and run command in terminal
 ```
 chmod 777 /var/www/test/cakephp-basic/app/tmp -R
 ```

-Change in app/Config/core.php  to 'Security.salt' value like DYhG93b0qyJfIxfs2guVoUubWwvniR2G0FgaC9mi2014

-Change in app/Config/core.php  to 'Security.cipherSeed' value like 768593096574535424967496836452014


####Create a host in nginx
-Set virtual host on /etc/nginx/site-available/default See http://book.cakephp.org/2.0/en/installation/url-rewriting.html or copy bellows code and set root to /app/webroot
(here my domain is cakephpbasic.dev and root folder isn cakephp-basic)
```
 	server {
 		listen 80;
 		server_name cakephpbasic.dev;
 		root /var/www/test/cakephp-basic/app/webroot;

 		access_log /var/log/nginx/cakephp-basic.access.log;
 		error_log /var/log/nginx/cakephp-basic.error.log;

 		location / {
 			index index.php;
 			try_files $uri $uri/ /index.php?$args;
 		}

 		location ~ \.php/?(.*)$ {
 			fastcgi_connect_timeout 300s; # default of 60s is just too long
 			fastcgi_read_timeout 300s; # default of 60s is just too long
 			fastcgi_pass unix:/var/run/php5-fpm.sock;
 			fastcgi_index index.php;
 			include fastcgi_params;
 			fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
 		}
 		#Access phpmyadmin
 		location /phpmyadmin {
 			root /usr/share/;
 			index index.php index.html index.htm;
 			location ~ ^/phpmyadmin/(.+\.php)$ {
 				try_files $uri =404;
 				fastcgi_pass unix:/var/run/php5-fpm.sock;
 				include fastcgi_params;
 			}
 		}

 	}


```

-Set host ip in /etc/hosts
```
127.0.1.1	cakephpbasic.dev
```