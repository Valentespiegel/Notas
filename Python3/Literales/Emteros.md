[[Python]]
Quizá ya sepas un poco acerca de como las computadoras hacen cálculos con números. Tal vez has escuchado del **sistema binario**, y como es que ese es el sistema que las computadoras utilizan para almacenar números y como es que pueden realizar cualquier tipo de operaciones con ellos.

No exploraremos las complejidades de los sistemas numéricos posicionales, pero se puede afirmar que todos los números manejados por las computadoras modernas son de dos tipos:

- **enteros**, es decir, aquellos que no tienen una parte fraccionaria,
- y números **punto-flotantes** (o simplemente **flotantes**), los cuales contienen (o son capaces de contener) una parte fraccionaría.

La característica del valor numérico que determina el tipo, rango y aplicación se denomina el **tipo**.

Tomemos por ejemplo, el número _once millones ciento once mil ciento once_. Si tomaras ahorita un lápiz en tu mano, escribirías el siguiente número: `11,111,111`, o así: `11.111.111`, incluso de esta manera: `11 111 111`.

Es claro que la separación hace que sea más fácil de leer, especialmente cuando el número tiene demasiados dígitos. Sin embargo, Python no acepta estas cosas, está **prohibido**. ¿Qué es lo que Python permite?. El uso de **guion bajo** en los literales numéricos.*

Por lo tanto, el número se puede escribir ya sea así: `11111111`, o como sigue: `11_111_111`.

  **Nota**     *Python 3.6 ha introducido el guion bajo en los literales numéricos, permitiendo colocar un guion bajo entre dígitos y después de especificadores de base para mejorar la legibilidad. Esta característica no está disponible en versiones anteriores de Python.

¿Cómo se codifican los números negativos en Python? Como normalmente se hace, agregando un signo de **menos**. Se puede escribir: `-11111111`, o `-11_111_111`.

Los números positivos no requieren un signo positivo antepuesto, pero es permitido, si se desea hacer. Las siguientes líneas describen el mismo número: `+11111111` y `11111111`.

### Números octales y hexadecimales

Existen dos convenciones adicionales en Python que no son conocidas en el mundo de las matemáticas. El primero nos permite utilizar un número en su representación **octal**.

Si un número entero esta precedido por un código 0O o 0o (cero-o), el número será tratado como un valor octal. Esto significa que el número debe contener dígitos en el rango del [0..7] únicamente.

0o123 es un número **octal** con un valor (decimal) igual a 83.

La segunda convención nos permite utilizar números en **hexadecimal**. Dichos números deben ser precedidos por el prefijo 0x o 0X (cero-x).

![[Pasted image 20230724161123.png]]

