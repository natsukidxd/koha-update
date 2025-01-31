# UPDATE LATEST KOHA v24.05

sudo mysql -uroot -p[password] mysqldump --single-transaction -uroot -p[password] koha_library > koha_library.sql
sudo apt-get update
sudo apt-get upgrade
sudo apt install sudo apt-transport-https ca-certificates curl
sudo mkdir -p --mode=0755 /etc/apt/keyrings
sudo curl -fsSL https://debian.koha-community.org/koha/gpg.asc -o /etc/apt/keyrings/koha.asc
sudo apt-get update
echo 'deb [signed-by=/etc/apt/keyrings/koha.asc] https://debian.koha-community.org/koha 24.05 main' | sudo tee /etc/apt/sources.list.d/koha.list
sudo apt-get update
sudo apt-get install koha-common
sudo apt-get install gedit
sudo gedit /etc/koha/koha-sites.conf
sudo apt-get install mysql-server
sudo a2enmod rewrite
sudo a2enmod cgi
sudo service apache2 restart
sudo koha-create --create-db library
sudo gedit /etc/apache2/ports.conf
sudo service apache2 restart
sudo a2dissite 000-default
sudo a2enmod deflate
sudo a2ensite library
sudo service apache2 restart
sudo koha-passwd library

<install DBeaver>
USE mysql;
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '[password]';
FLUSH PRIVILEGES;
EXIT;
 
sudo mysql -uroot -p[password]
drop database koha_library;
create database koha_library;
quit;
sudo mysql -uroot -p[password] koha_library < koha_library.sql 
sudo service memcached restart
sudo koha-upgrade-schema library
sudo koha-rebuild-zebra -v -f library
