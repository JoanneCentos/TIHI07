# Instalación máquina virtual: 🔧

Integrantes:  ✒️
* Felipe rodriguez,
* Rene barria,
* Ricardo gallardo,

La siguiente será una guía de instalación de la máquina virtual (virtual box) e instalación de sistema operativo (centos7), Nosotros usaremos la versión 6.0.4 disponible para Windows de 64-bits.

Cabe destacar que esta guía está siendo creada con fines didácticos realizados en nuestra maquina personal. Estos serán los programas necesarios:

### 1.-: descargar e instalar virtual box:

Para descargarlo le dejamos el link la página oficial:
Virtual Box (6.0.4): https://www.virtualbox.org/wiki/Downloads

2.-: descargar e instalar CentOS-7:

Una vez que ya tenemos instalada virtual box descargaremos la versión mínima de CentOS-7.

CentOS-7(versión mínima): http://isoredirect.centos.org/centos/7/isos/x86_64/CentOS-7-x86_64-Minimal-1810.iso

1.-: descargar e instalar Putty:}

Cuando ya hayamos descargado CentOS-7 procederemos a descargar el software putty e instalarlo respectivamente.

Putty (versión 0.71): https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html

 Instalación máquina.
 
Luego abriremos el software de virtual box y seleccionaremos la opción "nuevo", allí asignaremos un espacio de memoria RAM de 4096mb
A continuación crearemos un disco virtual (VDI Virtual Box Disk Image) de 15GB.

Una vez que finalice el proceso procederemos a iniciar e instalar CentOS-7
En la siguiente ventana seleccionaremos el lenguaje en el cual iremos a trabajar, en este caso, English (United States) y presionaremos "Continuar"

Si todo va correctamente el programa nos pedirá que seleccionemos el destino de la instalación, el cual será nuestro disco de 15GB creado previamente y en la esquina superior izquierda presionaremos "Done"

Para finalizar en la esquina inferior derecha presionaremos "Begin Installation" para comenzar la instalación
Teniendo en cuenta de que nadie más accederá a nuestra maquina crearemos una root password la cual para este caso será "root"
Luego crearemos un usuario el cual tendrá como username "user" y contraseña "user" y para finalizar haremos click en "reboot"
Una vez que termine de reiniciar accederemos con nuestro usuario y contraseña (user)

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
Luego habilitaremos SSH a través de nuestra consola

Para instalar el servidor y cliente OpenSSH escribiremos "yum -y install openssh-server openssh-clients" en la consola
habilitar al comenzar "chkconfig sshd on"

reiniciar SSHD "service sshd restart"

Ahora pasaremos a instalar java 8 jdk

En la consola escribiremos el comando cd ~

Luego escribiremos lo siguiente:
wget --no-cookies --no-check-certificate --header "Cookie: gpw_e24=http%3A%2F%2Fwww.oracle.com%2F; oraclelicense=accept-securebackup-cookie" "https://download.oracle.com/otn-pub/java/jdk/8u201-b09/42970487e3af4f5aa5bca3f542482c60/jdk-8u201-linux-x64.rpm"
