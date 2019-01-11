---
title: 'Lenguajes de marcas para configuraciones'
taxonomy:
    category:
        - docs
visible: true
---

La configuración de servicios relacionados con el despliegue, así como la configuración de otras muchas herramientas de desarrollo suelen hacerse en ficheros de texto cuya estructura está basada en algún **Lenguaje de marcas**.

Vamos a citar algunos:
[miniTOC]

## XML 
**Extended Markup Languaje** es el lenguaje de marcas oficial del w3c, y lo conocemos ampliamente porque es el que hemos estudiado con más profundidad en la asignatura de lenguaje de marcas.   

Se basa en: 
* **elementos**: contenidos estructurales, encerrados entre **etiquetas** de apertura y cierre. Un elemento puede contener otros elementos. 
* **atributos**: son valores asociados a un elemento.

>> Se suele utilizar en algunas configuraciones. Ej, el servidor de apliaccions **Apache Tomcat**, o el gestor de dependencias **maven** usan XML para sus configuraciones.

Ej: un fragmento de la configuración de **tomcat**
```xml
<?xml version='1.0' encoding='utf-8'?>
<Server port="8005" shutdown="SHUTDOWN">
  <Listener className="org.apache.catalina.core.JasperListener" />
  <Listener className="org.apache.catalina.core.AprLifecycleListener" SSLEngine="on" />
  <Listener className="org.apache.catalina.core.JreMemoryLeakPreventionListener" />
  <Listener className="org.apache.catalina.mbeans.GlobalResourcesLifecycleListener" />
  <Listener className="org.apache.catalina.core.ThreadLocalLeakPreventionListener" />
 
  <GlobalNamingResources>
    <Resource name="UserDatabase" auth="Container"
              type="org.apache.catalina.UserDatabase"
              description="User database that can be updated and saved"
              factory="org.apache.catalina.users.MemoryUserDatabaseFactory"
              pathname="conf/tomcat-users.xml" />
  </GlobalNamingResources>
 
  <Service name="Catalina">
    <Connector port="8080" protocol="HTTP/1.1"
               connectionTimeout="20000"
               redirectPort="8443" />
    <Connector port="8009" protocol="AJP/1.3" redirectPort="8443" />
 
    <Engine name="Catalina" defaultHost="localhost">
 
      <Realm className="org.apache.catalina.realm.LockOutRealm">
        <Realm className="org.apache.catalina.realm.UserDatabaseRealm"
               resourceName="UserDatabase"/>
      </Realm>
 
      <Host name="localhost"  appBase="webapps"
            unpackWARs="true" autoDeploy="true">
        <Valve className="org.apache.catalina.valves.AccessLogValve" directory="logs"
               prefix="localhost_access_log." suffix=".txt"
               pattern="%h %l %u %t "%r" %s %b" />
      </Host>
    </Engine>
  </Service>
</Server>
```

## Ficheros de directivas estilo UNIX
Tradicionalmente utilizados en servicios Unix, y heredados en Linux/Android/MacOS 

* Son ficheros con estructura posicional *
* las líneas empiezan por un identificador llamado **directiva** que hace referencia a un determinado aspecto de la configuración. Cada directiva tiene su propio conjunto de valores, que se suele poner en la misma línea, a continuación de la directiva.  (Ej: `DefaultServer on`,  `ServerType standalone`)
* Habitualmente en sistemas GNU/linux y asimilados, los ficheros de configuración de directivas se guardan en alguna subcarpeta de  `/etc`
* Hay un caráter para escribir comentarios de una línea, a partir del cual se ignora la línea. Habitualmente es **#**   
* Los espacios entre la directiva y sus valores suelen ser ignorados. Mucha gente aprovecha esta característica para alinear los valores en columnas.

Este tipo de ficheros se utilizan en **OpenSSH**, **proftpd**, **apache 2** y un larga lista más.

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
En algunos ficheros de directivas estilo Unix, se utilizan marcas ente ángulos para delimitar secciones. 
Ej: `<Directory /var/www/ejemplo>` y `</Directory>`. La marca de apertura va en una línea, la de cierre en otra, y las directivas que queden en el interior se ven afectadas por la marca. **OJO: aunque la sintaxis se asemeja a la de los elementos de XML, esto no es XML**

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

## Ficheros de directivas "ini" estilo Windows.
Tradicionalmente utilizados en las versiones de Windows de los años 90, se siguen usando en algunos contextos sencilos. El fichero  de configuración de **php**, llamado `php.ini` es un ejemplo de este formato.

* Son ficheros con estructura posicional. Suelen tener la extensión **.ini**
* las líneas empiezan por un identificador llamado **directiva** que hace referencia a un determinado aspecto de la configuración. Cada directiva tiene su propio conjunto de valores, que se suele poner en la misma línea, a continuación de la directiva detrás del signo **=**.  (Ej: `memory_limit = 32M`,  `track_errors = yes`)
* Hay un caráter para escribir comentarios de una línea, a partir del cual se ignora la línea **;**   
* Puede haber marcas de sección, simplemente el nombre de sección entre corchetes Ej: `[php]`

Ej. de código
```
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
* Es la abreviatura de **JavaScript Object Notation**, es el formato de serialización estándar de javascript.
* Hay identificadores asociados a valores. Tanto los valores como los identificadores van entre comillas dobles. Ej: `"nombre" : "arturo"`. 
* Los valores pueden ser de cualquier tipo, pero:

```json
{
    "menu": {
        "id": "file",
        "value": "File",
        "popup": {
            "menuitem": [
                {
                    "value": "New", "onclick": "CreateNewDoc()"
                },{
                    "value": "Open", "onclick": "OpenDoc()"
                },{
                    "value": "Close", "onclick": "CloseDoc()"
                }
            ]
        }
    }
}
```

## YAML
YAML es un formato de serialización de datos basado en texto, en los que las indentaciones funcionan con separador, al estilo de Python.

```yaml
nombre: pepe
apellidos:
   - perez
   - lopez
aficiones: [leer, correr]
notas:
   programacion: 5
   lenguajes de marcas: 3
```

```json
{
  "nombre": "pepe", 
  "apellidos": ["perez", "lopez"], 
  "aficiones": ["leer", "correr"], 
  "notas": {
    "programacion": 5, 
    "lenguajes de marcas": 3
  }
}
```