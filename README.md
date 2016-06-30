## **This  project base on :**
Reference:
[https://docs.google.com/document/d/1J0gpbuSlcFa2IQScrTIqI6o3dice-9T7v8EDNjJDfUI/pub?embedded=true]

- the securing and configuring the Linux server
- Deploy project 3 restaurant menu app using Apache web server, Flask python Frame work, and PostgreSQL

## **Server info:**
- Server IP address: 56.36.114.47
- SSH port : 2200
- URL  to Restaurant Menu App:

## **Packages installed**

- Tmux
- finger
- Apache2
- git 
- postgresql
- flask
- python-setuptools
- sqlalchemy
- python-psycopg2
- oauth2
- google-api-python client
- failban2
- glances

## **Configuration Overview**

- Set up environment provided  by Udacity by launching  you virtual machine and ssh into the server
- Create user by adding new user  "grader' and grant "grader" sudo  permissions
- Update all current  installed packages
- Change SSH Port from 22 to 2200
- Configure UFW  to only allow incoming connections  SSH (Port:2200), HTTP(Port:80),  and NTP (Port:123)
- Configure Local Time Zone  to UTC
- Install and configure  Apache to serve a Python mod_wsgi application
- Install and configure PostgreSQL
- Install Git and clone  project 3 restaurant menu app so that it functions correctly when you visit server's Ip address in the browser

## 1.**Setup Environment**
Reference:
[https://www.udacity.com/account#!/development_environment]

 1. Public Id and private key provided by udacity
 2. Download rsa private key provided  by udacity
 3. Safe private key' under .ssh folder :
   `C:\Users\Kenneth\.ssh\udacity_key.rsa`
 4. Allow to 'read' and 'write' file :
   `$ chmod 600 ~/.ssh/udacity_key.rsa`
 5. SSH instance:
   `$ ssh -i ~/.ssh/udacity_key.rsa  root@52.36.114.47` 
 
## 2.**Create a New User with sudo permissions**
## 3.**Update and upgraded all current packages**
## 4.**Configure SSH access change ssh port 22 to port 2200**
## 5.**Configure UFW only allowing connections for SSH (Port: 2200), HTTP(Port: 80) and NTP (Port: 123)**
## 6.**Configure Local time zone to UTC**
## 7.**Install and Configure Apache to serve a Python mod_wsgi application**
## 8.**Install Git and Setup Environment for deloplying Flask Application**
## 9.**Install and configure PostgreSQL**
## 10.**Create a new user: catalog, add user to PostgreSQL databse with limited permissions to catalog application database.**
## 11.**Get OAUTH-LOGINS (Google+ and Facebook) working**
## 12. **Run your app on amazonaws.**

