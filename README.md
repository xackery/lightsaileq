# lightsaileq
EQ Lightsail Config

bzcat file.sql.bz2 | mysql -u root -p peq
mysqldump -u root -p peq --lock-tables=false | bzip2 > file.sql.bz2

ubuntu 18.04
```
sudo apt update
sudo apt install build-essential \
    gcc-5 g++-5 libtool cmake curl debconf-utils \
    git git-core libio-stringy-perl liblua5.1 \
    liblua5.1-dev libluabind-dev libmysql++ \
    libperl-dev libperl5i-perl libjson-perl libsodium-dev \
    libmysqlclient-dev libssl-dev lua5.1 \
    minizip make mariadb-client locales \
    nano open-vm-tools unzip uuid-dev iputils-ping \
    zlibc wget \
    gdb valgrind 
sudo apt install mysql-server
wget http://ftp.us.debian.org/debian/pool/main/libs/libsodium/libsodium-dev_1.0.11-2_amd64.deb -O /tmp/libsodium-dev.deb
wget http://ftp.us.debian.org/debian/pool/main/libs/libsodium/libsodium18_1.0.11-2_amd64.deb -O /tmp/libsodium18.deb
sudo dpkg -i /tmp/libsodium*.deb
rm -f /tmp/libsodium-dev.deb
rm -f /tmp/libsodium18.deb

# add swap
sudo fallocate -l 1G /swapfile 
sudo chmod 600 /swapfile 
sudo mkswap /swapfile 
sudo swapon /swapfile 
sudo cp /etc/fstab /etc/fstab.bak 
echo '/swapfile none swap sw 0 0' | sudo tee -a /etc/fstab

sudo mysql_secure_installation
sudo hostname <server>
cd ~/
mkdir eq
cd eq
ssh-keygen -f ~/.ssh/githubkey
cat ~/.ssh/githubkey.pub
# log into github, Top right avatar, settings, SSH and PGP keys, new SSH key, # paste in ssh-rsa lines in.
nano ~/.ssh/config
# into config, do next 3 lines:
Host github.com
        User git
        IdentityFile ~/.ssh/githubkey
mkdir -p ~/eq/server
wget https://raw.githubusercontent.com/Akkadius/eqemu-install-v2/master/eqemu_config.json
nano eqemu_config.json
# edit to your heart's content
wget https://raw.githubusercontent.com/EQEmu/Server/master/utils/scripts/eqemu_server.pl
perl eqemu_server.pl opcodes
perl eqemu_server.pl patches
sudo nano /etc/mysql/conf.d/mysql.cnf
```
# on bottom, add the lines:
```
[mysqld]

sql_mode=NO_ENGINE_SUBSTITUTION
```
now restart mysql
```
sudo service mysql restart
## TODO: source your database
```
(for non-rebuildeq)
```
# if you didn't source your database, you can use:
perl eqemu_server.pl source_peq_db
# above as an alternative
perl eqemu_server.pl quests
perl eqemu_server.pl lua_modules
perl eqemu_server.pl plugins
perl eqemu_server.pl maps
perl eqemu_server.pl check_db_updates
```


(for rebuildeq)
```
sudo apt install python-software-properties
sudo add-apt-repository ppa:ondrej/php
sudo apt update
sudo apt install -y php5.6 php5.6-mbstring hugo
# next, clone repo
cd ~/eq/server/
# git clone git@github.com:xackery/rebuildeq.git src #commented out, copy binaries built elsewhere, faster
git clone git@github.com:rebuildeq/plugins.git
git clone git@github.com:rebuildeq/quests.git
git clone git@github.com:rebuildeq/lua_modules.git
git clone git@github.com:rebuildeq/maps.git
sudo rm -rf /var/www
sudo mkdir -p /var/www
cd /var/www
sudo chown -R ubuntu /var/www
git clone git@github.com:rebuildeq/web.git .
chmod 777 /var/www/application/logs
chmod 777 /var/www/application/cache
sudo nano /etc/apache2/apache2.conf
# Search for <Directory /var/www/>, you'll see an entry AllowOverride None, change it to AllowOverride All
sudo a2enmod rewrite
sudo service apache2 restart
cd /var/www/hugo
hugo
cp /var/www/application/config/database.txt /var/www/application/config/database.php
nano /var/www/application/config/database.php
# change any password '' fields to your mysql password
unlink /var/www/html/changelog
ln -s /var/www/hugo/public /var/www/html/changelog

# in database, variables table, update site to your test's url e.g. http://test.rebuildeq.com
```
