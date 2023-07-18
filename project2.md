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

