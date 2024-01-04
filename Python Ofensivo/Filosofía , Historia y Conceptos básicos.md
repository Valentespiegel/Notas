Python es un lenguaje de programación de alto nivel, interpretado y con una filosofía que enfatiza una sintaxis que favorece un código legible. Fue creado por Guido van Rossum y su lanzamiento inicial fue en 1991. Van Rossum modeló Python con la idea de superar las limitaciones del lenguaje ABC, buscando crear un lenguaje que pudiera hacer todo lo que ABC hacía, pero con una sintaxis clara que fuera fácil de aprender y de usar.

Desde su concepción, Python ha estado enfocado en el principio de legibilidad y simplicidad. Esto no solo hace que sea más fácil de aprender, sino que también permite a los programadores expresar conceptos complejos en menos líneas de código en comparación con otros lenguajes de programación.

Python se ha desarrollado bajo una licencia de código abierto, lo que significa que cualquiera puede contribuir al desarrollo del lenguaje. Esta filosofía colaborativa ha ayudado a Python a crecer y adaptarse rápidamente a las cambiantes necesidades de la industria de la tecnología.

Uno de los documentos más importantes en la comunidad de Python es el ‘**PEP 20**‘, conocido como “**El Zen de Python**“. Este documento contiene 19 aforismos que capturan la esencia de la filosofía de Python. Algunos ejemplos notables incluyen “Lo bello es mejor que lo feo”, “Explícito es mejor que implícito” y “Si la implementación es difícil de explicar, es una mala idea”.

La filosofía de Python también enfatiza la importancia de la eficiencia y la practicidad. Python se ha diseñado para ser altamente extensible, lo que permite a los programadores escribir nuevos módulos y extensiones en C o C++ para realizar operaciones críticas rápidamente.

En resumen, Python es más que un lenguaje de programación; es una comunidad y una filosofía de diseño que continúa guiando su desarrollo. Con su énfasis en la claridad, la colaboración y la eficiencia, Python se ha solidificado como uno de los lenguajes de programación más populares y queridos del mundo.

---
**Características Principales:**

- **Sintaxis simple y fácil de aprender**: Python es famoso por su legibilidad, lo que facilita el aprendizaje para los principiantes y permite a los desarrolladores expresar conceptos complejos en menos líneas de código que serían necesarias en otros lenguajes.
- **Interpretado**: Python es procesado en tiempo de ejecución por el intérprete. Puedes ejecutar el programa tan pronto como termines de escribir los comandos, sin necesidad de compilar.
- **Tipado dinámico**: Python sigue las variables en tiempo de ejecución, lo que significa que puedes cambiar el tipo de datos de una variable en tus programas.
- **Multiplataforma**: Python se puede ejecutar en una variedad de sistemas operativos como Windows, Linux y MacOS.
- **Bibliotecas extensas**: Python cuenta con una gran biblioteca estándar que está disponible sin cargo alguno para todos los usuarios.
- **Soporte para múltiples paradigmas de programación**: Python soporta varios estilos de programación, incluyendo programación orientada a objetos, imperativa y funcional.
```java
sudo su 
apt install python2
```
![[Pasted image 20240103092558.png]]
```java
apt install python3
```
![[Pasted image 20240103092623.png]]
```java
python2 --version
python3 --version
```
![[Pasted image 20240103092722.png]]

---
**Python 2 vs Python 3:**

- **Sintaxis de print**: En Python 2, ‘print’ es una declaración, mientras que en Python 3, ‘print()’ es una función, lo que requiere el uso de paréntesis.
- **División de enteros**: Python 2 realiza una división entera por defecto, mientras que Python 3 realiza una división real (flotante) por defecto.
- **Unicode**: Python 3 usa Unicode (texto) como tipo de dato por defecto para representar cadenas, mientras que Python 2 utiliza ASCII.
- **Librerías**: Muchas librerías populares de Python 2 han sido actualizadas o reescritas para Python 3, con mejoras y nuevas funcionalidades.
- **Soporte**: Python 2 llegó al final de su vida útil en 2020, lo que significa que ya no recibe actualizaciones, ni siquiera para correcciones de seguridad.
```java
python2
print "Hola"
```
![[Pasted image 20240103093005.png]]
```java
python3 
print ("Hola)
```
![[Pasted image 20240103093117.png]]
```java
python2
5/3
type(5/3)
sudo ```
![[Pasted image 20240103093325.png]]
```java
python3
5/3
1.6666666666667
type(5/3)
```
![[Pasted image 20240103093401.png]]

