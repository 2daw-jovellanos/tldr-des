---
title: 'Lenguajes de marcas para configuraciones'
taxonomy:
    category:
        - docs
visible: true
---

La configuración de servicios relacionados con el despliegue, así como la configuración de otras muchas herramientas de desarrollo suelen hacerse en ficheros de texto cuya estructura está basada en algún **Lenguaje de marcas** que sirva para intercambiar información.

Vamos a citar algunos:
[miniTOC]

## XML 
**Extended Markup Languaje** es el lenguaje de marcas oficial del w3c, y lo conocemos ampliamente porque es el que hemos estudiado con más profundidad en la asignatura de lenguaje de marcas.   

Se basa en: 
* **elementos**: contenidos estructurales, encerrados entre **etiquetas** de apertura y cierre. Un elemento puede contener otros elementos. 
* **atributos**: son valores asociados a un elemento.

>>> Se suele utilizar en algunas configuraciones. En particular, las relacionadas con el mundo de Java.
>>> **Apache Tomcat**, o el gestor de dependencias **maven** (del que hablaremos más adelante en el curso) usan XML para sus configuraciones.
>>>  También en algunas aplicaciones de Microsoft, como los ficheros de configuración de las aplicaciones de ASP.NET, aunque las herramientas más modernas de Microsoft tienden a utilizar JSON.

Ej: un fragmento de la configuración de **tomcat** (sólo para ver su aspecto)
```xml
<?xml version='1.0' encoding='utf-8'?>
<Server port="8005" shutdown="SHUTDOWN">
  <Listener className="org.apache.catalina.core.ThreadLocalLeakPreventionListener" />
 
  <GlobalNamingResources>
    <Resource name="UserDatabase" auth="Container"
              type="org.apache.catalina.UserDatabase"
              factory="org.apache.catalina.users.MemoryUserDatabaseFactory"
              pathname="conf/tomcat-users.xml" />
  </GlobalNamingResources>
 
  <Service name="Catalina">
    <Connector port="8080" protocol="HTTP/1.1"
               connectionTimeout="20000"
               redirectPort="8443" />
   <!--- etc, etc -->
   
```

Otro ejemplo: Un fragmento de código del descriptor de despliegue de una aplicación ASP.NET, igualmente sólo para ver su aspecto.
```xml
<configuration>

   <!-- Configuration section-handler declaration area. -->
      <configSections>
         <section name="section1" type="section1Handler" />
         <section name="section2" type="section2Handler" />
      </configSections>
   <!-- Configuration section settings area. -->
   
   <section1>
      <s1Setting1 attribute1="attr1" />
   </section1>
   
   <section2>
      <s2Setting1 attribute1="attr1" />
   </section2>
   
   <system.web>
      <authentication mode="Windows" />
   </system.web>
   
</configuration>
```

## Ficheros de directivas estilo UNIX
Tradicionalmente utilizados en servicios Unix, y heredados en Linux/Android/MacOS 

* Son ficheros con estructura posicional
* las líneas empiezan por un identificador llamado **directiva** que hace referencia a un determinado aspecto de la configuración. Cada directiva tiene su propio conjunto de valores, que se suele poner en la misma línea, a continuación de la directiva.  (Ej: `DefaultServer on`,  `ServerType standalone`)
* Habitualmente en sistemas GNU/linux y asimilados, los ficheros de configuración de directivas se guardan en alguna subcarpeta de  `/etc`
* Hay un caráter para escribir comentarios de una línea, a partir del cual se ignora la línea. Habitualmente es **#**   
* Los espacios entre la directiva y sus valores suelen ser ignorados. Mucha gente aprovecha esta característica para alinear los valores en columnas.

>>> Este tipo de ficheros se utilizan en **OpenSSH**, **proftpd**, **apache 2** y un larga lista más.

Ej: un fragmento de configuración de __proftpd__

```
# This is a basic ProFTPD configuration file (rename it to 
# 'proftpd.conf' for actual use.  It establishes a single server
# and a single anonymous login.  It assumes that you have a user/group
# "nobody" and "ftp" for normal operation and anon.

ServerName     "ProFTPD Default Installation"
ServerType     standalone
DefaultServer  on

# Port 21 is the standard FTP port.
Port           21

# Umask 022 is a good standard umask to prevent new dirs and files
# from being group and world writable.
Umask          022
```
### Secciones
En algunos ficheros de directivas estilo Unix, se utilizan marcas ente ángulos con una etiqueta para delimitar secciones. 
Ej: `<Directory /var/www/ejemplo>` y `</Directory>`. La marca de apertura va en una línea, la de cierre en otra. Tienen la misma etiqueta, solo que la marca de cierre la etiqueta va precedida de una barra `/`. Las directivas que queden en el interior se ven afectadas por la marca. **OJO: aunque la sintaxis se asemeja a la de los elementos de XML, esto no es XML**

