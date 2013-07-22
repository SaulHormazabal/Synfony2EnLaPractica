Creación de Bundles
===================

Los bundles son paquetes que mantienen el orden de nuestro proyecto, además nos permiten utilizarlos en posteriores desarrollos, ahorrándonos líneas de código. Así que crearemos 3 bundles de forma interactiva en la consola de Symfony2 ejecutando el siguiente comando:

	$ php app/console generate:bundle


Se nos irán haciendo preguntas, pero solo necesitamos completar dos cosas: "Bundle namespace" y "Configuration format".

Para "Configuration format" pondremos en los 3 casos "yml".

	$ Configuration format (yml, xml, php, or annotation) [annotation]: yml


El namespace de los tres bundles serán "Sahch/UserBundle", "Sahch/TipBundle" y "Sahch/TagBundle".

	Bundle namespace: Sahch/UserBundle
	Bundle namespace: Sahch/SahchTipBundle
	Bundle namespace: Sahch/TagBundle
