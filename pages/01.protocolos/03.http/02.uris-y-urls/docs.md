---
title: 'URIs y URLs'
taxonomy:
    category: docs
visible: true
---

Los navegadores pueden manejar de manera nativa los protocolos **http**, **https** y **ftp** para lectura. De manera indirecta pueden derivar a otras aplicaciones solicitudes de uso de otros protocolos, por ejemplo el correo electrónico o una llamada de telefónica en un movil.

El navegador maneja los recursos identificándolos mediante una URI.
La definición de URI, y URL (un subconjunto de las URI) se encuentra estandarizada por el IETF en el [RFC3986](https://tools.ietf.org/html/rfc3986)

**URI: _Universal Resource Identifier_**: Un mecanismo estándar para identificar a un recurso en la web.  
Empieza por un identificador de protocolo, seguido de dos puntos (:) y un formato propio dependiente del protocolo.

**URL: _Universal Resource Locator_**: Un mecanismo estándar para identificar a un recurso en la web, pero especificando su localización, dependiente del protocolo. **Toda URL es una URI. El término URI es más generico y engloba al de URL**.


Ej de URI:

* ftp://ftp.is.co.za/rfc/rfc1808.txt    &larr;
* http://www.ietf.org/rfc/rfc2396.txt   &larr;
* tel:+1-816-555-1212
* mailto:John.Doe@example.com  
* jdbc:h2:~:test

De estas, las dos primeras se pueden considerar URL, porque indican dónde esta el recurso.


(Ej del mundo real: en el intituto "Victor Fernández" me identifica (podría considerarse una URI), pero si preguntas por "El profesor de despliegue del aula 6", también me identifica, y además me localiza (podría considerarse una URL).