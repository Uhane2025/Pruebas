En esta vez, se va a realizar la instalación de un servidor zabbix en la nube

el primer paso es la creación de una mv en azure, tenerla en linea y una buena conexión a internet

Notas: Se necesita minimo 4 cpus, 8-16 gm ram y medio tera de almacenamiento

cabe mencionar que esto es para un entorno donde se tienen demaciados equipos conectados a la maquina de monitoreo en abientes más pequeños pueden variar 

Como primer paso es realizar una conexión por medio de ssh, para esta ocasion se hace el apoyo de la aplicación mobaxterm

Una vez completada la conexión usando las contraseñas compartidas por el admin se comienza la instalación del servidor

Primero accedemos a la pagina: https://www.zabbix.com/la/download

Se nos muestra la lista de seleccion de OS, distribusion, etc, para este caso se instalara en un server de prueba de tipo linux, debian, aunque hay una gran variedad para hacer la instalacion, como se muestra en la imagen de abajo

<img width="1630" height="664" alt="image" src="https://github.com/user-attachments/assets/31271cfa-087c-4929-8779-c57eb5350c5f" />

ua vez seleccionados los diferentes componentes de la mv, pasamos a la parte baja de las selecciones donde se nos muestran las diferentes formas de instalar, en este caso vamos a hacer una instalación desde 0 con la mv para el caso de los paquetes

Una vez dentro de moba con ssh, es necesario inresar con privilegios de super usuario para no tener problemas con la instalacion de los diferentes paquetes, para eso usamos el comendo 

SU

damos enter, ingresamos la contraseña

y despues ingresamos el comando:

apt install sudo

esperamos a que se instale, y despue singresaoms la ruta:

nano /etc/sudoers

Lo siguiente es que se aba una ventana donde aparece el codigo de sudoers, y bajamos hasta donde se encuentra el aartado de # User privilege specification y debajo del usuario root escribimos:

USUARIO  ALL=(ALL:ALL) ALL

Cambiamos el apartado de usuario por el usuario que queremos que tenga privilegios, en este caso se pone uno de los diferentes usuarios creados en la mv, para esta practica se uso zabbix y quda el codigo asi:

zabbix ALL=(ALL:ALL) ALL

<img width="1023" height="673" alt="image" src="https://github.com/user-attachments/assets/c85e316f-3738-454d-b697-4fa1bfcf2469" />


Una vez terminado todo esto, se debe usar la combinación de teclas Ctl + O, y dar enter, seguido de esto usamos ctl + X

Despues ingresamos el comando exit para salir el modo root, y usamos el comando:

Sudo apt update y damos enter

lo siguiente es introducir la contraseña del usuario zabbix y dar enter, si comienza una descarga de paquetes, significa que la instalación de sudo fue un exito

lo siguiente es regresar al portal de descraga de zabbix, copiamos el primer comando del apartao 2 agreando al principio SUDO, como por ejemplo

sudo wget https://repo.zabbix.com/zabbix/7.4/release/debian/pool/main/z/zabbix-release/zabbix-release_latest_7.4+debian13_all.deb

damos nter, y despues introducimos el siguiente comando siempre usanod sudo al principio cuando se trate de una interacción con paquetes

sudo dpkg -i zabbix-release_latest_7.4+debian13_all.deb

despues vamos a actualizar con:

sudo apt update

esto es para descargar los paquetes descargados de zabbix

Ahora pasamos a la instalación de los paquetes de zabbix, con el comando.

sudo apt install zabbix-server-pgsql zabbix-frontend-php php8.4-pgsql zabbix-apache-conf zabbix-sql-scripts zabbix-agent2

damos click y esperamos a que se instalen los paquetes, se mostrara un mensaje de confirmación a lo que ingresamos "S" y damos enter, esperanod a que se instalen todos los paquetes

lo siguiente es descargar los plugins con el comando:

sudo apt install zabbix-agent2-plugin-mongodb zabbix-agent2-plugin-mssql zabbix-agent2-plugin-postgresql

al dar eter se comienzan a descargar los diferentes pligins para las bases de datos

como no tebemos instalado postgrest debemos hacer la instalacion desde 0 siguiendo los siguientes comandos:

para instalar las herramientas necesarias:


sudo apt update
sudo apt install curl tar xz-utils -y

Obtener automáticamente la última versión de Postgresql
Postgresql publica sus binarios para Linux en la página oficial. Según la documentación oficial, se descargan como .tar.xz y se extraen con tar en Linux.

sudo apt install -y postgresql postgresql-contrib

Este comando descarga desde la repo de debian

lo siguiente es revisar que se instalo correctamente despues de que se termine la instalacipon con el comando:

sudo systemctl status postgresql
<img width="1115" height="265" alt="image" src="https://github.com/user-attachments/assets/c7a86ef6-f939-44c3-be2e-b2f8f38bd279" />

quedando como se muestra en la imagen de arriba

una vez terminada la instalación seguimos con la instalación de zabbix con el siguiente comando

sudo -u postgres createuser --pwprompt zabbix

Nos pedira una contraseña para estos fines se ocupa: admin123
se repite la contraseña por dos veces debido a la confirmacion 







