# Instalació ownCloud

## Instal·lar la versió 7.4 de PHP a Ubuntu 24.04

Instalarem els requisits previs de PPA:
```bash
sudo apt install software-properties-common -y
```

Instalarem les eines necessàries
```bash
LC_ALL=C.UTF-8 sudo add-apt-repository ppa:ondrej/php -y
```

Actualitzarem ara els repositoris:
```bash
sudo apt update
```

Instalarem les llibreries de PHP de la versió 7.4
```bash
sudo apt install php7.4 -y
```
```bash
sudo apt install -y php libapache2-mod-php7.4
```
```bash
sudo apt install -y php7.4-fpm php7.4-common php7.4-mbstring php7.4-xmlrpc php7.4-soap php7.4-gd php7.4-xml php7.4-intl php7.4-mysql php7.4-cli php7.4-ldap php7.4-zip php7.4-curl
```

Seleccionem la versió de PHP que voleu:
```bash
sudo update-alternatives --config php
```

Activarem els mòduls d'apache2 necessaris:
```bash
sudo a2enmod proxy_fcgi setenvif
```
```bash
sudo a2enconf php7.4-fpm
```

Reiniciarem l'apache2:
```bash
sudo service apache2 restart
```


## Instal·lació d'apache2 i mysql
Actualització de la màquina.
```bash
sudo apt update
```
```bash
sudo apt upgrade
```

Instal·lació del servidor web
```bash
sudo apt install -y apache2
```

Instal·lació del servidor de bases de dades
```bash
sudo apt install -y mysql-server
```

Instal·lació d'algunes llibreries de php
```bash
sudo apt install -y php libapache2-mod-php
```
```bash
sudo apt install -y php-fpm php-common php-mbstring php-xmlrpc php-soap php-gd php-xml php-intl php-mysql php-cli php-ldap php-zip php-curl
```

Reiniciem el servidor apache2
```bash
sudo systemctl restart apache2
```

## Configuració de MySQL

Des de la terminal hem d'executar la següent comanda:
```bash
sudo mysql
```

Un cop dins la consola de MySQL executem les comandes per a crear la base de dades.
```bash
CREATE DATABASE bbdd;
```

Per a la creació de l'usuari hem de tenir en compte que s'haurà d'identificar la IP 
```bash
CREATE USER 'usuario'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
```

Donem privilegis a l'usuari:
```bash
GRANT ALL ON bbdd.* to 'usuario'@'localhost';
```

Sortim de la base de dades
```bash
exit
```

Des d'un terminal amb un usuari sense privilegis hem de ser capaços de connectar introduïnt la nostra contrassenya.
```bash
mysql -u usuario -p
```

Tornarem a sortir
```bash
exit
```


## Descarreguem els fitxers de l'aplicació web

Anem al directori /var/www/html i descomprimim allà els fitxers de l'aplicació web, heu de substituir app-web.zip per el nom del vostre fitxer que heu descarregat
```bash
sudo cp ~/Baixades/app-web.zip /var/www/html
```

Aneu al directori /var/www/html
```bash
cd /var/www/html
```
Descomprimiu el fitxer que heu baixat
```bash
sudo unzip app-web.zip
```
Copieu els fitxers a la carpeta /var/www/html, modifiqueu app-web pel nom del directori on s'ha descomprimit el vostre arxiu.
```bash
sudo cp -R app-web/. /var/www/html
```
Eliminem la carpeta creada quan hem fet l'unzip
```bash
sudo rm -rf app-web/
```


## Eliminem el fitxer index.html de l'apache2
```bash
sudo rm -rf /var/www/html/index.html
```


## Aplicació de permisos a les nostres aplicacions web

Un cop descomprimits els fitxers de l'aplicació web al directori /var/www/html, apliquem els següents permisos al directori /var/www/html
```bash
cd /var/www/html
```
```bash
sudo chmod -R 775 .
```
```bash
sudo chown -R usuario:www-data .
```
<img src="Captura de pantalla 2024-11-07 202013.png">

## Accedim al navegador per veure que tot funciona

Poseu la direcció http://localhost al navegador web i configureu la cloud.

Si tot ha anat bé i heu seguit el manual us apareixerà l'instal·lador de l'aplicació web que heu baixat i us demanarà crear un usuari admin i la informació de la base de dades.

La informació que heu de posar (si no heu modificat la informació del manual) és la següent:

usuari: usuario
contrasenya: password
base de dades: bbdd
domini: localhost

En el seguent enllaç trobaras la configucació d'ownCloud
[Configuració ownCloud](https://github.com/JonEL1010/Inicial/blob/main/messi.md)












