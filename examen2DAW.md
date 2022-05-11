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
Descomprimo el paquete
```
sudo tar xf mediawiki-1.37.2.tar.gz -C /var/www/html/
```
 Creo un enlace simbólico sin números de versión
 ```
 sudo ln -s /var/www/html/mediawiki-1.37.3/ /var/www/html/wiki
```
Conecto el servicio de base de datos
```
sudo mysql -u root -p
```
Creo la base de datos
```
create database my_wiki character set utf8mb4 collate utf8mb4_unicode_ci;
```
Creo el usuario
```
create user mediawiki@localhost identified by 'mediawiki';
```
Concedo permisos al usuario sobre la base de datos
```
grant all privileges on my_wiki.* to mediawiki@localhost;
```
Cierro sesión
```
exit
```
Instalo las extensiones de php
```
sudo apt install -y php-apcu php-gd php-imagick php-intl php-mbstring php-xml
```
Recargo apache
```
sudo systemctl reload apache2
```
Accedo al instalador desde el navegador
```
http://localhost:8080/mediawiki-1.37.2/
```


Usuario: user
Contraseña: alumno2022
Una vez finalizada la instalación descargo el archivo de configuración LocalSettings.php y lo muevo a su ubicación definitiva
```
sudo mv LocalSettings.php /var/www/html/mediawiki-1.37.2/
```
Entro en la wiki para comprobar que funciona y accedo con el usuario creado

