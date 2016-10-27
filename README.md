Simple Book Store: BackEnd
======================
- [Installation](#installation)
- [Develoment Tacks](#develoment-tacks)
	- [Run server](#run-server)
	- [Build](#build)
- [Design](#design)
- [Technology Stack](#technology-stack)
	- [Installing PHP on windows 10](installing-php-on-windows-10)
	- [Installing Composer (php package manager)](#installing-composer-php-package-manager)
	- [Configure virtual host](#Configure-virtual-host)
	- [Laravel PHP Framework 5.3](#Laravel-PHP-Framework-5.3)


Installation
------------
- Prerequisites (see _[Technology Stack](#technology-stack)_):
    * PHP with php.ini configurated
    * Composer
    * on Windows machines maybe requires [Visual Studio 2013 WD](https://www.visualstudio.com/downloads/download-visual-studio-vs#d-express-windows-desktop)
- Install:

	```bash
	git clone git@github.com:pablojavierjimenez/SimpleBookStore-BackEnd.git
	cd SimpleBookStore-BackEnd
	git checkout develop
	```

technology-stack
----------------
#### Installing PHP on windows 10
1. Download php for windows (10) : http://windows.php.net/download/
2. Create a folder ( C:\php )
  - rename file php.iniDevelopment to php.ini
  - Uncomment that comandas: (delete a semicolona **";"** at start of the line)
    - extension_dir = "ext"
    - extension=php_mbstring.dll
    - php_mysql.dll
    - php_mysqli.dll
3. on windows go to  _Control panel > System and security > System_ then to _Advance Sistem Settings_ and in advance tab, click on enviroment variables

	then open the comand line and test
	```bash
	php -v
	```
	if you need to see a reference check this [video tutorial](https://youtu.be/kuMTZowwjus?t=3m14s)

#### Installing Composer (php package manager)
1. From this site: [Download Composer](https://getcomposer.org/download/)
2. Download and run Composer-Setup.exe, and whend the instalation program request to you, put a root for php.exe, were you installed php eg: C:\php\php.exe

	then open the comand line and test
	```bash
	composer -version
	```
	**NOTE:** its just in case or for other proyect here is the command to start a proyect
	```bash
	composer create-project laravel/laravel nombre_del_proyecto --prefer-dist
	```

#### Configure virtual host

1. __Windows host configuration__
	
	Go to this windows folder _C:/Windows/System32/drivers/etc_ and open the __host__ file 
	and edit it putting the next code:
	```apache
	# localhost name resolution is handled within DNS itself.
	#	127.0.0.1       localhost
	#	::1             localhost

	127.0.0.1   localhost
	127.0.0.1	SimpleBookStore.dev
	```

2. __Apache configuration__

	* Go to _xampp/apache/conf/httpd.conf_ and see that vhost module is eneable
	```apache
	# Virtual hosts
	Include conf/extra/httpd-vhosts.conf
	```
	* then go to _xampp/apache/conf/extra/httpd-vhosts.conf_ and add this code to configurate your proyect
	```apache
		#
		## localhost *:80
		# SI EN ESTE ARCHIVO APPACHE NO ENCUENTRA NINGUNA RUTA 
		# POR DEFECTO LA RUTA A LA CARPETA HTDOCS SERA localhost
		# PERO EN EL CASO DE QUE AGREGUES OTRA RUTA ej: example.dev
		# ANTES DE AGREGAR ESA RUTA DEBES AGREGAR ESTA, DADO QUE SI NO LO HACES
		# APACHE DESACTIVARA LAS REFERENCIAS A localhost 
		# PARA ESTE O CUALQUIERA DE TUS OTROS PROYECTOS
		#
		<VirtualHost *:80>
		   DocumentRoot "E:/xampp/htdocs"
		   ServerName localhost
		</VirtualHost>

		#
		## SimpleBookStore.dev *:80
		# RUTA AGREGADA PARA LA APLICACION DE SIMPLE BOOK STORE
		# CON LARAVEL QUE SERVIRA COMO API
		#
		<VirtualHost *:80>
		   DocumentRoot "E:/xampp/htdocs/dev/SimpleBookStore-BackEnd"
		   ServerName SimpleBookStore.dev
		</VirtualHost>
	```
3. __.htacces configuration__

	Create a file __.htacces__ and put this code on it
	```apache
		# Webempresa.com
		# Redireccion de dominio principal a subdirectorio
		# Copiar y pegar y modificar según necesidades
		# Esta linea no quitarla
		RewriteEngine on
		# Cambiar sudominio.com por su nombre de dominio
		RewriteCond %{HTTP_HOST} ^(www.)?simplebookstore.dev$
		# Cambiar 'subdirectory' por el nombre del subdirectorio que quiere usar
		RewriteCond %{REQUEST_URI} !^/public/
		# No cambiar estas lineas.
		RewriteCond %{REQUEST_FILENAME} !-f
		RewriteCond %{REQUEST_FILENAME} !-d
		# Cambiar 'subdirectory' por el nombre del subdirectorio que quiere usar
		RewriteRule ^(.*)$ /public/$1
		# Cambiar sudominio.com por su nombre de dominio
		# Cambiar 'subdirectory' por el nombre del subdirectorio que quiere usar
		# followed by / then the main file for your site, index.php, index.html, etc.
		RewriteCond %{HTTP_HOST} ^(www.)?simplebookstore.dev$
		RewriteRule ^(/)?$ public/index.php [L]
	```
	

#### Laravel PHP Framework 5.3

[![Build Status](https://travis-ci.org/laravel/framework.svg)](https://travis-ci.org/laravel/framework)
[![Total Downloads](https://poser.pugx.org/laravel/framework/d/total.svg)](https://packagist.org/packages/laravel/framework)
[![Latest Stable Version](https://poser.pugx.org/laravel/framework/v/stable.svg)](https://packagist.org/packages/laravel/framework)
[![Latest Unstable Version](https://poser.pugx.org/laravel/framework/v/unstable.svg)](https://packagist.org/packages/laravel/framework)
[![License](https://poser.pugx.org/laravel/framework/license.svg)](https://packagist.org/packages/laravel/framework)

Documentation for the framework can be found on the [Laravel website](https://laravel.com/docs/5.3/).
