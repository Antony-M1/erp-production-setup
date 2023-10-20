# Reference Document
* [[Guide] How to install ERPNext v14 on Linux Ubuntu (step-by-step instructions)](https://discuss.frappe.io/t/guide-how-to-install-erpnext-v14-on-linux-ubuntu-step-by-step-instructions/92960/226)
* [Frappe-ERPNext-Version-14--in-Ubuntu-22.04-LTS](https://github.com/D-codE-Hub/Frappe-ERPNext-Version-14--in-Ubuntu-22.04-LTS)


# Get Started
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
  Reloading privilege tables
  
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
```
After move into the `frappe-bench` run this commands
```
bench set-config -g db_host mariadb
bench set-config -g redis_cache redis://redis-cache:6379
bench set-config -g redis_queue redis://redis-queue:6379
bench set-config -g redis_socketio redis://redis-socketio:6379
```
Start the bench
```
bench start
```
**STEP 14** `create a site in frappe bench`

Note: Open one more terminal and move to `frappe-bench` folder and run the upcoming commands

Username: `Administrator`

Password: `admin`


DB User: `root`

DB Password: `123`


But while running the below commands you can change the admin and Db password as your wish don't follow this one use some more secure password and take notes

`SITE_NAME` example --> `erpnext.com`, `example.com` this only example you can give any domain you have if you don't have domain you can create like this `erp.localhost` but you can't access through this domain `erp.localhost` but you can use the `IP Address` instead.
```
bench new-site <SITE_NAME> --mariadb-root-password 123 --admin-password admin --no-mariadb-socket
```


Tell the bech to use this site as a current site
```
bench use <SITE_NAME>
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
# STOP Production Mode
* [How to stop production setup?](https://discuss.frappe.io/t/how-to-stop-production-setup/106204)
```
sudo service nginx stop
sudo service supervisord stop
bench setup procfile
bench start
```
# Update the latest code 
No need to stop the server `git pull` the latest code and `migrate`
```
bench migrate
```
```
bench restart
```
