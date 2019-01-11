---
title: 'Entorno de java y Máquinas virtuales de proceso.'
taxonomy:
    category:
        - docs
visible: true
---

[TOC]
### Máquinas virtuales de proceso.

Java es un lenguaje con un enfoque de máquina virtual de proceso (Al igual que C# o Visual Basic.NET). En el entorno de ejecución de aplicaciones web escritas en Java, C# o VB.NET el modo CGI o FastCGI no se suele utilizar, dado que hay que que compilar el código. La solución utilizada habitualmente es recurrir a servidores web escritos directamente en Java. Estos servidores son capaces de compilar y ejecutar el código.

## Java. Tecnología Java EE
Las aplicaciones web para java se enmarcan dentro de **Java EE: Enterprise Edition**. El api de **Java EE** añade clases y elementos que proporcionan funcionalidad adicional para las aplicaciones web y por supuesto, se tiene también disponible el api de **Java SE**. Las clases de java EE están disponibles en el interior del entorno de ejecución de los servidores web de Java, y no hace falta instalarlas. El JDK básico de Java SE tiene que estar instalado y dispobible en la máquina en la que se ejecuten servidores de java.

Las aplicaciones web de java tienen una estructura estándar, y los entornos de desarrollo como NetBeans o Eclipse suelen tener incorporado el Java EE, y son capaces de generar, ejecutar y depurar proyectos de Java Web. NetBeans está preparado para interoperar con el servidor GlassFish.

Los principales servidores son:
* [Apache Tomcat](http://tomcat.apache.org/) También conocido como **Catalina**. Uno de los preferidos para el desarrollo, de la fundación  Apache. Escrito en java, a diferencia del servidor Apache, escrito en C.
* [Oracle GlassFish](https://javaee.github.io/glassfish) Otro de los preferidos para el desarrollo. Open Source, esponsorizado por Oracle. Hay un fork open source llamado [Paraya Server](https://www.payara.fish/software/payara-server/) que va cobrando popularidad desde que Oracle no da soporte comercial a GlassFish.
* [IBM Websphere](https://www.ibm.com/es-es/marketplace/java-ee-runtime) Uno de los clásicos en entorno empresarial.
* [Red Hat WildFly](http://wildfly.org/) Otro clásico. Anteriormente conocido como **JBoss**.
* [Oracle Weblogic Server](https://www.oracle.com/es/middleware/weblogic/) El servidor empresarial de Oracle.

## Microsoft. Tecnología ASP.NET

El entorno de máquina virtual de microsoft se llama **.NET**. La tecnología de desarrollo web de .NET es **ASP.NET**, con dos lenguajes principales: C# y Visual Basic.NET. Abreviado como VB.NET.
El servidor **Internet Information Server (IIS)** es el servidor de microsoft que contiene la tecnología de **ASP.NET**, y es capaz de servir aplicaciones preparadas para esta plataforma.
* Puede instalarse en los sistemas windows, 
* El IDE **Visual Studio** incorpora una versión simplificada del servidor llamado **IIS Express**, que permite probar las aplicaciones durante el desarrollo.
* Si se necesita la tecnología ASP.NET en cloud, el principal proveedor es [Microsoft Azure](https://azure.microsoft.com/es-es/)

