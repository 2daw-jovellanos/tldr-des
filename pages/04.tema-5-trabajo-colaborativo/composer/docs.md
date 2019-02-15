---
title: Composer
taxonomy:
    category:
        - docs
visible: true
---

[Composer](https://getcomposer.org) es el gestor de dependencias vinculado a php. Su principal fuente es el repositorio [packagist](https://packagist.org/)
Mas: [documentación de composer](https://getcomposer.org/doc/)

* Cada proyecto que use composer debe tener un fichero llamado `composer.json` que describe el proyecto y sus dependencias.
* Composer descargará las dependencias en una carpeta llamada  `vendor`.
* Si las dependencias son librerias de php, composer creará un fichero llamado `vendor/autoload.php`, que al incluirlo carga los autoload de todas las dependencias.
> Autoload es una característica de php5 y posteriores, para simplificar los includes y requires al utilizar clases.
> Si se utiliza una clase de código no incluido o requerido, se permite definir una o más funciónes que sean retrollamadas cuando se detecta esa situación y
> localicen el código de la clase y lo carguen, en lugar de terminar generando una excepción
Hay dos tipos de dependencias:
    * dependencias (a secas): son necesarias para el despliegue del proyecto y su explotación
    * dependencias de desarrollo (**devdependencies**): son necesarias solo para desarrolladores: suelen ser herramientas, tales como librerias de test, transpiladores, minificadores y similares.
* Tambien se pueden descargar dependencias que no sean del backend, sino del front, tales como frameworks de css (bootstrap, font-awesome etc) o de javascript (jquery, etc)

## el formato de composer.json
El fichero describe un objeto json, con propiedades. Cada propiedad tiene su propia estructura. Hay muchas apartados que se pueden incluir en composer.json. [esquema completo de composer.json](https://getcomposer.org/doc/04-schema.md)

#### name
Nombre del paquete, cadena, en el formato `vendor/package_name`
#### description
Una breve descripción del proyecto, cadena.
#### version
La versión en la que se encuentra el proyecto. 
