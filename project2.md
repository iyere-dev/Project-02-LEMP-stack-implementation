# Project-02-LEMP-stack-implementation

## Installing NGNIX web server

update server package

`sudo apt update`

![updating packages](./images/installing_ngnix/updating_packages.png)

`sudo apt install nginx`

![installing nginx](./images/installing_ngnix/installing_nginx.png)

verify nginx is successfully installed and running

`sudo systemctl status nginx`

![verifying ngnix is installed and running](./images/installing_ngnix/verifying_nginx_installed_and_running.png)

edit inbound rules by opening TCP port 80 in Ubuntu instance

![opening TCP port 80](./images/installing_ngnix/opening_TCP_port_80.png)

Access server locally with curl command

curl http://localhost:80

![accessing server locally with curl command](./images/installing_ngnix/accessing_server_locally.png)

Test how  the nginx server responds to requests from the internet

[nginx server response from broser](http://3.126.207.206:80)

![nginx server response](./images/installing_ngnix/nginx_server_response.png)

### Installing MYSQL DBMS

Install mysql-server

`sudo apt install mysql-server`

![installing mysql-server](./images/installing_mysql/installing_mysql-server_page1.png)

![installing mysql-server page2](./images/installing_mysql/installing_mysql-server_page2.png)

Log in to mysql console

`sudo mysql`

run a security script that comes pre-installed with MySQL. This script will remove some insecure default settings and lock down access to your database system. Before running the script you will set a password for the root user, using mysql_native_password as default authentication method. We’re defining this user’s password as PassWord.1.

set password for rooy user in mysql console by running the script below

ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'PassWord.1';

![setting password for root user](./images/installing_mysql/setting_password_for_root_user.png)

run interactive script

`sudo_mysql_secure_installation`

![running interactive script](./images/installing_mysql/running_interactive_script.png)

test to see if you can log in to MySQL console

`sudo mysql -p`

![Test log in to MySQL console](./images/installing_mysql/test_log_in%20_to_MYSQL_console.png)

`exit`

[exiting mysql console](./images/installing_mysql/exiting_mysql_console.png)

INSTALL PHP

install php packages

`sudo apt install php-fpm php-mysql`

![installing php packages](./images/installing_php/installing_php_packages.png)

check that php has been installed

`php -v`

![checking php is installed](./images/installing_php/checking_php_is_installed.png)

CONFIGURE NGINX TO USE PHP PROCESSOR

create domain directory (to be called projectLEMP) within server block /vaw/www/html

`sudo mkdir /var/www/projectLEMP`

![creating domain directory](./images/configuring_nginx_to_use_php_processor/creating_domain_directory.png)

assign ownership of the directory with the $USER environment variable, which will reference your current system user

`sudo chown -R $USER:$USER /var/www/projectLEMP`

![assigning ownership of directory](./images/configuring_nginx_to_use_php_processor/assingning_ownwership_of_directory.png)

open a new configuration file in Nginx’s sites-available directory using nano editor

`sudo nano /etc/nginx/sites-available/projectLEMP`   

![pasting barebones configuration](./images/configuring_nginx_to_use_php_processor/barebones_configuration.png)

Activate the configuration by linking to the config file from Nginx’s sites-enabled directory

`sudo ln -s /etc/nginx/sites-available/projectLEMP /etc/nginx/sites-enabled/`

test configuration file for syntax errors

`sudo nginx -t`

![testing configuration for syntax errors](./images/configuring_nginx_to_use_php_processor/testing_configuration_for_syntax_errors.png)

disable default nginx host that is currently configured to listen on port 80

`sudo unlink /etc/nginx/sites-enabled/default`

reload nginx to apply the changes

`sudo systemctl reload nginx`

the new website is now active, but the web root /var/www/projectLEMP is still empty. Create an index.html file in that location so that we can test that your new server block works as expected

`sudo echo 'Hello LEMP from hostname' $(curl -s http://169.254.169.254/latest/meta-data/public-hostname) 'with public IP' $(curl -s http://169.254.169.254/latest/meta-data/public-ipv4) > /var/www/projectLEMP/index.html`

![creating index.html file to test new server block](./images/configuring_nginx_to_use_php_processor/creating_index.html_file_to%20test_new_server_block.png)

open url in browser with public IP

![opening url in browser with public IP](./images/configuring_nginx_to_use_php_processor/oepning_url_in_browser.png)

access website in browser with public DNS name

![accessing website with public DNS name](./images/configuring_nginx_to_use_php_processor/accessing_website_with_public_DNS_name.png)

TESTING PHP WITH NGINX

create test PHP file

`sudo nano /var/www/projectLEMP/info.php`

![pasting barbones config in php file created](./images/testing_php_with_nginx/pasting_barebones_configuration_in_php_file.png)

access info.php page with browser

![accessing info.php page with browser](./images/testing_php_with_nginx/accessing_info.php_page%20_with_browser.png)

after checking information on php in the webpage, remove the info.php filr for security reasons as it containd sensitive information

`sudo rm /var/www/projectLEMP/info.php`

![removing info.php page](./images/testing_php_with_nginx/removing_info.php_page.png)

RETRIEVING DATA FROM MYSQL DATABASE WITH PHP

connect to mysql console using the root account and create database (example database)

`sudo mysql -p`

![signing into mysql and creating example database](./images/retrieving_data_from_mysql_database_with_php/signing_into_mysql_database_and_creating_database.png)

create a new user and grant him  full priviledges on the database created

`CREATE USER 'example_user'@'%' IDENTIFIED WITH mysql_native_password BY 'password';`

![creating new user with password](./images/retrieving_data_from_mysql_database_with_php/creating_new_user_with_password.png)

give the new user created permission over the example database created (This will give the example_user user full privileges over the example_database database, while preventing this user from creating or modifying other databases on your server.)

![granting example user permissions](./images/retrieving_data_from_mysql_database_with_php/granting%20example_user_permissions.png)

`exit`

test if the new user has the proper permissions by logging in to the MySQL console again, this time using the custom user credentials

`mysql -u example_user -p`

![testing new user log in to mysql console](./images/retrieving_data_from_mysql_database_with_php/testing_new_user_login.png)

confirm access to database

`SHOW DATABASES;`

![confirming access to database](./images/retrieving_data_from_mysql_database_with_php/confirming_database_access.png)

create test table called todo_list

`CREATE TABLE example_database.todo_list (item_id INT AUTO_INCREMENT,content VARCHAR(255),PRIMARY KEY(item_id));`

![creating tabled named todo_list](./images/retrieving_data_from_mysql_database_with_php/creating_table.png)

Insert a few rows of content in the test table

![inserting rows of content](./images/retrieving_data_from_mysql_database_with_php/inserting_rows_of_content.png)

confirm that the data was successfully saved to the table

`SELECT * FROM example_database.todo_list;`

![confirming data was successfully saved to table](./images/retrieving_data_from_mysql_database_with_php/confirming%20_data_saved.png)

exit mysql console

`exit`

Now you can create a PHP script that will connect to MySQL and query for your content. Create a new PHP file in your custom web root directory using your preferred editor. We’ll use nano for that

`nano /var/www/projectLEMP/todo_list.php`

![saving barebones config with nano editor](./images/retrieving_data_from_mysql_database_with_php/saving_barebones_config.png)

access page in web browser

[accessing page in web browser](http://3.126.207.206/todo_list.php)

[todo_list page in web browser](./images/retrieving_data_from_mysql_database_with_php/accessing_todo_list_in_browser.png)

END OF PROJECT!