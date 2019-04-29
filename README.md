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
<!--te-->


## Requisitos previos


1.-: Descargar e instalar Oracle VM VirtualBox
Lo primero que haremos será descargar el software de virtualización [Virtual Box (6.0.4)](https://www.virtualbox.org/wiki/Downloads)

2.-: Descargar e instalar CentOS-7:
Una vez que ya tenemos instalada Oracle VM VirtualBox descargaremos la versión mínima del sistema operativo [CentOS-7 versión mínima] (http://isoredirect.centos.org/centos/7/isos/x86_64/CentOS-7-x86_64-Minimal-1810.iso)

3.-: Descargar e instalar Putty
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


En la consola escribiremos el comando "su -" y nuestra contraseña "root", seguido de el comando "ifup enp0s3" mostrándonos el siguiente mensaje

Luego escribiremos "ip a" lo cual nos mostrará esta IP
Después iremos a nuestra ventana de virtual box y seleccionando OS iremos a configuración, iremos a la pestaña de red y haremos click en avanzadas y haremos click en "Reenvió de puertos"

Allí agregaremos la siguiente regla de envíos:

	IP anfitrion: 127.0.0.1 (Nuestra IP local)
	Puerto anfitrion: 8001 (Puerto inutilizado)
	IP invitado: 10.0.2.15 (IP en la consola CentOS-7)
	Puerto invitado: 22 (Puerto estandar)

Después abriremos putty donde agregaremos la siguiente IP "127.0.0.1" con puerto "8001"

Si todo ha ido bien nos debería abrir la siguiente ventana donde entraremos con nuestro usuario y contraseña "user"

## Habilitar SSH
================

Luego habilitaremos SSH a través de nuestra consola

Para instalar el servidor y cliente OpenSSH escribiremos "yum -y install openssh-server openssh-clients" en la consola
habilitar al comenzar "chkconfig sshd on"

reiniciar SSHD "service sshd restart"

Ahora pasaremos a instalar java 8 jdk

En la consola escribiremos el comando cd ~

Luego escribiremos lo siguiente:
wget --no-cookies --no-check-certificate --header "Cookie: gpw_e24=http%3A%2F%2Fwww.oracle.com%2F; oraclelicense=accept-securebackup-cookie" "https://download.oracle.com/otn-pub/java/jdk/8u201-b09/42970487e3af4f5aa5bca3f542482c60/jdk-8u201-linux-x64.rpm"
