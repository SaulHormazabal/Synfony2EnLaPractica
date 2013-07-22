Configuración de Symfony
========================

Ya estamos por terminar. Modificamos el propietario de los archivos y asignamos permisos a las carpetas "cache" y "logs".

	$ cd ~/public_html/microtip
	$ chown -R TU-USUARIO:www-data  *
	$ chmod 777 -R app/cache app/logs


Ahora abrimos nuestro navegador favorito y escribimos el nombre de nuestro Virtual Host y le agregamos al final "/config.php".

	http://microtip/config.php


Si está todo bien, podremos continuar con la configuración completando el formulario de la Base de Datos.

Ya con los datos listos de la Base de Datos generamos una clave secreta .

Y listo, se genera el archivo de configuración "parameters.yml", si hemos dado los permisos adecuados se escribirá automáticamente, si no, nos alertara de esto, pero podemos copiar el texto y editar nosotros mismos el archivo.

Ahora podemos acceder al entorno de desarrollo, accesible solo desde local poniendo "app_dev.php".

	http://microtip/app_dev.php