```xml
# A basic anonymous configuration, no upload directories.  If you do not
# want anonymous users, simply delete this entire <Anonymous> section.
<Anonymous ~ftp>
  User				ftp
  Group				ftp

  # We want clients to be able to login with "anonymous" as well as "ftp"
  UserAlias			anonymous ftp

  # Limit the maximum number of anonymous logins
  MaxClients			10

  # We want 'welcome.msg' displayed at login, and '.message' displayed
  # in each newly chdired directory.
  DisplayLogin			welcome.msg
  DisplayFirstChdir		.message

  # Limit WRITE everywhere in the anonymous chroot
  <Limit WRITE>
    DenyAll
  </Limit>
</Anonymous>
```

## Ficheros de parámetros "ini" estilo Windows.
Tradicionalmente utilizados en las versiones de Windows de los años 90, se siguen usando en algunos contextos sencilos. El fichero  de configuración de **php**, llamado `php.ini` es un ejemplo de este formato.

* Son ficheros con estructura posicional. Suelen tener la extensión **.ini**
* las líneas empiezan por un identificador llamado **parámetr** que hace referencia a un determinado aspecto de la configuración. Cada parámetro tiene su propio conjunto de valores, que se suele poner en la misma línea, a continuación de la directiva detrás del signo **=**.  (Ej: `memory_limit = 32M`,  `track_errors = yes`)
* Hay un caráter para escribir comentarios de una línea, a partir del cual se ignora la línea **;**   
* Puede haber marcas de sección, simplemente el nombre de sección entre corchetes Ej: `[php]`

Ej. de código
```ini
[gd]
; Tell the jpeg decode to ignore warnings and try to create
; a gd image. The warning will then be displayed as notices
; disabled by default
gd.jpeg_ignore_warning = 0

[exif]
; Exif UNICODE user comments are handled as UCS-2BE/UCS-2LE and JIS as JIS.
exif.encode_unicode = ISO-8859-15
```

## JSON
* Es la abreviatura de **JavaScript Object Notation**, es el formato de serialización estándar de javascript, estádar del IETF y de ECMA.
* En un fichero de JSON, se define un único objeto, entre llaves `{ }`, o un array, entre corchetes `[ ]`, ambos con sus elementos separados por comas.
* Los objetos pueden tener atributos, que son identificadores asociados a valores. Los identificadores se escriben entre comillas dobles y tambié  los valores de tipo texto, pero no ls numéricos. Ej: `"nombre" : "arturo"` `"annoNacimiento" : 1989"`
* Los valores no tienen tipo definido y siempre van entre comillas, pero
   * Si el valor es, a su vez un **objeto**, entonces va entre llaves, con sus atributos dentro, igualmente en el formato de identificador y valor. `"mascota" : {"nombre" : "paquito", "edad": 2, "especie" : "periquito"}`
   * Si el valor es un **array**, entonces va entre corchetes con sus valores separados por comas. Ej: `"aficiones: ["correr", "leer", "ver el GH Dúo sin volumen"]
* No se admiten comentarios en un fichero JSON
* JSON suele escribirse indentado [estilo k&r](https://en.wikipedia.org/wiki/Indentation_style) cuando puede haber intervención humana, como en los ficheros de configuración. Si no es así, suele escribirse [minificado](https://en.wikipedia.org/wiki/Minification_(programming)).  


Ej: Un fichero JSON que define un objeto que representa a una persona con sus atributos. Las aficiones y las mascotas van en un array.

```json
{
  "nombre": "Pepe", 
  "apellidos": "Perez López", 
  "aficiones": ["correr", "leer", "ver el GH Dúo sin volumen"], 
  "mascotas" : [
      {"nombre" : "Ataúlfo", "edad": 2, "especie" : "periquito"},
      {"nombre" : "Membrilla", "edad": 3, "especie" : "gato"}
  ]
}
````

## YAML
YAML es un formato de serialización de datos basado en texto, en los que las indentaciones funcionan con separador, al estilo de Python. 

* Es un estándar del IETF, mucho más rico que JSON.
* En un fichero de YAML, habitualmenet con extensión .yml se definen parejas de atributos y valores o listas. 
* Los objetos pueden tener atributos, que son identificadores asociados a valores. Los identificadores se escriben tal cual y pueden contener espacios, pero no ls numéricos. Ej: `nombre : arturo` `"año de nacimiento" : 1989"`
* Los valores no tienen tipo definido
   * Si los valores se agrupan formando un objeto, a su vez un **objeto**, entonces van indentados 
   * Si el valor es un **array** o lista, entonces va entre corchetes con sus valores separados por comas. Ej: `"aficiones: ["correr", "leer", "ver el GH Dúo sin volumen"], pero ser recomienda que vayan cada uno en una línea, indentado y con un guión delante
* Puede haber comentarios, precedidos de `#`
* Para indentar se utilizan <span style="color:red">2 o 4 espacios. <strong>Nunca tabs</strong></span>.


```yaml

nombre: Pepe
apellidos: Perez López
# las aficiones son una lista
aficiones: [correr, leer, ver el GH Dúo sin volumen]
# Los colores favoritos también son una lista:
colores favoritos:
  - rojo
  - amarrillo
# Las mascotas también, pero una lista de objetos
mascotas:
  -
    nombre: Ataúlfo
    edad: 2
    especie: periquito
  -
    nombre: Membrilla
    edad: 3
    especie: gato

```

