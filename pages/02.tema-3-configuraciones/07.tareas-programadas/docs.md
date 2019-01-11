---
title: 'Tareas programadas'
taxonomy:
    category:
        - docs
visible: true
---

[TOC] En el sistema operativo Unix y derivados, cron es un demonio que ejecuta procesos o scripts a intervalos regulares (por ejemplo, cada minuto, día, semana o mes). Los procesos que deben ejecutarse y la hora en la que deben hacerlo se especifican en el fichero crontab.

## Cómo funciona

El demonio cron inicia de `/etc/rc.d/` o `/etc/init.d` dependiendo de la distribucion. Cron se ejecuta en background y revisa cada minuto la tabla de tareas crontab en `/etc/crontab` o en `/var/spool/cron` en búsqueda de tareas que se deban cumplir. Como usuario podemos agregar comandos o scripts con tareas a cron para automatizar algunos procesos. Esto es util por ejemplo para automatizar la actualizacion de un sistema o un buen sistema de respaldos.

### ¿Qué es Crontab?

Crontab es un simple archivo de texto que guarda una lista de comandos a ejecutar en un tiempo especificado por el usuario. Crontab verificará la fecha y hora en que se debe ejecutar el script o el comando, los permisos de ejecución y lo realizará en el background. Cada usuario puede tener su propio archivo crontab, de hecho el `/etc/crontab` se asume que es el archivo crontab del usuario root, cuando los usuarios normales (e incluso root) desean generar su propio archivo de crontab, entonces utilizaremos el comando crontab.

Crontab es la manera mas sencilla de administrar tareas de cron en sistemas multiusuario, ya sea como usuario normal de sistema o usuario root.

#### Agregar tareas a crontab

Ejecutamos la edición del crontab con `crontab -e`, en algunas distribuciones como ubuntu nos da la opcion de elegir el editor de textos que deseemos, en las demás se suele utilizar el editor vi. El archivo crontab será de este estilo:

```
# m h dom mon dow command
```

donde:
* m corresponde al minuto en que se va a ejecutar el script, el valor va de 0 a 59
* h la hora exacta, se usa el formato de 24 horas, los valores van de 0 a 23 
* dom hace referencia al día del mes, por ejemplo se puede especificar 15 si se quiere ejecutar cada dia 15
* dow significa el día de la semana, puede ser numérico (0 a 7, donde 0 y 7 son domingo) o las 3 primeras letras del día en inglés: mon, tue, wed, thu, fri, sat, sun.
* command refiere al comando o a la ruta absoluta del script a ejecutar, ejemplo: /home/usuario/scripts/actualizar.sh, si se llama a un script este debe ser ejecutable

Ejemplos:

* `15 10 * * * /home/usuario/scripts/actualizar.sh` Ejecutará el script actualizar.sh a las 10:15. todos los días
* `15 22 * * * /home/usuario/scripts/actualizar.sh` Ejecutará el script actualizar.sh a las 22:15. todos los días
* `00 10 * * 0 apt-get -y update` Ejecutará una actualización todos los domingos a las 10:00
* `45 10 * * sun apt-get -y update` Usuario root ejecutará una actualización todos los domingos (sun) a las 10:45
* `30 7 20 11 * /home/usuario/scripts/actualizar.sh` El día 20 de noviembre a las 7:30, con las credenciales de `usuario` 
* `30 7 11 11 sun /home/usuario/scripts/pastel_con_velitas.sh` El día 11 de noviembre a las 7:30 a.m. y que sea domingo.
* `1 * * * * /home/usuario/scripts/molestorecordatorio.sh` Cada minuto 1

Se puede especificar más de un valor en cada campo temporal separándolos con comas, y sin espacios:

* `30 17 * * 1,3,5` A las 5:30 de la tarde todos los días lunes, miércoles y viernes.
* `00 12 1,15,28 * *` A las 12 del día todos los días primero, quince y 28 de cada mes

Se puede especificar un rango con guiones

* `30 17 * * 1-5` A las 5:30 de la tarde todos los días de lunes a viernes.

Se puede especificar fracciones de tiempo en cada campo, escribiendo en el campo `*/n` siendo n la fracción de tiempo
* `*/5 * * * *` Cada 5 minutos.
* `*/5 2-8 * * *` Cada 5 minutos entre las 2 y las 8 de la mañana, ambas incluidas.
* `*/1 * * * * /home/usuario/scripts/molestorecordatorio.sh` Cada minuto


Crontab también tiene algunas marcas especiales.

* `@reboot` Ejecuta una vez, al inicio
* `@yearly` ejecuta sólo una vez al año. Igual que `0 0 1 1 *`
* `@annually` igual que @yearly
* `@monthly` ejecuta una vez al mes, el día primero: 0 0 1 * *
* `@weekly` Semanal el primer minuto de la primer hora de la semana. 0 0 * * 0″.
* `@daily` diario, a las 12:00A.M. 0 0 * * *
* `@midnight` igual que @daily
* `@hourly` al primer minuto de cada hora: 0 * * * *

Ejemplos:
```
@hourly /home/usuario/scripts/molestorecordatorio.sh
@monthly  /home/usuario/scripts/respaldo.sh
@daily apt-get update && apt-get -y upgrade
```

#### Algunos Comandos de administracion de trabajos en cron
* `crontab archivo` Remplaza el existente archivo crontab con un archivo definido por el usuario
* `crontab -e` Editar el archivo crontab del usuario, cada linea nueva sera una nueva tarea de crontab.
* `crontab -l` Lista todas las tareas de crontab del usuario
* `crontab -d` Borra el crontab del usuario


Sitio web recomendado para probar tus configuraciones de crontab: [crontab.guru](https://crontab.guru)