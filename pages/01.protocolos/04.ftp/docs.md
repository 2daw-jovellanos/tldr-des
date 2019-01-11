---
title: FTP
media_order: 'Abhay.jpg,ftp-windows.png'
taxonomy:
    category: docs
visible: true
---

[TOC]
## Descripción
FTP es el protocolo estándar para la transferencia de ficheros del IETF.  
Está descrito en términos de Cliente/Servicio, de tal manera que la aplicación servidora permite que, desde la aplicación cliente se carguen archivos y se realicen otras operaciones con archivos y carpetas (borrar, crear carpetas, renombrar, listar, permisos...).

* Significado: File Transfer Protocol 
* Nivel: aplicación
* Puerto: **21 TCP** para el control. Luego, abre más puertos aleatorios.
* Versión actual: Sin numerar: Año 1985. Estándar IETF [RFC959](https://tools.ietf.org/html/rfc959). 
* Primera versión de 1971 por _Abhay Bhushan_, MIT.
![Abhay Bhushan](Abhay.jpg) (Abhay Bhushan, India, 1944) 

## Modo de funcionamiento del servicio:
FTP fue creado incluso antes de que TCP/IP se popularizara. Tiene muchas opciones que hoy en día no son demasiado útiles.

 En primer lugar tiene dos modos de funcionamiento: el activo y el pasivo. El que se utiliza hoy en día casi siempre debido a las características de la internet actual es el pasivo.
 
**Pasivo**:  Es el modo más utilizado en éste momento. 
* El servidor abre el puerto TCP21 para la escucha. En ese puerto se establece el transporte de “control”. Los clientes se conectan a él, e intercambian con el servidor mensajes de protocolo acerca qué es lo que van haciendo.
* Siempre que hay que transmitir un fichero en cualquier sentido, el servidor abre un puerto para la transmisión, le indica al cliente qué puerto es por el transporte de control, y espera a que el cliente se conecte. 

**Activo**: prácticamente no utilizado hoy en día.  Los servidores modernos entran en el modo pasivo automáticamente. El lado que debe recibir un fichero (cliente o servidor) abre el puerto 20 TCP y espera a que el otro lado se conecte y le envíe el fichero. Esto no es operativo para clientes situados en redes privadas, que suele ser la situación habitual.

## Usuarios:
Hay dos modos de funcionamiento básicos con respecto a los usuarios:

**Autenticado**: En el servidor se asignan cuentas de usuario, de tal manera que un usuario, identificado por un login y una contraseña tiene acceso a un directorio concreto en el servidor. Se pueden establecer permisos específicos para cada operación (escribir, leer, borrar, etc...).
Las cuentas de usuario pueden coincidir con las de la máquina o no:
* Usuarios reales: El servicio FTP de [vsftpd](https://security.appspot.com/vsftpd.htm) o [proftp](http://www.proftpd.org/) crea accesos ftp para las cuentas de usuarios del sistema linux, utilizando sus privilegios en el sistema. Lo mismo pasa con el servidor **FTP de Windows Server**.
* Usuarios virtuales: El servicio [Filezilla Server](https://filezilla-project.org) para windows o el servicio [pureftpd](https://www.pureftpd.org/project/pure-ftpd) de Linux pueden utilizar usuarios virtuales, que no corresponden a usuarios del sistema.

**Anónimo**: Se puede activar el acceso anónimo, asociado a una determinada carpeta, de tal manera que un usuario identificado con el login “anonymous” puede acceder a esa carpeta. Se utiliza para permitir la descarga de ficheros grandes o con más control que en un servidor http. (Un servidor ftp permite, por ejemplo, control sobre la velocidad de descarga, numero de accesos, y reanudación de descargas interrumpidas).
(el usuario anonymous no necesita contraseña)


## Los ficheros de texto.
En Windows, el fin de línea en ficheros de texto se marca con dos carácteres (CR+LF) frente a uno sólo en sistemas UNIX (CR).
La transmisión FTP entre sistemas distintos permite la conversión de éstos carácteres.
Los clientes como Filezilla automáticamente detectan el tipo de un fichero a transmitir, y si es un fichero de texto lo mandan en el modo texto, para que el servidor realice la conversión de los finales de las líneas, y el resto, en modo binario., en el que no hay conversiones.

El cliente de línea de comandos de Windows o Unix no realiza estas detecciones, con lo que es necesario cambiar manualmente al modo de transferencia texto antes de enviar ficheros de texto, y binario antes de enviar los otros archivos.

## Consideraciones:
* Se pueden manipular desde el cliente los atributos del fichero, siempre en formato UNIX.
* Algunos servidores, como filezilla, permiten la gestión de grupos de usuarios. Eso es un añadido que no forma parte del estándar.
* El protocolo FTP  tiene muchos años, y no ha sufrido modificaciones, aunque se le han hecho algunos añadidos. Eso quiere decir que la compatibilidad entre clientes y servidores es muy grande, y que el protocolo es robusto y estable (a la par que sencillo).
* Se sabe que no funcionará con la IPv6, así que será necesaria una adaptación del protocolo [que ya está prevista desde hace mucho](https://tools.ietf.org/html/rfc2428).
* Los navegadores de estaciones de trabajo (no tablets, no smartphones) tienen incorporado el protocolo FTP solo para descarga de ficheros, manejable a través de una URI con este formato: `ftp://usuario:contraseña@servidor/recurso`, siendo las partes de usuario, contraseña y recurso opcionales. Si no se especifica usuario se utiliza acceso anónimo. Ej: Accede con el navegador al el servidor FTP anónimo de la _Universidade Da Coruña_ haciendo clic en esta URI: [ftp://ftp.udc.es/](ftp://ftp.udc.es/)  
No obstante, este comportamiento de los navegadores puede [que tenga los días contados](https://omicrono.elespanol.com/2018/02/ftp-en-firefox/).
* Windows tiene completamente incorporado el protocolo en su explorador de ficheros y permite la carga, descarga y manipulación de ficheros. Prueba a teclear la URI ftp://ftp.udc.es en la barra del explorador de ficheros de windows.
* En Windows y linux existe preinstalado un [cliente de línea de comandos de ftp](https://es.ccm.net/contents/349-comandos-ftp)
![](ftp-windows.png)
