---
title: Introducción
taxonomy:
    category:
        - docs
visible: true
---

### Objetivos
La securización de un sitio web tiene dos objetivos:
1. Obtener un cifrado de la comunicación de extremo a extremo, es decir, entre el cliente y el servidor, para mantener la privacidad de la comunicación.
2. Asegurar la identidad del sitio web

### Protocolos
Se basa en añadir una capa de cifrado y verificacion basada en protocolos estándar del IETF:
* El protocolo **TLS** (Transport layer security)
* O bien su antecesor **SSL** (Secure Socket Layer)

Ambos protocolos se implementan en **cliente** y **servidor**, NO EN EL SISTEMA OPERATIVO, como TCP, UDP, o IP.
Se basan en estándares de intercambio de claves y firmas digitales llamado **X509**, que es un estándar de ITU.

En la comunicación con un sitio web securizado interviene el protocolo **https**, que es realmente el protocolo http, pero la transmisión se realiza cifrada, tras una negociación inicial entre cliente y servidor siguiendo las reglas de TLS (o SSL), y por el puerto 443TCP.
Es decir **https = http + tls**

### Requisitos
Para que el protocolo https funcione es necesario:
* Que cliente y servidor estén preparados para TLS con varios algoritmos de cifrado cada uno. Todos los servidores y clientes modernos lo están.
* Que en el servidor se active https, y para cada host virtual securizado se instale un **certificado**, que contendrá los datos de la identidad del sitio, una clave pública asimétrica para iniciar la negociación segura y una firma digital que verifique la validez del certificado.

### La PKI
La infraestructura de clave pública (Public Key Infrastructure) es un sistema estándar de emisión de certificados en condiciones de garantia global.  
Se basa en:
* Una serie de empresas llamadas **Autoridades de 

