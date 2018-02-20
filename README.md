# docker
How to install Docker on Fedora 27

# Install docker Ubuntu

sudo apt-get update
sudo apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D
sudo apt-add-repository 'deb https://apt.dockerproject.org/repo ubuntu-xenial main'
sudo apt-get update
apt-cache policy docker-engine
sudo apt-get install -y docker-engine
sudo systemctl status docker

# Install docker on Fedora 27
sudo dnf -y install dnf-plugins-core
sudo dnf config-manager \
    --add-repo \
    https://download.docker.com/linux/fedora/docker-ce.repo
sudo systemctl status docker

# Config Docker
docker build . -t proyecto
docker run -itd -v /home/tudirectorio/proyecto:/var/www/sites/ -p 9080:80 -p 9022:22 -p 9200:9200 -p 9006:3306 -p 9000:9000 --privileged --name app proyecto
docker ps -a
docker exec -ti app /bin/bash

# Correr Docker
systemctl start docker
docker start app
docker exec -ti app /bin/bash

# Provisionar
./setup.sh

# Instalar Xdebug 
docker exec -ti app /bin/bash
pecl install Xdebug
cd /etc/php.d
touch 20-xdebug.ini
nano 20-xdebug.ini

# Agregar configuración al archivo 20-xdebug.ini
[xdebug]
zend_extension=/usr/lib64/php/modules/xdebug.so
xdebug.remote_enable = 1
xdebug.remote_connect_back = 1
xdebug.collect_params   = 4
xdebug.collect_vars = on
xdebug.dump_globals = on
xdebug.dump.SERVER = REQUEST_URI
xdebug.show_local_vars = on
xdebug.cli_color = 1
xdebug.remote_port = 9002
