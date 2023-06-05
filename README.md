# 1. DevOps-Deploy-WordPress-with-Amazon-RDS-and-install-MySQL
![image](https://github.com/HoangGuruu/AWS-Deploy-WordPress-with-Amazon-RDS-and-install-MySQL/assets/111829092/f7a97342-c67f-4ccb-853c-9037e9d4ea6e)
# 2. Link Youtube

# 3. The necessary links for the project
### Link Hands-on AWS for this project - However it's not use ubuntu - So i will use Ubuntu for this project
https://aws.amazon.com/getting-started/hands-on/deploy-wordpress-with-amazon-rds/
### Install Apache by Ubuntu
https://ubuntu.com/server/docs/web-servers-apache
### Install PHP Ubuntu
https://ubuntu.com/server/docs/programming-php
### Install MySQL server
https://ubuntu.com/server/docs/databases-mysql
### Install and configure WordPress
https://ubuntu.com/tutorials/install-and-configure-wordpress#1-overview
### How To Secure Apache with Let's Encrypt on Ubuntu 20.04
https://www.digitalocean.com/community/tutorials/how-to-secure-apache-with-let-s-encrypt-on-ubuntu-20-04

### All the commands that are executed in the above youtube video are mentioned in this gist. 

#### Note :
- Allow MySQL with security group EC2
- Have a Domain
- - Find script in tutorial of web

1. Install Apache server on Ubuntu
```
sudo apt install apache2
```
2. Install php runtime and php mysql connector
```
sudo apt install php libapache2-mod-php php-mysql
```
3. Install MySQL server
```
sudo apt install mysql-server 
```
4. Login to MySQL server
```
sudo mysql -u root
```
5. Change authentication plugin to mysql_native_password (change the password to something strong)
```
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password by 'Testpassword@123';
```
6. Create a new database user for wordpress (change the password to something strong)
```
CREATE USER 'wp_user'@localhost IDENTIFIED BY 'Testpassword@123';
```
7. Create a database for wordpress
```
CREATE DATABASE wp;
```
8. Grant all privilges on the database 'wp' to the newly created user
```
GRANT ALL PRIVILEGES ON wp.* TO 'wp_user'@localhost;
```
9. Download wordpress
```
cd /tmp
wget https://wordpress.org/latest.tar.gz
```
10. Unzip
```
tar -xvf latest.tar.gz
# or
unzip latest.tar.gz
```
11. Move wordpress folder to apache document root
```
sudo mv wordpress/ /var/www/html
```

### Then check public ip/wordpress 
- Let's go
 Database Name wp
 Username wp_user
 Password Testpassword@123
 Database Host localhost
 Table Prefix wp_

- Copy and create a wp-config.php with this script
- Run installation
- And fill the blank with your information

### If you want to use wordpress as Main Page
```
cd /etc/apache2/sites-available/
sudo nano 000-default.conf
```
#### Change
```
DocumentRoot /var/www/html/wordpress
```
12. Command to restart/reload apache server
```
sudo systemctl restart apache2
OR
sudo systemctl reload apache2
```
### If you want to use your domain
```
cd /etc/apache2/sites-available/
sudo nano 000-default.conf
```
#### Ignore
```
DocumentRoot /var/www/html/wordpress
```
#### Add
```
# mysamplewebsite.online this is domain
ServerName mysamplewebsite.online
ServerAlias www.mysamplewebsite.online
```
#### Then
```
sudo systemctl restart apache2
OR
sudo systemctl reload apache2
```

### Then we got ip/wp-admin -> Sign in -> Setting -> General Settings -> Change domain
13. Install certbot
```
sudo apt-get update
sudo apt install certbot python3-certbot-apache
```
14. Request and install ssl on your site with certbot
```
sudo certbot --apache
```
