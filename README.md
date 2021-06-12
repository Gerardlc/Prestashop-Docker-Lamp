# Comandos para montar el prestashop

### Pasos a seguir:
- Clonar el repositorio
- Descargar prestashop y descomprimir en la carpeta www
- Levantar los contenedores con `docker-compose up -d`
- Instalar prestashop

### Comandos terminal para descargar prestashop y descomprimirlo:

Nos situamos en la raíz del repositorio y ejecutamos los siguientes comandos uno por uno:

- `wget https://download.prestashop.com/download/releases/prestashop_1.7.7.4.zip`
- `unzip prestashop_1.7.7.4.zip -d www`
- `rm prestashop_1.7.7.4.zip`

*Si no dispones de wget en tu pc puedes descargarlo igualmente desde el navegador y copiar el zip a la raíz del repositorio, desde: [https://www.prestashop.com/es/versiones](https://www.prestashop.com/es/versiones) y despues hacer el unzip con `unzip prestashop_1.7.7.4.zip -d www` para descomprimirlo y dejarlo en la carpeta www que es la que servirá al container.

### Instalar prestashop

Entrar a la url : [http://localhost:80](http://localhost:80) e comenzar la instalación de Prestashop

*Si actualmente ya estás usando los puertos 80, 8080 o 13306 tendrás que o bien cerrar los procesos que los estén usando o cambiar los puertos en el archivo `docker-compose.yml`

#### Accesos de base de datos para la instalación

- servidor: db
- base de datos: prestashop_dev
- usuario: root
- contraseña: root
- prefijo: el que mas te guste, pero cambialo 😀

Los accesos se pueden cambiar en el archivo `docker-compose.yml` al igual que los puertos de los contenedores


### Comandos útiles

#### Básicos:

- run container : `docker-compose up -d`
- stop container : `docker-compose down`

#### Otros:

- rebuild container : `docker-compose up -d --build` 

- enter into web container : `docker exec -it prestaweb bash` 

- install npm dependencies : `docker exec -it prestaweb npm i --prefix YOUR/FOLDER/PATH` 

- build assets with npm : `docker exec -it prestaweb run build --prefix YOUR/FOLDER/PATH` 

- watch assets with npm : `docker exec -it prestaweb run build --prefix YOUR/FOLDER/PATH` 

- database dump : `docker exec -it prestadb mysqldump -u root --password=root YOUR_DB_NAME --compact > YOUR_BACKUP.sql` 

- restore backup : `cat yourbackup.sql | docker exec -i prestadb /usr/bin/mysql -u root --password=root prestashop_dev` 


### Información sobre los contenedores y dependencias

- Php 7.3
- Mysql 5.7
- Phpmyadmin : latest
- NodeJs : 10.x
