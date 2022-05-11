## Web 1: wiki empresarial
Lanzo vagrant con la siguiente configuración
```
Vagrant.configure("2") do |config|
  config.vm.box = "bento/ubuntu-20.04"

  config.vm.network :forwarded_port, guest: 80, host: 8000
end
```
Levanto y actualizo el sistema
```
vagrant up
vagrant ssh
sudo apt update
```
Instalo el servidor de base de datos mariadb
```
sudo apt install mariadb-server
```
Instalo apache2 y el módulo que permite que apache2 interprete PHP
```
sudo apt install apache2 libapache2-mod-php php php-mysql
```
Instalo el cliente de base de datos mariadb 
```
sudo apt install mariadb-client
```
Descargo el paquete con la herramienta wget
```
wget https://releases.wikimedia.org/mediawiki/1.37/mediawiki-1.37.2.tar.gz
```

