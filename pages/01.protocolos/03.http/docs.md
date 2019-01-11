---
title: HTTP
taxonomy:
    category: docs
visible: true
---

[TOC] 
## Descripción
El Protocolo de transferencia de hipertexto (en inglés: Hypertext Transfer Protocol o HTTP) es el protocolo de comunicación que permite las transferencias de información en la World Wide Web. HTTP fue desarrollado por el _World Wide Web Consortium_ y la _Internet Engineering Task Force_, colaboración que culminó en 1999 con la publicación de una serie de RFC, el más importante de ellos es el RFC 2616 que especifica la versión 1.1. 

HTTP define la sintaxis y la semántica que utilizan los elementos de software de la arquitectura web (clientes, servidores, proxies) para comunicarse. 

HTTP <mark>**es un protocolo sin estado**</mark>, es decir, no guarda ninguna información sobre conexiones anteriores. El desarrollo de aplicaciones web necesita frecuentemente mantener estado. Para esto se usan otros mecanismos, como las cookies, que es información que un servidor puede almacenar en el sistema cliente. Esto le permite a las aplicaciones web instituir la noción de sesión, y también permite rastrear usuarios ya que las cookies pueden guardarse en el cliente por tiempo indeterminado. 

* Significado: Protocolo de transferencia de hypertexto.
* Nivel: aplicación
* Puerto: **80 TCP**
* Versión actual: 1.1. Año 1999. Estándar IETF [RFC2616](https://tools.ietf.org/html/rfc2616). 
   * Versión en actualización: 2.0. Año 2015. Estándar IETF [RFC7540](https://tools.ietf.org/html/rfc7540). 
* Primera versión de 1991 por _Tim Berners-Lee_, CERN Suiza
![Tim Berners-Lee](https://upload.wikimedia.org/wikipedia/commons/thumb/9/9d/Sir_Tim_Berners-Lee.jpg/640px-Sir_Tim_Berners-Lee.jpg) 
(Tim Berners-Lee, Reino Unido 1955) 

> Tim Berners-Lee desarrolló también la primera versión de HTML, y extendió el uso de la www.  
> Fue el primer presidente del **w3c**. El IETF reformó el protocolo en 1996 para darle las bases de lo que es hoy.

![El primer servidor web](https://upload.wikimedia.org/wikipedia/commons/thumb/d/d1/First_Web_Server.jpg/640px-First_Web_Server.jpg)
El primer servidor web fue el propio ordenador de Berners-lee en el CERN

## Estructura del mensaje.
En una comunicación http
1. El cliente abre un transporte hacia el servidor
2. El cliente envía un mensaje de **petición** al servidor
3. El servidor intenta satisfacer la petición enviando un mensaje de **respuesta**
4. Si el cliente tiene más peticiones, volvemos al paso 2, si no, el servidor cierra el transporte pasado un _timeout_ de unos pocos segundos.

Los mensajes HTTP, son en texto plano lo que lo hace más legible y fácil de depurar. Esto tiene el inconveniente de hacer los mensajes más largos.
Los mensajes tienen la siguiente estructura:

* Línea inicial (termina con retorno de carro y un salto de línea) con
    * Para las peticiones: la acción requerida por el servidor (método de petición) seguido del recurso y la versión HTTP que soporta el cliente.
    * Para respuestas: La versión del HTTP usado seguido del código de respuesta (que indica que ha pasado con la petición seguido de la URL del recurso) y de la frase asociada a dicho retorno.
* Las cabeceras del mensaje que **terminan con una línea en blanco**. Son metadatos. Estas cabeceras le dan gran flexibilidad al protocolo.
* Cuerpo del mensaje. Puede estar o no: su presencia depende de la línea anterior del mensaje y del tipo de recurso al que hace referencia la URL. Típicamente tiene los datos que se intercambian cliente y servidor. 
    * La petición puede contener datos para que el servidor los procese
    * La respuesta suele incluir los datos que el cliente ha solicitado.

## Petición
Ejemplo:
```http
 GET /index.html HTTP/1.1
 Host: www.example.com
 Referer: www.google.com
 User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:45.0) Gecko/20100101 Firefox/45.0
 Connection: keep-alive
 [Línea en blanco]
 ```

### 1ª Línea
La primera línea tiene la estrucutra `método recurso versión`. Ej:
```http
GET /pagina.html HTTP/1.1
```

* métodos (o _verbos_): Hay 20.
   * principales:
      * **GET** El método GET solicita **una representación del recurso** especificado. Las solicitudes que usan GET solo deben recuperar datos y _no deben tener ningún otro efecto_.
      * **POST** Envía los datos **para que sean procesados por el recurso** identificado. Los datos **se incluirán en el cuerpo de la petición**. Esto puede resultar en _la creación de un nuevo recurso o de las actualizaciones de los recursos existentes o ambas cosas_. <mark>El recurso debe procesar la infomación</mark>
      * **PUT** Envía datos para que **sean almacenados en el recurso que se indica**. (Se utiliza con javascript)
      * **DELETE** Solicita que sea borrada información relacionada con el recurso. (Se utiliza con javascript)
   * auxiliares:
      * HEAD Con el mismo significado que GET, pero el servidor no enviará cuerpo. Util para conocer el estado de representación de un recurso sin descargar el recurso.
      * TRACE El cliente solicita que el servidor le envíe de vuelta su propia petición. Util para saber si hay servidores intermedios que puedan alterar los mensajes.
      * OPTIONS Devuelve los métodos que soporta un servidor
      * CONNECT Abre un túnel HTTP: una conexión bidireccional basada en HTTP. Es la base del protocolo seguro HTTPS, y de la conexión entre servidores HTTP para proxy.
   * poco utilizados: PATCH, SEARCH, COPY, LOCK, UNLOCK, MOVE, MKCOL, PROPFIND, PROPPATCH, MERGE, UPDATE, LABEL. (no nos los aprederemos). 
   
### Cabeceras
En cada línea hay una propiedad, seguida de dos puntos (:), un espacio y un valor válido
Terminan con un cambio de línea.

* Cabeceras que indican las capacidades aceptadas por el que envía el mensaje: **Accept** (indica el MIME aceptado), **Accept-Charset** (indica el código de caracteres aceptado), **Accept-Encoding** (indica el método de compresión aceptado), **Accept-Language** (indica el idioma aceptado), **User-Agent** (para describir al cliente), **Server** (indica el tipo de servidor), **Allow** (métodos permitidos para el recurso)
* Cabeceras que describen el contenido: **Content-Type** (indica el **_MIME_** del contenido), **Content-Length** (longitud del mensaje), **Content-Range**, **Content-Encoding**, **Content-Language**, **Content-Location**.
* Cabeceras que hacen referencias a URIs: **Location** (indica donde está el contenido), **Referer** (Indica el origen de la petición).
* Cabeceras que permiten ahorrar transmisiones: **Date** (fecha de creación), **If-Modified-Since**, **If-Unmodified-Since**, **If-Match**, **If-None-Match**, **If-Range**, **Expires**, **Last-Modified**, **Cache-Control**, **Via**, **Pragma**, **Etag**, **Age**, **Retry-After**.
* Cabeceras para control de cookies: **Set-Cookie**, **Cookie**
* Cabeceras para autentificación: **Authorization**, **WW-Authenticate**
* Cabeceras para describir la comunicación: **Host** (indica máquina destino del mensaje), **Connection** (indica como establecer la conexión)
* Otras: **Range** (para descargar sólo partes del recurso), **Max-Forward** (límite de cabeceras añadidas en TRACE).

>>> Ver: [Cabeceras más utilizadas, en este mismo sitio](/protocolos/http/cabeceras)

### Cuerpo
Si hay cuerpo en la petición, suelen ser datos a procesar por el servidor.

Ej: En post, cada campo recogido por el formulario va en este formato:
```http
nombre=Recesvinto
ciudad=Fuenlabrada
```

Ej: Una petición realizada desde javascript podría enviar los datos en el lenguaje de marcas JSON
```js
{
    "nombre":"Recesvinto",
    "ciudad":"Fuenlabrada"
}
```


## Respuesta
Ejemplo
```http
HTTP/1.1 200 OK
Date: Fri, 31 Dec 2003 23:59:59 GMT
Content-Type: text/html
Content-Length: 1221

<html lang="eo">
<head>
<meta charset="utf-8">
<title>Título del sitio</title>
</head>
<body>
<h1>Página principal de tu host</h1>
(Contenido)
  .
  .
  .
</body>
</html>
```
### 1ª Línea

La primera línea tiene la estrucutra `version código_respuesta mensaje_informativo`. Ej:
```http
HTTP/1.1 200 OK
```

Los códigos informativos tienen tres cifras:
* 1XX Respuestas informativas
* 2XX Peticiones correctas. El más frecuente: 200.
* 3XX Redirecciones. El cliente tiene que reformular la petición.
* 4XX Errores del cliente. Ej. 404: el cliente ha especificado un recurso que el servidor considera que no existe
* 5XX Errores del servidor. Ej. 500: Error interno: el servidor tuvo un error al procesar la petición.

El mensaje informativo lo emite el servidor, y no tiene ninguna vinculación con respecto al cliente. Por ejemplo, el error 404 suele venir acompañado del mensaje _Not found_, pero podría tener cualquier otro texto.

>>> [Listado de todos los códigos de respuesta HTTP](https://es.wikipedia.org/wiki/Anexo:C%C3%B3digos_de_estado_HTTP) en wikipedia

Aprende al menos éstos:

Código | Nombre | Descripción
------ | ------ | -----------
200 | Ok | Respuesta estándar para peticiones correctas.
307 | Temporary Redirect | HTTP/1.1 Una redirección. La peticón debería haber sido hecha con otra URI, sin embargo aún puede ser procesada con la URI proporcionada. Similar a 303, pero indica que el método de la petición no debería ser cambiado cuando el cliente repita la solicitud. Por ejemplo, una solicitud POST tiene que ser repetida utilizando otra petición POST.
308 | Permanent Redirect | El recurso solicitado por el navegador se encuentra en otro lugar y este cambio es permanente. Similar a 301, pero no se permite cambiar el método HTTP para la nueva petición
400 | Bad Request | La solicitud contiene sintaxis errónea y no debería repetirse.
403 | Forbidden | La solicitud fue legal, pero el servidor rehúsa responderla dado que el cliente no tiene los privilegios para hacerla. Similar a 401 No autorizado, pero más específica.
404 | Not Found | Recurso no encontrado. Se utiliza cuando el servidor web no encuentra el recurso solicitado. 
500 | Internal Server Error | Emitido comunmente cuando hay errores en la configuración del servidor o de la aplicación web
503 | Service Unavailable | El servidor no puede responder a la petición por congestión, sobrecarga o conflictos en alguno de sus componentes.

### Cabeceras servidor
Las cabeceras del servidor tienen el mismo formato que las cabeceras del cliente.

>>> Ver: [Cabeceras más utilizadas, en este mismo sitio](/protocolos/http/cabeceras)

### Cuerpo
El cuerpo del mensaje constituye la respuesta del servidor. Habitualmente son representaciones de recursos o datos.
El servidor informa del tipo y de la longitud de la respuesta en la cabecera, con los campos **Content-Type** y **Content-Length** respectivamente.

Los tipos de representación vienen definidos por el estandar [MIME](https://es.wikipedia.org/wiki/Multipurpose_Internet_Mail_Extensions). 
>>>>> _Multipurpose Internet Mail Extensions o MIME_ (en español "extensiones multipropósito de correo de internet") son una serie de convenciones o especificaciones dirigidas al intercambio a través de Internet de todo tipo de archivos (texto, audio, vídeo, etc.) de forma transparente para el usuario.

MIME asigna un nombre a cada tipo de datos. Los nombres siguen el formato **tipo/subtipo** 

El tipo define la categoría general de los datos y el subtipo define un tipo más específico de esos datos.
Ej:
* **text/plain** &rarr; formato por defecto para texto plano
* text/html &rarr; fichero html
* text/css &rarr; css
* application/javascript &rarr; javascript
* image/jpeg  &rarr; binario conteniendo una imagen en formato jpeg
* image/png   &rarr; binario conteniendo una imagen en formato png
* audio/mpeg   &rarr; binario conteniendo audio en formato mp3
* video/mp4   &rarr; binario conteniendo una vídeo en formato mp4
* application/json   &rarr; lenguaje de marcas json
* application/xml &rarr; lenguaje de marcas xml
* application/zip &rarr; binario comprimido zip
* application/pdf &rarr; binario pdf
* **application/octet-stream** &rarr; binario genérico

>>> [Lista completa de tipos MIME importantes en la web](https://developer.mozilla.org/es/docs/Web/HTTP/Basics_of_HTTP/MIME_types/Lista_completa_de_tipos_MIME) _Mozilla Developer Network (MDN)_ 
