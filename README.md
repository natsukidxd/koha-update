# UPDATE LATEST KOHA v24.05

(in old koha server) sudo mysqldump --single-transaction -uroot -p koha_library > koha_library.sql </br>
(in new koha server) sudo apt-get update </br>
sudo apt-get upgrade </br>
sudo apt install sudo apt-transport-https ca-certificates curl </br>
sudo mkdir -p --mode=0755 /etc/apt/keyrings </br>
sudo curl -fsSL https://debian.koha-community.org/koha/gpg.asc -o /etc/apt/keyrings/koha.asc </br>
sudo apt-get update </br>
echo 'deb [signed-by=/etc/apt/keyrings/koha.asc] https://debian.koha-community.org/koha 24.05 main' | sudo tee /etc/apt/sources.list.d/koha.list </br>
sudo apt-get update </br>
sudo apt-get install koha-common </br>
sudo apt-get install gedit </br>
sudo gedit /etc/koha/koha-sites.conf </br>
sudo apt-get install mysql-server </br>
sudo a2enmod rewrite </br>
sudo a2enmod cgi </br>
sudo service apache2 restart </br>
sudo koha-create --create-db library </br>
sudo gedit /etc/apache2/ports.conf </br>
sudo service apache2 restart </br>
sudo a2dissite 000-default </br>
sudo a2enmod deflate </br>
sudo a2ensite library </br>
sudo service apache2 restart </br>
sudo koha-passwd library </br>
 </br>
<install DBeaver> </br>
USE mysql; </br>
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '[password]'; (for mysql db)</br>
ALTER USER 'root'@'localhost' IDENTIFIED BY 'your_new_password'; for(mariadb)</br>
FLUSH PRIVILEGES; </br>
EXIT; </br>
  </br>
sudo mysql -uroot -p </br>
drop database koha_library; </br>
create database koha_library; </br>
quit; </br>
sudo mysql -uroot -p koha_library < koha_library.sql  </br>
sed -i 's/utf8mb4_0900_ai_ci/utf8mb4_unicode_ci/g' [sql location]</br>
sudo service memcached restart </br>
sudo koha-upgrade-schema library </br>
sudo koha-rebuild-zebra -v -f library </br>
