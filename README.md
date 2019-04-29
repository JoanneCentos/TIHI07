# Guía Instalación Maquina Virtual

La siguiente será una guía de instalación de la máquina virtual (virtual box) e instalación de sistema operativo (centos7), Nosotros usaremos la versión 6.0.4 disponible para Windows de 64-bits.

Cabe destacar que esta guía está siendo creada con fines didácticos realizados en nuestra maquina personal.


## Sobre CentOS7

CentOS 7 es un sistema operativo de código abierto, basado en la distribución Red Hat Enterprise Linux, operándose de manera similar, y cuyo objetivo es ofrecer al usuario un software de "clase empresarial" gratuito. Se define como robusto, estable y fácil de instalar y utilizar. Desde la versión 5, cada lanzamiento recibe soporte durante diez años, por lo que la actual versión 7 recibirá actualizaciones de seguridad hasta el 30 de junio de 2024. [Ver mas información sobre CentOS 7](https://www.centos.org/)


Table of contents


<!--ts-->
   * [Requisitos Previos](#Requisitos-previos)
   * [Instalación](#Instalación)
   * [Acceso a la red](#Acceso-a-la-red)
   * [Habilitar SSH](#Habilitar-SSH)
   * [Instalación Java 8 JDK](#Instalación-Java-8-JDK)
   * [Instalación ambiente de escritorio](#Instalacion-ambiente-de-escritorio)
<!--te-->


## Requisitos previos


#### Descargar e instalar Oracle VM VirtualBox
Lo primero que haremos será descargar el software de virtualización [Virtual Box (6.0.4)](https://www.virtualbox.org/wiki/Downloads)

#### Descargar e instalar CentOS-7
Una vez que ya tenemos instalada Oracle VM VirtualBox descargaremos la versión mínima del sistema operativo [CentOS-7 versión mínima] (http://isoredirect.centos.org/centos/7/isos/x86_64/CentOS-7-x86_64-Minimal-1810.iso)

#### Descargar e instalar Putty
Cuando ya hayamos descargado CentOS-7 procederemos a descargar el software [Putty versión 0.71] (https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html) e instalarlo respectivamente.



## Instalación


Lo primero que haremos será abrir  el software VirtualBox y seleccionaremos la opción "nuevo"

<img src="https://raw.githubusercontent.com/JoanneCentos/TIHI07/master/Screenshot/Screenshot_1.png">

allí asignaremos un espacio de memoria RAM de 4096mb

<img src="https://raw.githubusercontent.com/JoanneCentos/TIHI07/master/Screenshot/Screenshot_2.png">

A continuación crearemos un disco virtual (VDI Virtual Box Disk Image) de 15GB.

<img src="https://raw.githubusercontent.com/JoanneCentos/TIHI07/master/Screenshot/Screenshot_6.png">

Una vez que finalice el proceso procederemos a iniciar e instalar CentOS-7

En la siguiente ventana seleccionaremos el lenguaje en el cual iremos a trabajar, en este caso, English (United States) o Español (Latinoamerica) y presionaremos "Continuar"

<img src="https://raw.githubusercontent.com/JoanneCentos/TIHI07/master/Screenshot/Screenshot_10.png">

Si todo va correctamente el programa nos pedirá que seleccionemos el destino de la instalación, el cual será nuestro disco de 15GB creado previamente y en la esquina superior izquierda presionaremos "Done"

<img src="https://raw.githubusercontent.com/JoanneCentos/TIHI07/master/Screenshot/Screenshot_12.png">

Para finalizar en la esquina inferior derecha presionaremos "Begin Installation" para comenzar la instalación
Teniendo en cuenta de que nadie más accederá a nuestra maquina crearemos una root password la cual para este caso será "root"
Luego crearemos un usuario el cual tendrá como username "user" y contraseña "user" y para finalizar haremos click en "reboot"
Una vez que termine de reiniciar accederemos con nuestro usuario y contraseña (user)

<img src="https://raw.githubusercontent.com/JoanneCentos/TIHI07/master/Screenshot/Screenshot_17.png">

## Acceso a la red


	En la consola escribiremos el comando "su -" y nuestra contraseña "root", seguido de el comando "ifup enp0s3" (Este comando deberá ser introducido cada vez que apaguemos o reiniciemos la maquina virtual de lo contrario no tendremos acceso a internet dentro de esta)

Luego escribiremos "ip a", comando con el cual podremos ver nuestra dirección IP

Después iremos a nuestra ventana de virtual box y seleccionando nuestro sistema operativo iremos a configuración, iremos a la pestaña de red y haremos click en avanzadas y haremos click en "Reenvió de puertos"

<img src="https://raw.githubusercontent.com/JoanneCentos/TIHI07/master/Screenshot/Screenshot_24.png">

Allí agregaremos la siguiente regla de envíos:

	IP anfitrion: 127.0.0.1 (Nuestra IP local)
	Puerto anfitrion: 8001 (Puerto inutilizado)
	IP invitado: 10.0.2.15 (IP en la consola CentOS-7 en nuestro caso)
	Puerto invitado: 22 (Puerto estandar)

Después abriremos nuestro software Putty donde agregaremos la siguiente IP "127.0.0.1" con puerto "8001"

<img src="https://raw.githubusercontent.com/JoanneCentos/TIHI07/master/Screenshot/Screenshot_23.png">

Si todo ha ido bien nos debería abrir la siguiente ventana donde entraremos con nuestro usuario y contraseña "user"

<img src="https://raw.githubusercontent.com/JoanneCentos/TIHI07/master/Screenshot/Putty.png">


## Habilitar SSH

#### Sobre Secure Shell
SSH (o Secure Shell) es el nombre de un protocolo y del programa que lo implementa cuya principal función es el acceso remoto a un servidor por medio de un canal seguro en el que toda la información está cifrada. Además de la conexión a otros dispositivos, SSH permite copiar datos de forma segura. El protocolo TCP asignado es el 22. [Mas información sobre SSH](https://www.ssh.com/ssh/)


Lo primero que haremos será habilitar SSH a través de nuestra consola. Para instalar el servidor y cliente OpenSSH escribiremos los siguientes comandos.

	"yum -y install openssh-server openssh-clients"
	"chkconfig sshd on"
	"service sshd restart"


## Instalación Java 8 JDK

#### Sobre Java Development Kit
JDK (Java Development Kit) o Herramientas de desarrollo para Java es un software que provee herramientas de desarrollo para la creación de programas en Java. Aquí nos encontraremos con el compilador javac que es el encargado de convertir nuestro código fuente el cual posteriormente sera interpretado y ejecutado con la JVM (Java Virtual Machine) por sus siglas en ingles, que nuevamente al español es La Maquina Virtual de Java.

Como primer paso iremos a nuestra consola como usuario root con el comando e ingresaremos nuestra contraseña

	su -
	
A continuación escribiremos el siguiente comando (Tenga en cuenta que la direccion de enlace pasará a variar dependiendo de la dirección de enlace que esté instalando, para esto copie la direccion de enlace del archivo .rpm en la pagina de [oracle](https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html))

	wget --no-cookies --no-check-certificate --header "Cookie: gpw_e24=http%3A%2F%2Fwww.oracle.com%2F; oraclelicense=accept-securebackup-cookie" "https://download.oracle.com/otn-pub/java/jdk/8u201-b09/42970487e3af4f5aa5bca3f542482c60/jdk-8u201-linux-x64.rpm"


## Instalación ambiente de escritorio

#### Sobre GNOME
GNOME es un entorno de escritorio e infraestructura de desarrollo para sistemas operativos GNU/Linux y Unix compuesto enteramente de software libre.

Para instalar el ambiente de escritorio GNOME escribiremos el siguiente comando

	 yum -y groups install "GNOME Desktop" 

Luego de que el proceso de instalación este terminado usaremos el siguiente comando para iniciarlo (Este comando lo tendremos que iniciar nuevamente cada vez que apaguemos o reiniciemos la maquina virtual)

	startx
	
	
## Instalación Netbeans 8.0.2

Para instalar netbeans iremos con el navegador (Firefox por defecto) a la pagina de [netbeans](#https://netbeans.org/downloads/8.0.2)

<img src="https://raw.githubusercontent.com/JoanneCentos/TIHI07/master/Screenshot/Netbeans.png">

Una vez descargado netbeans (Que por defecto se encontrará en la carpeta de descargas "Downloads") usaremos el siguiente comando con el que buscamos concederle los permisos para su instalación

	chmod +x netbeans-8.0.2-linux.sh

Luego de eso haremos el siguiente comando con el que abriremos el archivo en nuestra carpeta de descargas que nos abrirá el asistente de instalación

	./netbeans-8.0.2-linux.sh
	
###### En caso de que hayamos descargado otra versión de netbeans o que el archivo de descarga tenga un numero diferente lo corroboraremos  viendo el nombre del archivo haciendo

	cd Downloads
	ls

## Instalacion postgreSQL

####  Sobre postgreSQL

es un sistema de gestión de bases de datos relacional orientado a objetos y de código abierto, publicado bajo la licencia PostgreSQL,  similar a la BSD o la MIT.
