# Zabbix-Install-Centos7.9
Zabbix Install on Centos 7.9

url:https://www.youtube.com/watch?v=JoaBN7etqfo

Check the version:
# cat /etc/redhat-release 


Disable SELinux
# vi /etc/sysconfig/selinux
Change “SELINUX=enforcing” to “SELINUX=disabled”
# getenforce (command to check the status)

(Download the repo of the Zabbix)
# rpm -Uvh https://repo.zabbix.com/zabbix/5.0/rhel/7/x86_64/zabbix-release-5.0-1.el7.noarch.rpm
           https://repo.zabbix.com/zabbix/5.0/rhel/8/x86_64/zabbix-release-5.0-1.el8.noarch.rpm
#  yum clean all

Install zabbix server, agent and zabbix-get for log files
# yum install zabbix-get zabbix-agent zabbix-server-mysql -y

Install Zabbix Front end
Edit file and enable zabbix-frontend repository. 
# vi /etc/yum.repos.d/zabbix.repo
[zabbix-frontend]
enabled=1

Enable Red Hat Software Collections
# yum install centos-release-scl -y

Install Zabbix frontend packages:
# yum install zabbix-web-mysql-scl zabbix-apache-conf-scl -y

Install MariaDB server
# yum install mariadb-server -y

Start MariaDB
systemctl start mariadb
systemctl enable mariadb


mysql
create database zabbix_db character set utf8 collate utf8_bin;
grant all privileges on zabbix_db.* to zabbix@'localhost' identified by 'passw0rd';
flush privileges;

Database: zabbix_db
Username: zabbix
Password: passw0rd

Extract Schema file:
# cd  /usr/share/doc/zabbix-server-mysql-5.0.33/
# zcat create.sql.gz | mysql zabbix_db

Check the database
# mysql
# use zabbix_db;
# show tables;

Change the configuration file of Zabbix-server
# vim /etc/zabbix/zabbix_server.conf

Change these parameters on Zabbix_server.conf file.
DBName=zabbix_db
DBUser=zabbix
DBPassword=passw0rd

Start ZABBIX-SERVER
# systemctl start zabbix-server
systemctl enable zabbix-server

Check the Zabbix server is running or not by checking the log file
# less /var/log/zabbix/zabbix_server.log

Edit file and uncomment and set the right timezone for you. 
# vim /etc/opt/rh/rh-php72/php-fpm.d/zabbix.conf
; php_value[date.timezone] = Asia/Dhaka 

Start Zabbix server and agent processes:
# systemctl restart zabbix-server zabbix-agent httpd rh-php72-php-fpm mariadb
# systemctl enable zabbix-server zabbix-agent httpd rh-php72-php-fpm mariadb

Modify the firewall
firewall-cmd --add-service={http,https} --permanent
firewall-cmd --add-port={10051/tcp,10050/tcp} --permanent
firewall-cmd --reload

Go to Browser
Follow the instruction and use the database password, click next and login with default username and password.
Username: Admin
Password: zabbix

for first time initizing
http://192.168.1.10/zabbix

sudo zcat /usr/share/doc/zabbix-server-mysql*/create.sql.gz | mysql -uzabbix -p zabbix_db

cachesize=2G
hisroeycache=512M
valuesize=400M





Client Add:
====================
url:https://www.youtube.com/watch?v=NKTmN8s7IyU&list=PL0b-PCRYfcTSkkuK81do8CXwrTluU-dhS&index=19&t=2s
192.168.1.10
snmp:g0lden

IP:192.168.1.10
Zabbix credentials
user:Admin
PWS:xxxxxx



Telegram ADD:
====================
url:https://www.youtube.com/watch?v=qCjt3kj8rMk&list=PL0b-PCRYfcTSkkuK81do8CXwrTluU-dhS&index=20



https://git.zabbix.com/projects/ZBX/repos/zabbix/browse/templates/media/telegram

1. Register bot: send "/newbot" to @BotFather and follow instructions
2. Copy and paste the obtained token into the "Token" field above
3. If you want to send personal notifications, you need to get chat id of the user you want to send messages to:
    3.1. Send "/getid" to "@myidbot" in Telegram messenger
    3.2. Copy returned chat id and save it in the "Telegram Webhook" media for the user
    3.3. Ask the user to send "/start" to your bot (Telegram bot won't send anything to the user without it)
4. If you want to send group notifications, you need to get group id of the group you want to send messages to:
    4.1. Add "@myidbot" to your group
    4.2. Send "/getgroupid@myidbot" in your group
    4.3. Copy returned group id save it in the "Telegram Webhook" media for the user you created for  group notifications
    4.4. Send "/start@your_bot_name_here" in your group (Telegram bot won't send anything to the group without it)


Token:6102204790:AAH-2mare2adfascdacd-txRlfX_95w


