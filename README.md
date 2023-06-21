# Install and Secure phpMyAdmin with LAMP Stack on Ubuntu 20.04 LTS

## Introduction

phpMyAdmin is a web-based open-source database administration tool for MySQL and MariaDB servers. You can use it to easily manage databases, tables, indices, users, permissions, and more, without touching the command-line interface.

With its intuitive web interface, phpMyAdmin allows you to import and export data in various formats, including CSV and plain text SQL, making it one of the best GUI-based database management software.

In this tutorial, you'll install, configure and secure the phpMyAdmin package with a LAMP stack on your Ubuntu 20.04 LTS server.

# 1. Install the phpMyAdmin Package
SSH to your Ubuntu server and update the package repository index.
```sh 
$ sudo apt update -y
```
Make sure your system has the following required PHP extensions.
```sh
$ sudo apt install -y php-json php-mbstring php-zip php-gd php-curl
```
Install the phpmyadmin package.
```sh 
$ sudo apt install -y phpmyadmin
```
![image](https://github.com/vinayakz/Install-phpMyAdmin-on-Ubuntu/assets/33689324/41a5756c-436f-4d13-9329-b18422be1ec4)

![image](https://github.com/vinayakz/Install-phpMyAdmin-on-Ubuntu/assets/33689324/b5e9f2e3-78ae-4ca2-bda2-6e0728c8ba78)

Enter a strong password for the phpMyAdmin package.

![image](https://github.com/vinayakz/Install-phpMyAdmin-on-Ubuntu/assets/33689324/cbeaff72-531b-4908-a403-aa3d99cea2d2)

Repeat the same password to finalize the installation process.

![image](https://github.com/vinayakz/Install-phpMyAdmin-on-Ubuntu/assets/33689324/7111f9c0-f9f4-417d-93ca-d330a302d925)

Use the a2enconf command to enable the new configuration file created by the phpMyAdmin.

```sh 
$ sudo ln -s /etc/phpmyadmin/apache.conf /etc/apache2/conf-available/phpmyadmin.conf

$ sudo a2enconf phpmyadmin.conf
```

Restart Apache to load the new configuration file.

```sh
$ sudo systemctl restart apache2
```

With the phpMyAdmin package installed, you'll create a sample database and a user next to demonstrate the login process via a web browser.

## 2. Set up a Sample Database and User

Log in to your MySQL server as root via the command-line interface.
```sh
$ sudo mysql -u root -p
```
Enter your MySQL root password and press ENTER to proceed.

Create a sample_db database.

```sh 
mysql> CREATE database sample_db;
```
Create a test_user for the sample_db and exit from the command-line interface. Use the command for your database engine, either MySQL or MariaDB.
MySQL.
```sh
mysql> CREATE USER 'test_user'@'localhost' IDENTIFIED WITH mysql_native_password BY 'EXAMPLE_PASSWORD';

mysql> GRANT ALL PRIVILEGES ON sample_db.* TO 'test_user'@'localhost';

mysql> FLUSH PRIVILEGES;

mysql> QUIT;
```
MariaDB.
```sh
MariaDB> GRANT ALL PRIVILEGES on sample_db.* TO 'test_user'@'localhost' identified by 'EXAMPLE_PASSWORD';

MariaDB> QUIT;
```
Navigate to the URL below in a web browser to test the installation. Replace 192.0.3.1 with the correct domain name or public IP address of your server.
```sh
http://192.0.3.1/phpmyadmin
```
Then enter the credentials of the test_user you've just created to log in.
