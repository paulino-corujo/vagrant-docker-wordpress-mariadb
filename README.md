# vagrant-docker-wordpress-mariadb
Complete LAMP development environment for WordPress with Docker and (optionally) Vagrant

# Vagrant
Launch with ```vagrant up ```. It will create an ```ubuntu/trusty64``` environment with docker and docker-compose. The docker-compose provisioner will pull the images described in the section below.

If a public key ```$HOME/.ssh/id_rsa.pub``` is present it will be added to the ```authorized_keys``` in the guest machine.

# Docker Compose

Pulls the official WordPress, MariaDB and ```corbinu/docker-phpmyadmin``` images.

```/var/www/html``` folder is mapped to ```./src``` using a docker volume

# URLs

WordPress -> http://10.5.10.5

phpMyAdmin -> http://10.5.10.5:8080
