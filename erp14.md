
**STEP 1** `Install git`
```
sudo apt-get install git
```

**STEP 2** `install python-dev`
```
sudo apt-get install python3-dev
```

**STEP 3** `Install setuptools and pip (Python's Package Manager).`
```
sudo apt-get install python3-setuptools python3-pip
```

**STEP 4** `Install virtualenv`
```
sudo apt-get install virtualenv
sudo apt install python3.10-venv
```

**STEP 5** `Install MariaDB`
```
sudo apt-get install software-properties-common
sudo apt install mariadb-server
sudo mysql_secure_installation
```

  In order to log into MariaDB to secure it,
   we'll need the current
  password for the root user. 
  If you've just installed MariaDB, and
  haven't set the root password yet, 
  you should just press enter here.
  Enter current password for root (enter for none): # PRESS ENTER
  OK, successfully used password, moving on...
  `Switch to unix_socket authentication` [Y/n] Y

  
  Enabled successfully!
  Reloading privilege tables..
   ... Success!
  Change the root password? [Y/n] Y
  New password: 
  Re-enter new password: 
  Password updated successfully!
  Reloading privilege tables..
   ... Success!
   
  Remove anonymous users? [Y/n] Y
   ... Success!
   
   Disallow root login remotely? [Y/n] Y
   ... Success!
   
   Remove test database and access to it? [Y/n] Y
    Dropping test database...
   ... Success!
   
    Removing privileges on test database...
   ... Success!
   
   Reload privilege tables now? [Y/n] Y
   ... Success
   
**STEP 6** `MySQL database development files`
```
sudo apt-get install libmysqlclient-dev
```
**STEP 7** `Edit the mariadb configuration ( unicode character encoding )`
```
sudo nano /etc/mysql/mariadb.conf.d/50-server.cnf
```
>add this to the 50-server.cnf file
```
[mysql]
default-character-set = utf8mb4

[mysqld]
character-set-client-handshake = FALSE
character-set-server = utf8mb4
collation-server = utf8mb4_unicode_ci
innodb_read_only_compressed = FALSE   

[server]
user = mysql
pid-file = /run/mysqld/mysqld.pid
socket = /run/mysqld/mysqld.sock
basedir = /usr
datadir = /var/lib/mysql
tmpdir = /tmp
lc-messages-dir = /usr/share/mysql
bind-address = 127.0.0.1
query_cache_size = 16M
log_error = /var/log/mysql/error.log
```
```
sudo nano /etc/mysql/my.cnf
```
>add this to the my.cnf file
```
[mysqld]
character-set-client-handshake = FALSE
character-set-server = utf8mb4
collation-server = utf8mb4_unicode_ci
innodb_read_only_compressed = FALSE   
 ```
 ```
sudo service mysql restart
sudo systemctl restart mysqld
```
**STEP 8** `install Redis`
```
sudo apt-get install redis-server
```
**STEP 9** `install Node.js 14.X package`
```
sudo apt install curl 
```
```
curl https://raw.githubusercontent.com/creationix/nvm/master/install.sh | bash
source ~/.profile
nvm install 16
```

**STEP 10** `install Yarn`
```
sudo apt-get install npm
sudo npm install -g yarn
```
**STEP 11** `install wkhtmltopdf`
```
sudo apt-get install xvfb libfontconfig wkhtmltopdf
```
**STEP 12** `install frappe-bench`
```
sudo -H pip3 install frappe-bench==5.10.1

bench --version
```

**STEP 13** `initilise the frappe bench & install frappe latest version`
```
bench init frappe-bench --frappe-branch version-14
cd frappe-bench/
bench start
```
**STEP 14** `create a site in frappe bench`
```
bench new-site sitename
bench use sitename
```

**STEP 15** `install ERPNext latest version in bench & site`
```
bench get-app https://github.com/frappe/erpnext --branch version-14
bench --site sitename install-app erpnext
bench start
```
**Step 16** `setup production`
```
sudo bench setup production $USER
bench restart
```

If bench restart is not worked run the following command again with all Questions Yes
```
sudo bench setup production $USER
```
if js and css file is not loading on login window run the following command
```
sudo chmod o+x /home/$USER
```
```
bench restart
```
#STOP Production Mode
