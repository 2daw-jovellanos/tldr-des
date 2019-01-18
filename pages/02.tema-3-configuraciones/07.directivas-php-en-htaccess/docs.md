---
title: 'Directivas php en htaccess'
taxonomy:
    category:
        - docs
visible: true
---

Cuando se usa PHP como un módulo de Apache, se pueden usar directivas para cambiar sus valores de configuración, como con cualquier otro módulo en los ficheros de configuración de Apache y en los ficheros .htaccess si están activos. Es decir, utilizando directivas en formato apache se pueden cambiar los ajustes de configuración de php siempre que esté cargado como módulo. Se necesitarán los privilegios "AllowOverride Options" o "AllowOverride All" para poder hacerlo en .htaccess.

 * La directiva `php_value nombre valor` establece el valor de una propiedad de php. Ej: `php_value max_execution_time 300`
 * Para propiedades cuyo valor sea booleano (on u off) se utiliza `php_flag nombre on|off`. Por ejemplo: `php_flag display_errors on`

Más en [el manual de php](http://php.net/manual/es/configuration.changes.php)