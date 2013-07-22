Creación del proyecto
=====================

Ahora creamos el proyecto, donde "microtip" se refiere al nombre que le daremos, y los numero finales a la versión de Symfony2 que ocuparemos. 

El proyecto debe estar en  una carpeta del servidor, por defecto es /var/www, aunque yo recomiendo habilitar carpetas public_html en el home de los usuarios y servir hay el proyecto y adicionalmente crear un virtualhost.

	$ mkdir -p ~/public_html
	$ cd ~/public_html
	$ composer.phar create-project symfony/framework-standard-edition microtip/ 2.3.1
