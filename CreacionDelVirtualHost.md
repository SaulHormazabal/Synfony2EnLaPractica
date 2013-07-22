Creación del VirtualHost
========================

Primero debemos cambiarnos a root.

	$ sudo -s


Agregamos el nombre que le damermos al VirtualHost editando el archivo hosts.

	$ nano /etc/hosts


En este archivo debemos incluir el nombre que le daremos a nuestro VirtualHost bajo la linea 127.0.0.1 localhost. Nosotros ocuparemos “microtip” , pero puede ser el que tu quieras.

	$ 127.0.0.1       microtip


Ahora necesitamos hacer las configuraciones, cambiandonos de directorio, creamos el archivo y agregar el nombre del Virtual Host y la ruta de nuestro proyecto.

	$ cd /etc/apache2/site-available
	$ nano microtip


Nuestro archivo debiese quedar así:

	<VirtualHost *:80>
	        ServerAdmin saul.hormazabal@gmail.com
	        ServerName microtip
	        DocumentRoot /home/sahch/public_html/microtip
	        <Directory /home/sahch/public_html/microtip/>
	                Options Indexes FollowSymLinks MultiViews
	                AllowOverride All
	           	    Order allow,deny
	                allow from all
	        </Directory>
	        ErrorLog ${APACHE_LOG_DIR}/error.log
	        LogLevel warn
	        CustomLog ${APACHE_LOG_DIR}/access.log combined
	</VirtualHost>


Ahora solo queda habilitarlo, reiniciar apache y volver a nuestro usuario.

	$ a2ensite microtip
	$ service apache2 reload
	$ exit
