---
title: Comandos
taxonomy:
    category:
        - docs
visible: true
---

Algunos comandos básicos de linux:
## Directorios y ficheros
* `mkdir` crea directorios, `rmdir` borra directorios
*  `mv` mueve directorios o ficheros, o simplemente les cambia el nombre
*  `cp` hace copias de ficheros y directorios
*  `ls` lista el contenido `ls -l` muestra información completa, con propietarios y permisos.

## Usuarios y permisos
* `useradd` y `adduser` añaden un usuario al sistema. 
* `groupadd` y `addgroup` añaden un grupo al sistema.
* `chown` cambia el propietario de un archivo o directorio.
* `chmod` cambia los permisos de un archivo o directorio. (`chmod g+s` en un directorio fuerza a que su contenido tome el grupo de ese directorio, y no del creador del contenido. El cambio del propietario no se puede forzar.)
* `setfacl` fija la **l**ista de **c**ontrol de **a**cceso a un **f**ichero  o carpeta. En cierto modo, se parece a _chmod_, pero con otra sintaxis. Sin embargo, tiene un modificador `-d` (default) que fija los permisos por defecto que tendrán los futuros ficheros o carpetas que se metan dentro.
    *  Ejemplo: `setfacl -dR g::rwX directorio` aplica permisos por defecto (`-d`) y de manera recursiva (`-R`) a la carpeta _directorio_ que adquirirá su futuro contenido. Los permisos son de grupo (por la `g`) y de lectura, escritura (`rw`) y ejecucion solo para directorios, pero no ficheros (por la `X` en mayúsculas, si fuera en minúsculas sería también para ficheros).
    *  Otro ejemplo: análogamente, `setfacl -dR o::rwX directorio` aplica los permisos para todos los usuarios (`o`, de _others_)