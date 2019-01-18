---
title: Apache
taxonomy:
    category:
        - docs
visible: true
---

Apache deriva del servidor web original de la NCSA. 
La versión actual es la 2.4
Es el servidor web con mayor número de instalaciones en internet. Se calcula que no menos del 60% de los sitios web de internet lo utilizan. 
Es altamente modular y configurable. Es muy rápido y con un funcionamiento estable. 
Muy bien documentado  
100% software libre, mantenido por la Fundación Apache. [apache.org](http://apache.org/)

## instalación y configuración en Debian, Ubuntu, Mint y derivados
```
apt-get -y install apache2
```

* El fichero de configuración principal está en `/etc/apache2/apache2.conf`
* Cada sitio web tiene su propia configuración, que se carga con directivas include, desde el fichero principal
* Las configuraciones de los sitios se guardan en `/etc/apache2/sites-available`. Un fichero por sitio.
* Apache es un sistema modular, con varios modulos, activables por separado. Cada uno tiene su configuración en `/etc/apache2/mods-available`.


El servicio apache2 tiene scripts de **service**, así que se aplica lo mismo que ya sabemos para OpenSSH y proftpd.

Viene con una serie de scripts auxiliares:
* `a2ensite` y `a2dissite` activan y desactivan un sitio, respectivamente. Aceptan como parámetro el nombre de un fichero de configuración del sitio, que tendremos que crear previamene.  
Crean y quitan respectivamente un enlace simbólico en la carpeta `/etc/apache2/sites-enabled`, de tal manera que si hay enlace el sitio está activo y si no, no.
* `a2enmod` y `a2dismod` actuan de la misma manera con módulos. Los ficheros de configuración básica de los módulos ya existen, y se pueden configurar de manera específica para cada site en el fichero de configuración del site. Un módulo activo tiene un enlace simbólico en `/etc/apache2/mods-enabled`

Se ejecuta con el usuario `www-data` del grupo `root`.  
La carpeta `/var/www` está a disposición de apache para guardar sitios web.  
La carpeta `/var/www/html` contiene los archivos del sitio por defecto.

Si vamos a crear más sitios, es sensato crearlos dentro de `/var/www`.


