Sistema de Usuario con FosUserBundle
====================================

Este es un bundle generado por la comunidad “Friends Of Symfony” (FOS) el cual nos brinda la mayoría de las funcionalidades deseadas en un sistema de usuarios como el registro, verificación de correo, inicio de sesión, edición de perfil, cambio de contraseña, etc.

Primero debemos habilitar la traducción en el archivo “config.yml” ubicado en “app/config/” descomentando la línea “translator”, borrando el signo “#” del comienzo, quedando de la siguiente forma.

    framework:
        translator: ~


Ahora es necesario cambiar el idioma a español en el archivo “parameters.yml” ubicado en “app/config/” de la siguiente forma.

        locale:            es


Agregamos FosUserBundle al archivo “composer.json”.

    {
        "require": {
            "friendsofsymfony/user-bundle": "*"
        }
    }


Ahora lo descargamos usando “composer.phar” con la siguiente línea de comando:

    composer.phar update


Lo siguiente es agregar el nuevo bundle al kernel en el archivo “AppKernel.php” en “app/”.

    <?php
    
    public function registerBundles() {
        $bundles = array(
            // ...
            new FOS\UserBundle\FOSUserBundle(),
        );
    }


Las entidades son la abstracción de las tablas de la base de datos, las cuales se representan como una clases php, en las cuales realizaremos las especificaciones técnicas a través de comentarios.

A continuación crearemos una carpeta llamada “Entity” en “src/Sahch/UserBundle”.

    mkdir src/Sahch/UserBundle/Entity


Y en esta carpeta creamos el archivo “User.php” con el siguiente contenido:
    
    <?php
    
    namespace Sahch\UserBundle\Entity;
    
    use FOS\UserBundle\Entity\User as BaseUser;
    use Doctrine\ORM\Mapping as ORM;
    
    /**
     * @ORM\Entity
     * @ORM\Table(name="fos_user")
     */
    class User extends BaseUser {
    
        /**
         * @ORM\Id
         * @ORM\Column(type="integer")
         * @ORM\GeneratedValue(strategy="AUTO")
         */
        protected $id;
    
        public function __construct() {
            parent::__construct();
        }
    }

Cambiamos el contenido del archivo “security.yml” en “app/config/” por este:

    security:
        encoders:
            FOS\UserBundle\Model\UserInterface: sha512

        role_hierarchy:
            ROLE_ADMIN:       ROLE_USER
            ROLE_SUPER_ADMIN: ROLE_ADMIN

        providers:
            fos_userbundle:
                id: fos_user.user_provider.username_email

        firewalls:
            main:
                pattern: ^/
                form_login:
                    provider: fos_userbundle
                    csrf_provider: form.csrf_provider
                logout:       true
                anonymous:    true

        access_control:
            - { path: ^/login$, role: IS_AUTHENTICATED_ANONYMOUSLY }
            - { path: ^/register, role: IS_AUTHENTICATED_ANONYMOUSLY }
            - { path: ^/resetting, role: IS_AUTHENTICATED_ANONYMOUSLY }
            - { path: ^/admin/, role: ROLE_ADMIN }


Incorporamos las especificaciones de configuración de FosuserBundle al final del archivo “config.yml” en “app/config/”.

    fos_user:
        db_driver: orm
        firewall_name: main
        user_class: Sahch\UserBundle\Entity\User

Y para terminar con el sistema de usuario agregamos las rutas al archivo“routing.yml” en “app/config/”.

    fos_user_security:
        resource: "@FOSUserBundle/Resources/config/routing/security.xml"

    fos_user_profile:
        resource: "@FOSUserBundle/Resources/config/routing/profile.xml"
        prefix: /profile

    fos_user_register:
        resource: "@FOSUserBundle/Resources/config/routing/registration.xml"
        prefix: /register

    fos_user_resetting:
        resource: "@FOSUserBundle/Resources/config/routing/resetting.xml"
        prefix: /resetting

    fos_user_change_password:
        resource: "@FOSUserBundle/Resources/config/routing/change_password.xml"
        prefix: /profile


Ahora solo queda generar la tabla en la base de datos a partir de la entidad de usuario con la siguiente línea de comandos:

    $ php app/console doctrine:schema:update --force


Ahora comprobaremos que todo esté funcionando bien, asi que primero limpiamos la cache para los entornos de desarrollo y producción y daremos los permisos correspondientes.

    $ php app/console cache:clear
    $ php app/console cache:clear --env=prod
    $ chmod 777 -R app/cache

Ahora podemos ingresar al sistema de usuarios en las siguientes direcciones:


| URL                        | Descripción                             |
| :-------------------------:| ---------------------------------------:|
| Inicio de sesión           | http://microtip/login                   |
| Formulario de registro     | http://microtip/register/               |
| Perfil de usuario          | http://microtip/profle                  |
| Editar perfil              | http://microtip/profile/edit            |
| Cambiar contraseña         | http://microtip/profile/change-password |
| Recuperación de contraseña | http://microtip/resetting/request       |
| Cerrar sesión              | http://microtip/logout                  |
