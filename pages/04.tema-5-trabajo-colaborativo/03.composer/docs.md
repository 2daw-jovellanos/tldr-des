---
title: Composer
media_order: '1_T0mhMbVbXzdrcH6R9BuevQ[1].png'
taxonomy:
    category:
        - docs
visible: true
---

[TOC][Composer](https://getcomposer.org) es el gestor de dependencias vinculado a php. Su principal fuente es el repositorio [packagist](https://packagist.org/)  
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
* Tambien se pueden descargar dependencias que no sean del backend, sino del front, tales como frameworks de css (bootstrap, font-awesome, etc) o de javascript (jquery, etc)
* La carpeta vendor debería ser ignorada por git o cualquier otro <abbr title="source code manager">scm</abbr>. En el caso de git, añadirla a `.gitignore`
* Cuando se han instalado las dependencias, composer anota las versiones instaladas en un fichero llamado `composer.lock`.

## el formato de composer.json
El fichero describe un objeto json, con propiedades. Cada clave tiene su propia estructura. Hay muchas apartados que se pueden incluir como claves en el objeto de composer.json.  
Más: [esquema completo de composer.json](https://getcomposer.org/doc/04-schema.md)

#### name
Nombre del paquete (una cadena) en el formato _vendor/package_name_.
```json
   "name": "despliegue/ejemplo-composer",
```

#### description
Una breve descripción del proyecto (cadena)
```json
   "description": "Un proyecto de ejemplo para probar composer",
```
#### type
El tipo de proyecto que estamos haciendo. Cadena. Ej: `library`, `project`
```json
   "type": "project",
```
#### license
La [licencia](https://spdx.org/licenses/) del proyecto. Cadena.
```json   
   "license": "mit",
```

#### minimum-stability
Cadena. La estabilidad mínima que se requiere para las dependencias: `dev`, `alpha`, `beta`, `rc` o `stable`. ([Ver versiones](#versiones))
```json
"minimum-stability": "RC"
```

#### require
Un objeto, que contiene las dependencias el proyecto. Cada clave de este objeto es el idenficador de una dependencia en el formato `vendor/name`. Cada valor describe la versión aceptable para la dependencia. [(ver versiones)](#versiones)
```json
    "require": {
        "noahbuscher/macaw": "dev-master",
        "monolog/monolog": "^2.0"
    },
```

#### require-dev
La misma estructura que require, pero para dependencias que sólo son necesarias durante el desarrollo. Ej.: frameworks de pruebas, minificadores, transpiladores, etc.
```json
    "require-dev": {
        "phpunit/phpunit": "^8.1"
    },
```
#### authors
Un array con objetos que describen los autores del proyecto. Cada objeto tiene dos claves: `name` y `email`.
```json
    "authors": [
        {
            "name": "John Doe",
            "email": "john.doe@example.com"
        }
    ],
```

## versiones

En el sistema estándar de etiquetado de versiones se utilizan hasta tres números separados por puntos:
![Standard version system](1_T0mhMbVbXzdrcH6R9BuevQ%5B1%5D.png)
* La versión mayor cambia cuando hay modificaciones que rompen la compatibilidad
* La versión menor cambia cuando se introducen mejoras que no rompen la compatibilidad
* La versión de patch cambia cuando se hacen modificaciones que arreglan mal funcionamiento o problemas de seguridad.

Se puede añadir un sufijo que indica la **estabilidad** de la versión, seguido opcionalmente de un número. De menor a mayor estabilidad:
* `-dev` El proyecto está en desarrollo. Mínima fiabilidad.
* `-alpha` (`-a`) Inestable, pero se pueden probar funcionalidades, al menos de manera parcial.
* `-beta` (`-b`) Inestable, pero se supone que están todas las funcionalidades, y que se pueden realizar pruebas de aceptacion, estabilidad, rendimiento, etc.
* `-RC` Release candidate: Versión que se supone estable, y se realizan todas las pruebas necesarias antes de considerarla formalmente versión estable.
Ej: `1.2.9-alpha3`, `1.0-RC`

Hay muchas formas de especificar la versión de una dependencia en composer. Algunas de las más habituales:
* Exactamente. Ej: `1.0.3`: exactamente la versión etiquetada 1.0.3
* Con comparadores: `>=1.0` La 1.0 o cualquiera superior; `>=1.0 <2.0` Mayor o igual que 1.0 y menor que 2.0; `>=1.0 <1.1 || >=1.2 `mayor o igual que 1.0 y menor que 1.1 o mayor o igual que 1.2.
* Rango con guiones: `1.0 - 2.0` Cualquier versión entre 1.0 y 2.0 ambas inclusive. Se incluyen también todas las versiónes 2.0. Ej. 2.0.45 también estaría incluida.
* Virgulilla: permite que crezca el último numero especificado. Ej: `~1.5` A partir de la 1.5 y <2.0; Ej, `~1.5.22` A partir de la 1.5.22 y <1.6
* Acento circunflejo: Mantiene la compatibilidad de la versión mayor. Ej: `^1.2.4` permite todas las versiones partir de 1.2.4 y <2.0. (Excepción: en las versiones anteriores a la 1, es decir, si la versión mayor es 0, sólo permite que incremente el tercer número. Ej: `^0.3` permite versiones >=0.3.0 y <0.4.0. 
* Rama de scm: Se utiliza `dev-` seguido del nombre de la rama. Ej: `dev-master` es la rama master.

Más: [Versions and constraints](https://getcomposer.org/doc/articles/versions.md)

## comandos usuales

* **composer init** → Compone un composer.json básico interactivamente
* **composer install** → instala las dependencias especificadas en `composer.json`. Se tiene en cuenta el fichero `composer.lock`:
    * Si no existe, se descargan las últimas versiones de las dependencias que cumplan las restricciones de versión, y se anotan en composer.lock
    * Si existe, se comprueban las versiones anotadas composer.lock y si no están instaladas, se reinstalan, y también se instalan las dependencias nuevas que no estuvieran anotadas en composer.lock.  
El comando install no busca versiones actualizadas. Si tiene que reinstalar, instala las versiones anotadas en composer.lock. Compartir composer.lock con el equipo de desarrollo hace que se compartan las mismas versiones instaladas.
* **composer install --no-dev** → No instala las dependencias de desarrollo
* **composer require _vendor/name_** → añade una dependencia
* **composer require -dev _vendor/name_** → añade una dependencia de desarrollo
* **composer remove _vendor/name_** → Elimina una dependencia de desarrollo
* **composer update** → Busca y descarga actualizaciones de las dependencias. Anota las versiones actualizadas en composer.lock.

Más: [cli/commands](https://getcomposer.org/doc/03-cli.md)



