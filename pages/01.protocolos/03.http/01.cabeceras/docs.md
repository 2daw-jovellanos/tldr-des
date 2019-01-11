---
title: 'Cabeceras '
taxonomy:
    category: docs
visible: true
---

### Cabeceras que indican las capacidades o características del que envía el mensaje
Nombre | Descripción | Ejemplo | Petición / Respuesta / Los 2
--- | --- | --- | ---
Accept | Content-Types (tipos de contenido) que se aceptan. | `Accept: text/plain`|P
Accept&#8209;Charset | Conjunto de caracteres que se aceptan. | `Accept-Charset: utf-8`|P
Accept&#8209;Encoding | Lista de métodos de compresión que se aceptan. | `Accept-Encoding: gzip, deflate`|P
Accept&#8209;Language | Idiomas que se aceptan. | `Accept-Language: en-US` | P
User&#8209;Agent | Infomación sobre el cliente: navegador, el sistema operativo, plug-ins, etc.| `Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:64.0) Gecko/20100101 Firefox/64.0` | P
|Server|A name for the server|Server: Apache/2.4.1 (Unix)|R

### Cabeceras que describen el contenido
Nombre | Descripción | Ejemplo | P/R
--- | --- | --- | ---
Content&#8209;Type | El tipo MIME de este contenido | `Content-Type: text/html; charset=utf-8` | R
Content&#8209;Length | El tamaño del contenido en bytes | `Content-Length: 348` | R
Content&#8209;Encoding | El tipo de compresión utilizado | `Content-Encoding: gzip` | R
Content&#8209;Language | El idioma natural de la audiencia a la que va dirigida el contenido | `Content-Language: en` | R

### Cabeceras que hacen referencias a URIs
Nombre | Descripción | Ejemplo | P/R
--- | --- | --- | ---
Location|Usado en redirección, o cuando se crea un nuevo recurso|`Location: http://www.w3.org/pub/WWW/People.html` <br> `Location: /pub/WWW/People.html`|R
Referer | El recurso del que proviene la solicitud (ej: img, a, link, script, etc) | `Referer: http://en.wikipedia.org/wiki/Main_Page`|P

### Cabeceras que permiten ahorrar transmisiones
Nombre | Descripción | Ejemplo | P/R
--- | --- | --- | ---
Date | Fecha y hora del mensaje, en formato estandar | `Date: Tue, 15 Nov 1994 08:12:31 GMT` | 2
ETag | Es un identificador opaco asignado por el servidor a una versión específica de un recurso encontrado en una URL. Si la representación del recurso cambia, se asigna un nuevo ETag. Usado de esta manera, se puede considerar al ETag como una huella digital. | `ETag: "737060cd8c284d8af7ad3082f209582d"`|R
If&#8209;Match | Realiza una acción solo si la representación del recurso en el servidor coincide con el ETag | `If-Match: "737060cd8c284d8af7ad3082f209582d"`|P
If&#8209;Modified&#8209;Since | Permite una respuesta 304 Not Modified si el contenido no ha cambiado.|`If-Modified-Since: Sat, 29 Oct 1994 19:43:31 GMT`|P
If&#8209;Unmodified&#8209;Since, If&#8209;None&#8209;Match, If&#8209;Range | Similares, con distintas condiciones | |P
Expires | Fecha y hora en que el contenido se debe considerar obsoleto | `Expires: Thu, 01 Dec 1994 16:00:00 GMT`|R
Last&#8209;Modified | Fecha de la última modificación del contenido | `Last-Modified: Tue, 15 Nov 1994 12:45:26 GMT` | R
Cache&#8209;Control | El servidor le indica a los mecanismos de caché del cliente cómo debe guardar el contenido. Medido en segundos | `Cache-Control: max-age=3600`<br>`Cache-Control: no-cache`|R
Via| Informa al cliente de los proxies que han procesado la respuesta | `Via: 1.0 fred, 1.1 example.com (Apache/1.1)`|R
Pragma | Forma de especificar que el recurso no debe ser cacheado en HTTP/1.0. (Por compatiblidad). En HTTP/1.1 se ututiza Cache-Control | Pragma: no-cache

### Cabeceras para el control de cookies
Una cookie es un pequeño fragmento de información en forma varias claves con sus respectivos valores que un servidor envía al cliente, y este tiene la obligación de guardar hasta que expire y enviarla de vuelta al servidor en cada comunicación.

De esta manera, un servidor http, que no guarda estado por sí mismo, puede guardarlo en el cliente.
Sirve principalmente para el mantenimiento de sesiones, pero también para fines publicitarios o de seguimiento de hábitos de conducta, para configuraciones sencillas de aplicaciones, etc.

Nombre | Descripción | Ejemplo | P/R
--- | --- | --- | ---
Set&#8209;Cookie | El servidor establece una cookie que el cliente debe conservar | `Set-Cookie: UserID=JohnDoe; Max-Age=3600; Version=1`|R
Cookie | Envía una cookie previamente establecida por un servidor | `Cookie: $Version=1; Skin=new;`|P

### Cabeceras para autentificación
Aunque no es muy utilizado, HTTP admite que para acceder a un determinado recurso, el servidor deba solicitar credenciales por sus propios medios.

Authorization, WWW-Autenthicate

### Cabeceras para el control de la conexión
Nombre | Descripción | Ejemplo | P/R
--- | --- | --- | ---
Host | Indica nombre de dominio y puerto al que va dirigida la petición | `Host: es.wikipedia.org`<br>`Host: es.prueba.com:8080` | P
Connection | De HTTP/1.0. Controla si la conexión debe permanecer abierta. En HTTP/1.1 todos los transportes son persistentes y los cierra el servidor tras un timeout | `Connection: keep-alive` | 2

<hr>
>>> [Listado de todas las cabeceras HTTP](https://en.wikipedia.org/wiki/HTTP_headers) en Wikipedia