---
**PIP (Pip Installs Packages) PIP2 vs PIP3:**

- **Gestión de paquetes**: PIP2 y PIP3 son herramientas que permiten instalar paquetes para Python 2 y Python 3, respectivamente. Es importante usar la versión correcta para garantizar la compatibilidad con la versión de Python que estés utilizando.
- **Comandos de instalación**: El uso de pip o pip3 antes de un comando determina si el paquete se instalará en Python 2 o Python 3. Algunos sistemas operativos pueden requerir especificar pip2 o pip3 explícitamente para evitar ambigüedades.
- **Ambientes virtuales**: Es una buena práctica usar ambientes virtuales para mantener separadas las dependencias de proyectos específicos y evitar conflictos entre versiones de paquetes para Python 2 y Python 3.
```java
apt install python3-pip
```
![[Pasted image 20240103093923.png]]
```java
python
wget https://bootstrap.pypa.io/pip/2.7/get-pip.py
python2 get-pip.py
```
![[Pasted image 20240103094108.png]]
```java
pip3 install pwntools
```
![[Pasted image 20240103094239.png]]

**Ventajas de Usar Python:**

- **Productividad mejorada**: La simplicidad de Python aumenta la productividad de los desarrolladores ya que les permite enfocarse en resolver el problema en lugar de la complejidad del lenguaje.
- **Amplia comunidad**: Una comunidad grande y activa significa que es fácil encontrar ayuda, colaboración y contribuciones de terceros.
- **Aplicabilidad en múltiples dominios**: Python se utiliza en una variedad de aplicaciones, desde desarrollo web hasta inteligencia artificial, ciencia de datos y automatización.
- **Compatibilidad y colaboración**: Python se integra fácilmente con otros lenguajes y herramientas, y es una excelente opción para equipos de desarrollo colaborativos.
---
**El intérprete de Python**

El intérprete de Python es el corazón del lenguaje de programación Python; es el motor que ejecuta el código que escriben los programadores. Cuando hablamos del “**intérprete de Python**“, nos referimos al programa que lee y ejecuta el código Python en tiempo real.

**Funciones Clave del Intérprete de Python:**

- **Ejecución de Código**: El intérprete ejecuta el código escrito en Python línea por línea, lo que facilita la depuración y permite a los desarrolladores probar fragmentos de código de forma interactiva.
- **Modo Interactivo**: El intérprete puede usarse en un modo interactivo que permite a los usuarios ejecutar comandos de Python uno a uno y ver los resultados de inmediato, lo cual es excelente para el aprendizaje y la experimentación.
- **Modo de Script**: Además del modo interactivo, el intérprete puede ejecutar programas completos o scripts que se escriben en archivos con la extensión ‘**.py**‘.
- **Compilación a Bytecode**: Aunque Python es un lenguaje interpretado, internamente, el intérprete compila el código a bytecode antes de ejecutarlo, lo que mejora el rendimiento.
- **Máquina Virtual de Python**: El bytecode compilado se ejecuta en la Máquina Virtual de Python (Python Virtual Machine – PVM), que es una abstracción que hace que el código de Python sea portable y se pueda ejecutar en cualquier sistema operativo donde el intérprete esté disponible.

**Ventajas del Intérprete de Python:**

- **Facilidad de Uso**: La capacidad de ejecutar código inmediatamente y de manera interactiva hace de Python una herramienta excelente para principiantes y para el desarrollo rápido de aplicaciones.
- **Portabilidad**: El intérprete de Python está disponible en múltiples plataformas, lo que significa que los programas de Python pueden ejecutarse en casi cualquier sistema sin modificaciones.
- **Extensibilidad**: El intérprete de Python permite la extensión con módulos escritos en otros lenguajes como C o C++, lo que puede ser utilizado para optimizar el rendimiento.
```java
python3 
Todos_somos_Lamers = True
type(Todos_somos_Lamers)
if Todos_somos_Lamers:
	print("Esto es verdad como un templo")
```
![[Pasted image 20240103133423.png]]
```java
python3
Todos_somos_Lamers = False
type(Todos_somos_Lamers)
if Todos_somos_Lamers:
	print("Esto es verdad como un templo")
```
![[Pasted image 20240103133615.png]]
```java
python3 -c 'Todos_somos_lammers = True; print ("Esto es verdad como un templo") if Todos_somos_lammers else None'
```
![[Pasted image 20240103134005.png]]


```java
mkdir ~/.config/{bspwm,sxhkd}
```