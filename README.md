# Cordero_Miguel_RecISO

Primero tenemos que crear nuestras vpc donde vamos a albergar nuestras dos subredes la subred 1 donde estará el Balanceador junto a nuestros servidores apache y en la segunda subred donde se almacenará el servidor mysql.

![](Fotos/1.png)
![](Fotos/2.png)
![](Fotos/3.png)

Editamos reglas de entrada

![](Fotos/4.png)

Editamos las reglas de salida

![](Fotos/5.png)

Creamos las Instancias 
Las instancias que he usado son debian 

![](Fotos/6.png)
![](Fotos/7.png)

A continuación vamos a asociar una ip estática al balanceador para poder conectarnos y tener acceso a internet.

![](Fotos/8.png)

Conectamos la gateway antes creada a internet.

![](Fotos/9.png)

Luego nos vamos a asociar una dirección ip elástica para tener accesoa internet desde el balanceador.

![](Fotos/10.png)

Aquí podemos ver que nos la ha asociado al balanceador

![](Fotos/11.png)

Se me olvidaba decir que tenemos que poner una puerta de enlace a internet para poder tener internet en la otras máquina mientras las configuramos y descargamos los archivos necesarios.

![](Fotos/12.png)

-Configuración del balanceador

Copiamos el contenido del archivo default por si liamos y le ponemos un nombre para saber cual es.
![](Fotos/13.png)

A continuación dentro del balanceador copiamos lo siguiente
![](Fotos/14.png)

Luego de copiar lo anterior habilitamos el sitio web con a2ensite y le damos los permisos

Nos vamos a nuestro explorador y  ponemos la ip del balanceador

![](Fotos/15.png)
![](Fotos/16.png)
![](Fotos/17.png)

Pero como queremos que nos muestre la página con un certificado vamos a instalar certbot y configurar un nombre de dominio.

![](Fotos/18.png)
![](Fotos/19.png)

Comprobamos que el certificado está activo y asociado.

![](Fotos/20.png)

Configuración del servidor de apache 1

sudo apt update
sudo apt install -y apache2
sudo apt install php libapache2-mod-php php-mysql

Volvemos a copiar el archivo por si la volvemos a liar

![](Fotos/21.png)

En documentroot la ruta donde tiene que buscar el index.php.

![](Fotos/22.png)

Activamos el sitio que acabamos de configurar

![](Fotos/23.png)

Copiamos el repositorio git dónde está la aplicación que queremos implementar en la página web.

![](Fotos/24.png)
![](Fotos/25.png)

Luego vamos al archivo config en el apache1

![](Fotos/26.png)

Le tenemos que dar permisos al la carpeta apache1

![](Fotos/27.png)

Sudo systemctl restart apache2
Instalamos mariadb-client para conectarnos al servidor de base de datos

![](Fotos/28.png)

Pasamos la base de datos al servidor mysql

![](Fotos/29.png)

Configuración del servidor de base de datos (MYSQL)

![](Fotos/30.png)

Nos vamos al archivo 50-server.conf y donde esta el bind-address ponemos la ip del server mysql

![](Fotos/31.png)

Entramos a la base de datos y metemos un usuario para la base de datos que hemos pasado antes

![](Fotos/32.png)
![](Fotos/33.png)
![](Fotos/34.png)

Si todo sale bien cuando ponemos nuestro nombre de dns saldra la pagina donde podemos ingresar, eliminar o editar los usuarios de la base de datos.

![](Fotos/35.png)
