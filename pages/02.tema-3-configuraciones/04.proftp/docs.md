---
title: proftp
taxonomy:
    category: docs
visible: true
---

**proftpd** es un popular servidor web con licencia GPL, instalable a través del gestor de paquetes _apt_ desde el repositorio de _ubuntu_.  
web: [proftpd.org](http://www.proftpd.org/)

### Instalación:
```
apt-get -y install proftpd
```

### Configuración.
El fichero de configuración es `/etc/proftpd/proftpd.conf`.  
Es un fichero de directivas con marcas para delimitar regiones.

Por defecto, el usuario _root_ no puede acceder por ftp. Los usuarios "normales" acceden a su _home_, con sus propios privilegios.

Los usuarios pueden moverse por todo el almacenamiento del sistema, a menos que se les _enjaule_ (_jailing_) a su propio directorio _home_:  
(Descomentando o añadiendo la siguiente directiva)
```
DefaultRoot ~
```

### Manejo del servicio
Se dispone de los scripts **service** habituales. El nombre del servicio es `proftpd`.  
Ej: `service proftpd status`


