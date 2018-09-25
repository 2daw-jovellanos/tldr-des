---
title: 'Lenguajes de programación.'
taxonomy:
    category: docs
visible: true
---

## Generaciones

   Según el momento histórico en el que surgieron se suele clasificar a los lenguajes en distintas generaciones. 

   * **Primera generación**: Los primeros lenguajes de programación utilizaban secuencias binarias para representar
     cada una de las operaciones de un programa. Cada procesador (CPU) tiene un lenguaje binario específico, el **código máquina**.
     En los primeros ordenadores, los programas se realizaban directamente en código máquina, así que los consideramos
     lenguajes de primera generación. Hoy en día, los procesadores sólo entienden el código máquina, pero no lo programamos directamente.
   * **Segunda generación**: Lenguajes _simbólicos_, en especial los lenguajes **ensambladores**. En ellos se utiliza una palabra para
     representar una operación simple del procesador. Un programa traductor del lenguaje ensamblador traduce cada símbolo a su
     correspondiente secuencia binaria en código máquina.
   * **Tercera generación**: Lenguajes de alto nivel, concebidos para tener una mayor expresión conceptual. En ellos se permite la
     utilización de instrucciones complejas que son traducidas a grandes secuencias de código máquina. Son de esta generación los
     lenguajes de programación utilizados hoy día (Java, C#, Visual Basic.net, Python, php, ruby, javascript, etc.) y otros que tuvieron
     su pico de importancia hace años (C, Pascal, Fortran, Cobol, etc.)
     
     Aunque esta clasificación se suele citar en los cursos introductorios de programación, carece de importancia y cada vez se utiliza menos,
     siendo más descriptiva la clasificación de los lenguajes por **paradigmas**.
     
## Paradigmas
Un paradigma de programación representa un enfoque particular de las características esenciales de un lenguaje de programación.
Hay varios paradigmas. Entre los más comunes:
   * **Imperativo**: El lenguaje se basa en instrucciones que directamente suponen órdenes que el ordenador debe ejecutar.
   * **Orientado a objetos (O.O.)**: el lenguaje dispone estructuras organizativas llamadas objetos, en las que se agrupan datos y algoritmos, y    
     estos objetos son parte fundamental en la construcción de las aplicaciones y programas.
   * **Funcional**: el lenguaje dispone del concepto de _función_, con un sentido similar a como se utiliza en matemáticas, y estas funciones
     son elementos importantes o fundamentales en la construcción de los programas.
     
### Algunos ejemplos:
|Lenguaje|Paradigma|
|--------|---------|
|C       |Imperativo|
|Java, C#, C++ | Imperativo y O.O.|
|F#, Haskell |  Funcional|
|Scala | O.O y funcional|
|Javascript | Imperativo, O.O. y algo de funcional|

## Proceso de traducción
Según como se traduzcan las instrucciones del lenguaje de 3ª generación y se ejecuten se suelen clasificar los lenguajes como

* **Interpretados**: El código fuente va siendo leido línea a línea por un **intérprete**, que comprueba la sintaxis de una instrucción, y si
  es correcta, la ejecuta inmediatamente. No se produce un ejecutable. El programa es traducido cada vez que se ejecuta.
  Ej: Python, php, ruby, javascript son lenguajes habitualmente interpretados.
* **Compilados**: El código fuente se lee por un **compilador**, que comprueba la sintaxis de una instrucción y si es correcta, va
  realizando una traducción a código máquina que va guardando en un _fichero ejecutable_. El fichero ejecutable es un programa
  que puede ser ejecutado por el sistema operativo.
  Ej: C, C++ son lenguajes habitualmente compilados.
* **Máquina virtual de proceso**: Este enfoque aprovecha las ventajas de los dos anteriores:  
  El código fuente se lee por un **compilador**, que comprueba la sintaxis de una instrucción y si es correcta, va
  realizando una traducción a código máquina de un procesador virtual, que va guardando en un _fichero ejecutable, pero de código intermedio_ 
  (también llamado _bytecode_). Es un ejecutable, pero no dirigido directamente a la CPU, sino a un _intérprete_.  
  El ejecutable de _código intermedio_, ya libre de errores sintácticos y mucho más compacto que el fuente es _interpretado_ por un 
  intérprete.  
  Ej: Java de Oracle, Scala, Java para Android, Kotlin para Android, C# o Visual Basic.net son lenguajes con enfoque de máquina virtual.  
   
|Enfoque| Ventajas | Inconvenientes|
|-------|----------|---------------|
|Interpretado| Portable, sencillo | Lento. Hay que traducir en cada ejecución |
|Compilado | Rápido. Aprovechamiento de la plataforma | No portable. Dirigido a una máquina.<br>Un mal comportamiento afecta a la estabilidad de la máquina|
|Máquina virtual | Portable, bastante rápido | No tan rápido como los compilados, no tan sencillo como los interpretados|

