# lightsaileq
EQ Lightsail Config

ubuntu 18.04

sudo apt install build-essential \
    gcc-5 g++-5 libtool cmake curl debconf-utils \
    git git-core libio-stringy-perl liblua5.1 \
    liblua5.1-dev libluabind-dev libmysql++ \
    libperl-dev libperl5i-perl libjson-perl libsodium-dev \
    libmysqlclient-dev libssl-dev lua5.1 \
    minizip make mariadb-client locales \
    nano open-vm-tools unzip uuid-dev iputils-ping \
    zlibc wget \
    gdb valgrind mysql-server
sudo mysql_secure_installation
sudo hostname <server>
sudo apt install python-software-properties
sudo add-apt-repository ppa:ondrej/php
sudo apt update
sudo apt install -y php5.6
