	La palabra _**print**_ que puedes ver aquí es el **nombre de una función**. Eso no significa que dondequiera que aparezca esta palabra, será siempre el nombre de una función. El significado de la palabra proviene del contexto en el cual se haya utilizado la palabra.
Probablemente hayas encontrado el término función muchas veces antes, durante las clases de matemáticas. Probablemente también puedes recordar varios nombres de funciones matemáticas, como seno o logaritmo.
Las funciones de Python, sin embargo, son más flexibles y pueden contener más que sus parientes matemáticos.
Una función (en este contexto) es una parte separada del código de computadora el cual es capaz de:

- **causar algún efecto** (por ejemplo, enviar texto a la terminal, crear un archivo, dibujar una imagen, reproducir un sonido, etc.); esto es algo completamente inaudito en el mundo de las matemáticas.
- **evaluar un valor** (por ejemplo, la raíz cuadrada de un valor o la longitud de un texto dado) y **devolverlo como el resultado de la función**; esto es lo que hace que las funciones de Python sean parientes de los conceptos matemáticos.

Pueden venir **de Python mismo**. La función print es una de este tipo; dicha función es un valor agregado de Python junto con su entorno (está **integrada**); no tienes que hacer nada especial (por ejemplo, pedirle a alguien algo) si quieres usarla;

Pueden provenir de uno o varios de los **módulos**; de Python llamados complementos algunos de los módulos vienen con Python, otros pueden requerir una instalación por separado - cual sea el caso, todos deben estar conectados explícitamente con el código (te mostraremos cómo hacer esto pronto);

Puedes **escribirlas tú mismo**, colocando tantas funciones como desees y necesites dentro de su programa para hacerlo más simple, claro y elegante.

### **1. ¿Qué efecto tiene la función** print()?

El efecto es muy útil y muy espectacular. La función:

- toma sus argumentos (puede aceptar más de un argumento y también puede aceptar menos de un argumento)
- los convierte a un formato legible si es necesario (como puedes sospechar, las cadenas no requieren esta acción, ya que la cadena ya es legible)
- y **envía los datos resultantes al dispositivo de salida** (normalmente la consola); en otras palabras, todo lo que pongas en la función print() se aparecerá en tu pantalla.

No es de extrañar entonces que, de ahora en adelante, utilices print() muy intensamente para ver los resultados de sus operaciones y evaluaciones.

---

==Code

print("La Witsi Witsi Araña subió a su telaraña.")
print()
print("Vino la lluvia y se la llevó.")


==Console

La Witsi Witsi Araña subió a su telaraña.

Vino la lluvia y se la llevo.

---

==Code

print("La Witsi Witsi Araña\nsubió a su telaraña.")
print()
print("Vino la lluvia\ny se la llevó.")

==Console

La Witsi Witsi Araña
subió a su telaraña.

Vino la lluvia
y se la llevo.

---

==Code

print("Mi nombre es", "Python.", end=" ")
print("Monty Python.")

==Console 

Mi nombre es Python. Monty Python.

---

==Code

print("Mi", "nombre", "es", "Monty", "Python.", sep="-")

==Console

Mi-nombre-es-Monty-Python.

---

==code

print("Programming","Essentials","in", sep="***", end="...")
print("Python")

==Console

Programming***Essentials***in...Python

---

==Code

Sample Solution

###################
print("original version:")
###################
print("    *")
print("   * *")
print("  *   *")
print(" *     *")
print("***   ***")
print("  *   *")
print("  *   *")
print("  *****")
###################
print("with fewer 'print()' invocations:")
###################
print("    *\n   * *\n  *   *\n *     *\n***   ***")
print("  *   *\n  *   *\n  *****")
###################
print("higher:")
###################
print("        *")
print("       * *")
print("      *   *")
print("     *     *")
print("    *       *")
print("   *         *")
print("  *           *")
print(" *             *")
print("******     ******")
print("     *     *")
print("     *     *")
print("     *     *")
print("     *     *")
print("     *     *")
print("     *     *")
print("     *******")
###################
print("doubled:")
###################
print("        *        "*2)
print("       * *       "*2)
print("      *   *      "*2)
print("     *     *     "*2)
print("    *       *    "*2)
print("   *         *   "*2)
print("  *           *  "*2)
print(" *             * "*2)
print("******     ******"*2)
print("     *     *     "*2)
print("     *     *     "*2)
print("     *     *     "*2)
print("     *     *     "*2)
print("     *     *     "*2)
print("     *     *     "*2)
print("     *******     "*2)

print("Programming", "Essentials", "in", "Python", sep="***", end="...")