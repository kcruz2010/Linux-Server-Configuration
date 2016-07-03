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

## **Setup Environment**
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
 
## **Create a New User with sudo permissions**
Reference:
[https://www.digitalocean.com/community/tutorials/how-to-add-and-delete-users-on-an-ubuntu-14-04-vps]

- Create new user:grader
 
 `root@ip-10-20-3-15:~# adduser grader`

- Give sudo permission: open sudoer config file
 
 `root@ip-10-20-3-15:~# visudo`

- Add new user `grader` once you open nano editor and  add `grader ALL=(ALL:ALL)`  under root `root ALL=(ALL:ALL)`

`root ALL=(ALL:ALL)`

`grader ALL=(ALL:ALL)`

- Save changes `ctrl+x, y` then hit the `Enter` key
 
## **Update and upgraded all current packages**

- Update all current available packages:
 
`root@ip-10-20-3-215:~# sudo apt-get update`

- Install unattended-upgrade packages:

`root@ip-10-20-3-215:~# sudo apt-get upgrade`

- Install unattended-upgrade packages:

`root@ip-10-20-3-215:~# sudo apt-get install unattended-upgrades`

- Enable the unattended-upgrade packages:

`root@ip-10-20-3-215:~# sudo dpkg-reconfigure -plow unattended-upgrades`


## **Configure SSH access change ssh port 22 to port 2200**
Reference [http://askubuntu.com/questions/16650/create-a-new-ssh-user-on-ubuntu-server]

- Configure SSH file by using nano editor:

`root@ip-10-20-3-215:~# nano /etc/ssh/sshd_config`

- In nano editor change:

`Port 22` to `Port 2200`

`PermitRootLogin without-password` to `PermitRootLogin no`

 Temporarily change `PasswordAuthentication no` to `PasswordAuthentication yes`
 
 Add `UseDNS no` and `AllowUsers grader` at the end of the file. Allow grader for SSH login access
 
 - Exit nano editor: `ctrl+x, y` then hit `enter` key

 - Restart SSH for update changes:
 
`root@ip-10-20-3-215:~# sudo service apache ssh restart`

 - Connect your new 'user' `grader` from your local terminal:
 
`root@ip-10-20-3-215:~# sudo service ssh restart`

 - Connect to `your local terminal (ubuntu) :~ ssh grader@52.36.114.47 -p 2200`
 
 - Create a SSH key pair
 
Reference: [https://www.digitalocean.com/community/tutorials/how-to-set-up-ssh-keys--2]

## **Configure UFW only allowing connections for SSH (Port: 2200), HTTP(Port: 80) and NTP (Port: 123)**
Reference:[https://help.ubuntu.com/community/UFW]

- Change  the status of UFW. Make sure it is `inactive`:

`grader@ip-10-20-3-215:~$ sudo ufw status`

-  Deny all incoming connections and allow the ones we need

grader@ip-10-20-3-215:~$ sudo ufw status` default deny incoming`

-Allow incoming connections : SSH (PORT: 220), HTTP (PORT:80), NTP (PORT:123)

`grader@ip-10-20-3-215:~$ sudo ufw allow 2200/tcp`

`grader@ip-10-20-3-215:~$ sudo ufw allow 80/tcp`

`grader@ip-10-20-3-215:~$ sudo ufw allow 123/udp`

- Enable firewall:

`grader@ip-10-20-3-215:~$ sudo ufw enable`

## **Configure Local time zone to UTC**
Reference:[https://help.ubuntu.com/community/UbuntuTime#Using_the_Command_Line_.28terminal.29]

- Access timezone dialog box

`grader@ip-10-20-3-215:~$ sudo dpkg-reconfigure tzdata`

-Select `None of the above` then hit the 'Enter' key choose UTC

-setup `ntp daemon` to improve time sync:

`grader@ip-10-20-3-215:~$ sudo apt-get install ntp`

## **Install and Configure Apache to serve a Python mod_wsgi application.**


- Install Apache

`grader@ip-10-20-3-215:~$ sudo apt-get install apache2`

- Browser enter `http://52.36.47.114` and will set up a 'It Works!'

-Install 'mod_wsgi' 'python-setup tools'

`grader@ip-10-20-3-215:~$  sudo apt-get install python-setuptools libapache2-mod-wsgi`

- Configure Apache to handle  requests using the 'WSGI' model

Reference: [https://classroom.udacity.com/nanodegrees/nd004/parts/00413454014/modules/357367901175461/lessons/4340119836/concepts/48018692630923]

`grader@ip-10-20-3-215:~$  sudo cat /etc/apache2/sites-enabled/000-default.conf`

- Add WSGIScriptAlias line : WSGIScriptAlias / /var/www/html/myapp.wsgi at the tail end of <VirtualHost *:80> block, right before the closing </VirtualHost>. Now save and quit the nano editor.

- Restart Apache:

`grader@ip-10-20-3-215:~$ sudo apache2ctl restart`

## **Setup Environment to Deploy Flask Application**
Reference: [https://www.digitalocean.com/community/tutorials/how-to-deploy-a-flask-application-on-an-ubuntu-vps]

- Add additional Python Packages to enable Apache serve Flask Applications

`grader@ip-10-20-3-215:~$  sudo apt-get install libapache-mod-wsgi python-dev`

- Enable mod_wsgi

`grader@ip-10-20-3-215:~$  sudo a2enmod wsgi`

- Set up a directory folder for our app call it `Catalog`

`
## **Install and configure PostgreSQL**
## **Create a new user: catalog, add user to PostgreSQL databse with limited permissions to catalog application database.**
## **Get OAUTH-LOGINS (Google+ and Facebook) working**
## **Run your app on amazonaws.**

