**This a project base on :**

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
