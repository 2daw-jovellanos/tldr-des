---
title: 'Modos de ejecución de intérpretes'
taxonomy:
    category: docs
visible: true
---

Los intérpretes de lenguajes como php, ruby o python se pueden ejecutar a petición de un servidor web como apache.

Hay básicamente tres formas de lograrlo, con distintos niveles de concurrencia y eficiencia.

* **CGI** Common gateway interface. Es un estándar para ejecutar programas en servidores web. Es el primer sistema históricamente, y básicamente consiste en que el proceso del servidor web ejecuta el proceso del intérprete y le pasa mediante un sistema estándar información de la petición y de la plataforma, y el proceso intérprete debe devolver contenido en un tipo MIME.  
El intérprete se ejecuta habitualmente como un proceso independiente, y la concurrencia depende del sistema operativo que la gestionará con su propio scheduler. Cuando el intérprete termina de procesar un script, termina, y el sistema operativo dispondrá de sus recursos.
Eficaz pero lento.  
Si el intérprete se desestabiliza no afecta al servicio web, ya que son procesos independientes.
* **módulo** Si existe un módulo para el servidor web (ej: php-apache), el servidor carga el intérprete embebido en su propio proceso y gestiona la concurrencia mediante hilos, y no procesos, compartiendo memoria. Es un sistema rápido y eficaz, pero servidor web e intérprete son un solo proceso. Si se desestabiliza uno, también el otro.
* **fastCGI** es un sistema derivado de CGI, en el que el intérprete se carga en memoria y permanece como servicio, a disposición del servidor web, que se comunica con él mediante sockets u otro mecanismo de comunicación. Servidor web e intérprete son dos procesos independientes que están siempre en ejecución.  
Si se desestabiliza uno, el otro continua por su cuenta con sus propios mecanismos.  
También se permite que estén en máquinas distintas, aunque eso ralentizaría la comunicación.
