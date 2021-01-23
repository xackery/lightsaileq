# lightsaileq
EQ Lightsail Config

ubuntu 18.04
```
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
```
(for rebuildeq)
```
sudo apt install python-software-properties
sudo add-apt-repository ppa:ondrej/php
sudo apt update
sudo apt install -y php5.6
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
        IdentityFile ~/.ssh/test.rebuildeq.com
# next, clone repo
git clone git@github.com:xackery/rebuildeq.git src
git clone git@github.com:rebuildeq/plugins.git
git clone git@github.com:rebuildeq/quests.git
git clone git@github.com:rebuildeq/lua_modules.git
git clone git@github.com:rebuildeq/maps.git
```
for any EQ
```
# or make a server bin folder, e.g.
mkdir -p ~/eq/server
wget https://raw.githubusercontent.com/Akkadius/eqemu-install-v2/master/eqemu_config.json
nano eqemu_config.json
# edit to your heart's content
wget https://raw.githubusercontent.com/EQEmu/Server/master/utils/scripts/eqemu_server.pl

## from your local PC, copy built binaries
scp ~/src/bin/zone target:~/eq/server/
## and source your database!! (No instruction)

perl eqemu_server.pl opcodes
perl eqemu_server.pl patches

```
