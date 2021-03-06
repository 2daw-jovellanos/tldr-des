---
title: Introducción
taxonomy:
    category:
        - docs
visible: true
---

### Objetivos
La securización de un sitio web tiene varios objetivos:
* Obtener un cifrado de la comunicación de extremo a extremo, es decir, entre el cliente y el servidor, para mantener:
	*  la **privacidad** de la información: que un tercero no pueda tener acceso a la información mientras viaja por la red
	*  la **integridad** de la comunicación: que un tercero no pueda interceptar la comunicación e incluso falsearla o desviarla [(man in the middle)](https://es.wikipedia.org/wiki/Ataque_de_intermediario)
* Asegurar la **identidad** del sitio web, bien mediante la garantia de que el dominio es veraz, o incluso mediante una verificación extendida, que la empresa que hay detrás también lo es.

### Protocolos
Se basa en añadir una capa de cifrado y verificacion basada en protocolos estándar del IETF:
* El protocolo **TLS** (Transport layer security)
* O bien su antecesor **SSL** (Secure Socket Layer)

Aunque SSL ha sido considerado obsoleto y el estándar actual es TLS1.3 (de 2018), el nombre de SSL se sigue utilizando como sinonimo.

Ambos protocolos se implementan en **cliente** y **servidor**, NO EN EL SISTEMA OPERATIVO, como TCP, UDP, o IP.
Se basan en estándares de intercambio de claves y firmas digitales llamado **X509**, que es un estándar de ITU.

En la comunicación con un sitio web securizado interviene el protocolo **https**, que es realmente el protocolo http, pero la transmisión se realiza cifrada, tras una negociación inicial entre cliente y servidor siguiendo las reglas de TLS (o SSL), y por el puerto 443TCP.
Es decir **https = http + tls**

### Requisitos
Para que el protocolo https funcione es necesario:
* Que cliente y servidor estén preparados para TLS con varios algoritmos de cifrado cada uno. Todos los servidores y clientes modernos lo están.
* Que en el servidor se active https, y para cada host virtual securizado se instale un **certificado**, que contendrá los datos de la identidad del sitio, una clave pública 
* Que el cliente tenga instaladas las claves públicas de las CA que certifican la identidad de los sitios a los que nos conectamos. Con esas claves públicas se comprueba la firma del certificado de los sitios.
    * Firefox de Windows y linux tiene preinstaladas las claves públicas de las principales CA.
    * Chrome, Opera, Safari y derivados utilizan el repositorio de claves del sistema operativo, donde también están las principales CA.
* asimétrica para iniciar la negociación segura y una firma digital que verifique la validez del certificado.

### La PKI
La infraestructura de clave pública (Public Key Infrastructure) es un sistema estándar de emisión de certificados en condiciones de garantia global.  
Se basa en:
* Una serie de empresas llamadas **Autoridades de Certificación** (CA), pertenecientes todas ellas al ITU, que garantizan la identidad de los sitios firmando los certificados que se ponen en los sitios web.
* El protocolo TLS (o SSL), que es una capa adicional a otros protocolos, como http, formando el https. Pero también ftp tiene una versión segura llamada FTP/TLS (que no es lo mismo que SFTP).
* El estándar de intercambio de certificados X.509, en el que las claves se guardan en ficheros con estructura estándar. **Los servidores deben guardar un certificado en formato estándar X.509**, que se descarga al cliente al principio de un transporte cifrado con TLS.  

>>> Existen varios formatos de ficheros de certificados que corresponden con el estándar X.509.  
>>> El formato **pem** y derivados son los habituales de apache. Lo vemos en ficheros con extensión **.pem, crt, key** y algunos otros. Es un fichero que contiene un único objeto criptográfico en formato de texto. Habitualmente, bien un certificado o bien una clave privada.
>>> **.pkcs** es un formato que se utiliza habitualmente en servidores Java o Microsoft. Más compacto, y su origen no está en el ITU, pero tiene la misma funcionalidad.

