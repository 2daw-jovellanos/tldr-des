---
title: Composer
media_order: 'wheelbarrel-with-tilde-caret-white-bg-w1000[1].jpg'
taxonomy:
    category:
        - docs
visible: true
---

>>>> En proceso de redacción


[Composer](https://getcomposer.org) es el gestor de dependencias vinculado a php. Su principal fuente es el repositorio [packagist](https://packagist.org/)
Mas: [documentación de composer](https://getcomposer.org/doc/)

* Cada proyecto que use composer debe tener un fichero llamado `composer.json` que describe el proyecto y sus dependencias en la raíz de la carpeta del proyecto.
* Composer descargará las dependencias en una carpeta llamada  `vendor`.
* Si las dependencias son librerias de php, composer creará un fichero llamado `vendor/autoload.php`, que al incluirlo carga los autoload de todas las dependencias.
> [Autoload](https://developer.hyvor.com/php/autoload-classes-namespaces) es una característica de php5 y posteriores, para simplificar los includes y requires al utilizar clases.
> Si se utiliza una clase de código no incluido o requerido, se permite definir una o más funciónes que sean retrollamadas cuando se detecta esa situación y
> localicen el código de la clase y lo carguen, en lugar de terminar generando una excepción
Hay dos tipos de dependencias:
    * dependencias (a secas): son necesarias para el despliegue del proyecto y su explotación
    * dependencias de desarrollo (**devdependencies**): son necesarias solo para desarrolladores: suelen ser herramientas, tales como librerias de test, transpiladores, minificadores y similares.
* Tambien se pueden descargar dependencias que no sean del backend, sino del front, tales como frameworks de css (bootstrap, font-awesome etc) o de javascript (jquery, etc)
* La carpeta vendor debería ser ignorada por git o cualquier otro <abbr title="source code manager">scm</abbr>. En el caso de git, añadirla a `.gitignore`

## el formato de composer.json
El fichero describe un objeto json, con propiedades. Cada propiedad tiene su propia estructura. Hay muchas apartados que se pueden incluir en composer.json. [esquema completo de composer.json](https://getcomposer.org/doc/04-schema.md)

#### name
Nombre del paquete, cadena, en el formato `vendor/package_name`
```json
   "name": "despliegue/ejemplo-composer",
```

#### description
Una breve descripción del proyecto, cadena.
```json
   "description": "Un proyecto de ejemplo para probar composer",
```
#### type
El tipo de proyecto que estamos haciendo. Cadena. Ej: `library`, `project`
```json
   "type": "library, project",
```
#### license
La [licencia](https://spdx.org/licenses/) del proyecto. Cadena.
```json   
   "license": "mit",
```

#### minimum-stability
Cadena. La estabilidad mínima que se requiere para las dependencias: `dev`, `alpha`, `beta`, `rc` o `stable`.
```json
"minimum-stability": "RC"
```

#### require
Un objeto, que contiene las dependencias el proyecto. Cada clave de este objeto es el idenficador de una dependencia en el formato `vendor/name`

#### version
La versión en la que se encuentra el proyecto. En el sistema estándar de versiones se utilizan hasta tres números separados por puntos.
![Standard version system](wheelbarrel-with-tilde-caret-white-bg-w1000%5B1%5D.jpg)
Se puede añadir un sufijo que indica la **estabilidad** de la versión, seguido opcionalmente de un número. De menor a mayor estabilidad:
* `-dev` El proyecto está en desarrollo. Mínima fiabilidad.
* `-patch` (`-p`) El proyecto está en proceso de solventar problemas fundamentales de estabildad, funcionalidad o seguridad.
* `-alpha` (`-a`) Inestable, pero se pueden probar funcionalidades, al menos de manera parcial.
* `-beta` (`-b`) Inestable, pero se supone que están todas las funcionalidades, y que se pueden realizar pruebas de aceptacion, estabilidad, rendimiento, etc.
* `-RC` Release candidate: Versión que se supone estable, y se realizan todas las pruebas necesarias antes de considerarla formalmente versión estable.
Ej: `1.2.9-alpha3`, `1.0-RC`
