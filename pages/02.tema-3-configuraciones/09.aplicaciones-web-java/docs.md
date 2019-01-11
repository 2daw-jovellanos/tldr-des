---
title: 'Aplicaciones Web Java'
taxonomy:
    category:
        - docs
visible: true
---

[TOC]
## Tipos de scripts en aplicaciones Java
Una aplicación web en java es una unidad bien definida que consta de varios scripts en Java, junto con cualquier otro contenido habitual de la web (html, css, js, multimedia, bases de datos, etc)

Hay varias tecnologías de scripts, pero las más utilizadas son los Servlets y las JSP. Estas tecnologías forman parte de Java Enterprise Edition, que está implementado en los propios servidores de aplicaciones Java.
### servlets
Un servlet es una clase en el lenguaje de programación Java, que se instala en un servidor de aplicaciones preparado para este tipo de clases, y que puede responder a cualquier tipo de solicitudes http. Típicamente, el servlet genera contenido de manera dinámica (como un programa en PHP o en ASP.NET). Es una tecnología antigua pero potente, ya que desde un servlet puede utilizarse la mayor parte de capacidades de Java, y también las capacidades que ofrezca el servidor en el que se aloja.
No es habitual ver aplicaciones completas compuestas de servlets, ya que los JSP son más sencillos de utilizar y de más alto nivel.  La palabra servlet deriva de otra anterior, applet, que se refiere a pequeños programas que se ejecutan en el contexto de un navegador web.

Un servlet extiende a la clase `javax.servlet.HttpServlet` (de Java EE), y su funcionalidad básica se expresa haciendo overriding de una serie de método que pueden manejar una petición http con un detrminado método http:
* `public void doGet(HttpServletRequest request, HttpServletResponse response)`
* `public void doPost(HttpServletRequest request, HttpServletResponse response)`
* Etc...  para el resto de los métodos http (put, delete, head, etc.)

Mediante el descriptor de despliegue se asocia un servlet a una URI.
Cada uno de los métodos de la clase cuenta con dos parámetros, representando a la petición http, y a la respuesta. Estos objetos tienen casi todo lo necesario para tramitar la petición.

``` Java
// Import required java libraries
import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;

// Extend HttpServlet class
public class HelloWorld extends HttpServlet {
 
   private String message;

   public void init() throws ServletException {
      // Do required initialization
      message = "Hello World";
   }

   public void doGet(HttpServletRequest request, HttpServletResponse response)
      throws ServletException, IOException {
      
      // Set response content type
      response.setContentType("text/html");

      // Actual logic goes here.
      PrintWriter out = response.getWriter();
      out.println("<h1>" + message + "</h1>");
   }

   public void destroy() {
      // do nothing.
   }
}
```

### JSP
La tecnología de Java Server Pages está basada en combinar lenguajes de marcas con fragmentos en Java, al estilo de PHP o de ASP.NET. Además, permite crear clases que proporcionan marcas nuevas para el lenguaje de JSP.

Los bloques Java se delimitan con <% %>, el bloque <%= %> envia hacia la salida.
Se dispone de dos objetos: request y response, con la misma funcionalidad que en el servlet.

```
<html>
<head>
  <title>Echoing HTML Request Parameters</title>
</head>
<body>
  <h3>Choose an author:</h3>
  <form method="get">
    <input type="checkbox" name="author" value="Tan Ah Teck">Tan
    <input type="checkbox" name="author" value="Mohd Ali">Ali
    <input type="checkbox" name="author" value="Kumar">Kumar
    <input type="submit" value="Query">
  </form>
 
  <%
  String[] authors = request.getParameterValues("author");
  if (authors != null) {
  %>
    <h3>You have selected author(s):</h3>
    <ul>
  <%
      for (int i = 0; i < authors.length; ++i) {
  %>
        <li><%= authors[i] %></li>
  <%
      }
  %>
    </ul>
    <a href="<%= request.getRequestURI() %>">BACK</a>
  <%
  }
  %>
</body>
</html>
```

## Estructura de las aplicaciones Java
Las aplicaciones Web constan de varias partes que se organizan en varios directorios.  
* Directorio raíz de la aplicación Web: Ficheros HTML, JSP, CSS, JS, imágenes, etc. que son visibles a los clientes de la aplicación
* `/WEB-INF/web.xml`: Web Application Deployment Descriptor (descriptor de despliegue). Fichero XML que describe los servlets y otros componentes de la aplicación, además de parámetros de inicialización y restricciones de seguridad
* `/WEB-INF/classes/`: Clases Java y recursos asociados: Servlets y no servlets que no estén contenidos en ficheros JAR
* `/WEB-INF/lib/`: Ficheros JAR: Librerías de clases, drivers JDBC, etc.
 
Además, el servidor tiene una carpeta de librerías compartidas. 
 
* En el caso de Tomcat: `$CATALINA_HOME/lib` tiene disponibles librerias compartidas, y se pueden añadir más.
 
Ejemplo web.xml (Descriptor de despliegue)
```xml
<?xml version="1.0" encoding="ISO‐8859‐1"?>
<web‐app
	xmlns="http://java.sun.com/xml/ns/j2ee"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema‐instance" xsi:schemaLocation="http://java.sun.com/xml/ns/j2ee/web‐app_2_4.xsd"
 
version="2.4">
	<servlet>
		<servlet‐name>Nombre del Servlet</servlet‐name>
		<servlet‐class>es.ucm.cursoweb.MiServlet</servlet‐class>
		<init‐param>
			<param‐name>parametro</param‐name>
			<param‐value>valor</param‐value>
		</init‐param>
	</servlet>
	<servlet‐mapping>
		<servlet‐name>Nombre del Servlet</servlet‐name>
		<url‐pattern>/saluda</url‐pattern>
	</servlet‐mapping>
</web‐app>
```