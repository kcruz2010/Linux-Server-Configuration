## **This  project base on :**
Reference:
[https://docs.google.com/document/d/1J0gpbuSlcFa2IQScrTIqI6o3dice-9T7v8EDNjJDfUI/pub?embedded=true]

- the securing and configuring the Linux server
- Deploy project 3 restaurant menu app using Apache web server, Flask python Frame work, and PostgreSQL

## **Server info:**
- Server IP address: 56.36.114.47
- SSH port : 2200
- URL  to Restaurant Menu App: ec2-52-36-114-47.us-west-2.compute.amazonaws.com

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

`grader@ip-10-20-3-215: cd /var/www`

`grader@ip-10-20-3-215: cd /var/www$ sudo mkdir Catalog`

## **Install and configure PostgreSQL**
Reference: [https://www.digitalocean.com/community/tutorials/how-to-secure-postgresql-on-an-ubuntu-vps]
- Install the PostgreSQL database:

`(venv) grader@ip-10-20-3-215:/var/www/Catalog/catalog$ sudo apt-get install postgresql postgresql-contrib`

- No remote connections are allowed. It should be default

`(venv) grader@ip-10-20-3-215:/var/www/Catalog/catalog$ sudo nano /etc/postgresql/9.3/main/pg_hba.conf`

- Open your project 3 `database_setup.py` file:

`(venv) grader@ip-10-20-3-215:/var/www/Catalog/catalog$ sudo nano database_setup.py`

- Change syntax:

 `engine = create_engine('sqlite:///YOUR-DATABASE-NAME.db')` to 
 
 `engine = create_engine('postgresql://catalog:DB-PASSWORD@localhost/catalog')`
 
- Note: change  password from DB-PASSWORD to grader

- Rename your `app.py` to `__init__.py`

`(venv) grader@ip-10-20-30-101:/var/www/Catalog/catalog$ mv YOUR_APP.py __init__.py`
    `
    
    *Note*:  If you make that change above, make sure your 'catalog.wsgi` file reflects this change. It should read like so:
    
    ```python
    #!/user/bin/python
    import sys
    import logging
    logging.basicConfig(stream=sys.stderr)
    sys.path.insert(0,"/var/www/Catalog/catalog/")

    from __init__ import app as application
    application.secret_key = 'Add your secret key'
    ```
    
    If you did not make the above changes, then `catalog.wsgi` should have whatever application_name.py in your project 3 file that contains your `app = Flask(__name__)` so that it can be imported as application in the `catalog.wsgi` file.


## **Create a new user: catalog, add user to PostgreSQL databse with limited permissions to catalog application database.**
- Create a user `catalog` for psql:

    ```
    (venv) grader@ip-10-20-3-215:/var/www/Catalog/catalog$ sudo adduser catalog
    
    choose a password for that user.
    ```
    
- Change to the default user `Postgres`

    ```
    (venv) grader@ip-10-20-30-101:/var/www/Catalog/catalog$ sudo su - postgres
    postgres@ip-10-20-25-175:~$ 
    ```
    
    Connect to the postgres system:
    
    ```
    postgres@ip-10-20-30-101:~$ psql
    ```
    
    You see this:
    
    ```
    psql (9.3.12)
    Type "help" for help.

    postgres=# 
    ```
    
- Add the postgres user: `catalog` with a `login role` and `password`
    
    ```
    postgres=# CREATE USER catalog WITH PASSWORD 'DB-PASSWORD';
    ```
    *Note* : The *DB-PASSWORD*, should be the same password you used to create the postgresql engine in your database_setup.py file.(grader)
    
 - Allow the user `catalog` to be able to create databse tables
    
    ```
    postgres=# ALTER USER catalog CREATEDB;
    ```
- You can list the roles available in postgres, and their attribute:
    
    ```
    postgres=# \du
    ```
    
- Create a new database called `catalog` for the user: `catalog`:

    ```
    postgres=# CREATE DATABASE catalog WITH OWNER catalog;
    ```
    
-  Connect to the database:

    ```
    postgres=# \c catalog
    ```
    
- Revoke all rights on the database schema, and grant access to catalog only.

    ```
    catalog=# REVOKE ALL ON SCHEMA public FROM public;
    catalog=# GRANT ALL ON SCHEMA public TO catalog;
    ```
    
    Exit Postgresql and postgres user:
    
    ```
    postgres=# \q
    postgres@ip-10-20-3-215~$ exit
    ```
    
- Create Postgresql database schema:

    ```
    (venv) grader@ip-10-20-3-215:/var/www/Catalog/catalog$ python database_setup.py
    ```
    
    We can check that it worked. After you run `database_setup.py`, Go back to your postgres schema, and connect to `catalog` database.
    
    ```
    postgres@ip-10-20-3-215:~$ psql
    psql (9.3.12)
    Type "help" for help.

    postgres=# \c catalog
    ```
    
    When you conect to the `catalog` database, you can view all the relations created by your `python database_setup.py` command.
    
    ` catalog=# \dt`
 
    
    Now exit postgres, and return to Virtual environment.
    
-  Restart Apache:

    ```
    (venv) grader@ip-10-20-3-215:/var/www/Catalog/catalog$ sudo service apache2 restart
    ```
    
    Open  browser, put in PUBLIC-IP-ADDRESS : `52.36.114.47`.  Start Restaurant App

## **Get OAUTH-LOGINS (Google+ and Facebook) working**
- Update Google+  and Facebook client_secrets in json by `adding r'/var/www/Catalog/catalog`  and `/var/www/catalog/catalog`

`CLIENT_ID = json.loads(
    open(r'/var/www/Catalog/catalog/client_secrets.json', 'r').read())['web']['client_id']
APPLICATION_NAME = "Restaurant Menu Application"`

 `oauth_flow = flow_from_clientsecrets('/var/www/Catalog/catalog/client_secrets.json', scope ='')`

 `app_id = json.loads(open('/var/www/Catalog/catalog/fb_client_secrets.json', 'r').read())[
        'web']['app_id']
    app_secret = json.loads(
        open('/var/www/Catalog/catalog/fb_client_secrets.json', 'r').read())['web']['app_secret']`

- Go to  http://www.hcidata.info/host2ip.cgi to get a host name for your public ip Address 52.36.114.47 to 52-36-114-47.us-west-2.compute.amazonaws.com

- Edit `Catalog.conf` by adding ServerAlias 52-36-114-47.us-west-2.compute.amazonaws.com

`<VirtualHost *:80>

    ServerName 52.36.114.47
    
    ServerAdmin grader@52.36.114.47
    
    ServerAlias ec2-52-36-114-47.us-west-2.compute.amazonaws.com
    
    WSGIScriptAlias / /var/www/Catalog/catalog.wsgi
    
    <Directory /var/www/Catalog/catalog/>
    
        Order allow,deny
        
        Allow from all
        
    </Directory>
    
    Alias /static /var/www/Catalog/catalog/static
    
    <Directory /var/www/Catalog/catalog/static/>
    
        Order allow,deny
        
        Allow from all
        
    </Directory>
    
    ErrorLog ${APACHE_LOG_DIR}/error.log
    
    LogLevel warn
    
    CustomLog ${APACHE_LOG_DIR}/access.log combined
    
</VirtualHost>`

- Update Oauth authorized JavaScript origins  by going to http://console.developers.google.com/

- Under Credentials edit your 0Auth 2.0 client IDs and add 

`http://52.36.114.47/`

`http://ec2-52-36-114-47.us-west-2.compute.amazonaws.com`

- Update Facebook authorization by adding 

`http://52.36.114.47/` on the site URL



## **Run your app on amazonaws.**
- ec2-52-36-114-47.us-west-2.compute.amazonaws.com

Third party resource: [elnobun] (https://github.com/elnobun/Linux-Server-Configuration/blob/master/README.md)
