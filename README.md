 i used the apt install wordpress
```
sudo apt install wordpress
```
this command ran succesfully
also, the following packages were installed automatically

*** apache2
apache2-bin
apache2-data
apache2-utils
default-mysql-client
fontconfig-config
fonts-dejavu-core
javascript-common
libao-common
libao4
libapache2-mod-php
libapache2-mod-php7.4
libapr1
libaprutil1
libaprutil1-dbd-sqlite3
libaprutil1-ldap
libflac8
libfontconfig1
libgd3
libjansson4
libjbig0
libjpeg-turbo8
libjpeg8
libjs-cropper
libjs-jquery
libjs-prototype
libjs-scriptaculous
libjs-underscore
liblua5.2-0
libspeex1
libtiff5
libvorbisenc2
libwebp6
libxpm4
mysql-client-8.0
mysql-client-core-8.0
mysql-common
php-common
php-gd
php-getid3
php-mysql
php7.4-cli
php7.4-common
php7.4-gd
php7.4-json
php7.4-mysql
php7.4-opcache
php7.4-readline
ssl-cert
vorbis-tools
wordpress-l10n
 wordpress-theme-twentynineteen ***

# i wasnt sure of the location of the files i installed
# i used the dpkg-query commend to locate the files
```
sudo dpkg-query -L wordpress
```
# the files were located at /usr/share/wordpress
# i look for the apache config file
# the file was located at /etc/apache2/sites-available/000-default.conf
# i created a copy of the file wordpress.conf
```
cd /etc/apache2/sites-available
cp 000-default.conf wordpress.conf
vim wordpress.conf
```
# this is the currnt wordpress.conf log file
<VirtualHost *:80>
	ServerAdmin webmaster@localhost
	DocumentRoot /usr/share/wordpress

	ErrorLog ${APACHE_LOG_DIR}/error.log
	CustomLog ${APACHE_LOG_DIR}/access.log combined

</VirtualHost>

# vim: syntax=apache ts=4 sw=4 sts=4 sr noet

# i removed the old soft link 
```
rm 000-dafault.conf
```
# i created a new sodt link for the new wordpress.conf file
```
ln -sf ../sites-available/wordpress.conf 000-default.conf
```
# i check the syntax for apache2
```
apache2 -t
```
# the resulte was a syntax error message
# i resterted the apache server
```
systemctl restart apache
```
# then i check the status of the apache server 
```
systemctl status apache
```
# the commend showed that the apache server was active
# i opend the browser and nevigated to the web page
# the web page showed an error message
```
Neither /etc/wordpress/config-192.168.1.6.php nor /etc/wordpress/config-168.1.6.php could be found. Ensure one of them exists, is readable by the webserver and contains the right password/username.
```
