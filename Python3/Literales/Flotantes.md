Ahora es tiempo de hablar acerca de otro tipo, el cual esta designado para representar y almacenar los números que (como lo diría un matemático) tienen una **parte decimal no vacía**.

Son números que tienen (o pueden tener) una parte fraccionaria después del punto decimal, y aunque esta definición es muy pobre, es suficiente para lo que se desea discutir.

Cuando se usan términos como _dos y medio_ o _menos cero punto cuatro_, pensamos en números que la computadora considera como números **punto-flotante**:
 
		 `2.5                                -0.4`

Nota: _dos punto cinco_ se ve normal cuando se escribe en un programa, sin embargo si tu idioma nativo prefiere el uso de una coma en lugar de un punto, se debe asegurar que **el número no contenga comas**.

Python no lo aceptará, o (en casos poco probables) puede malinterpretar el número, debido a que la coma tiene su propio significado en Python.

Si se quiere utilizar solo el valor de dos punto cinco, se debe escribir como se mostró anteriormente. Nota que: hay un punto entre el _2_ y el _5_, no una coma.

Como puedes imaginar, el valor de **cero punto cuatro** puede ser escrito en Python como:

0.4  

Pero no hay que olvidar esta sencilla regla - se puede omitir el cero cuando es el único dígito antes del punto decimal.

En esencia, el valor 0.4 se puede escribir como:

.4  

Por ejemplo: el valor de 4.0 puede ser escrito como:

4.  

Esto no cambiará su tipo ni su valor.

### Enteros vs Flotantes

El punto decimal es esencialmente importante para reconocer números punto-flotantes en Python.

Observa estos dos números:

      `4                                4.0`
      
Se puede pensar que son idénticos, pero Python los ve de una manera completamente distinta.

4 es un número **entero** mientras que 4.0 es un número **punto-flotante**.

El punto decimal es lo que determina si es flotante.

Por otro lado, no solo el punto hace que un número sea flotante. Se puede utilizar la letra `e`.

Cuando se desea utilizar números que son muy pequeños o muy grandes, se puede implementar la **notación científica**.

Por ejemplo, la velocidad de la luz, expresada en _metros por segundo_. Escrita directamente se vería de la siguiente manera: `300000000`.

Para evitar escribir tantos ceros, los libros de texto emplean la forma abreviada, la cual probablemente hayas visto: `3 x 108`.

Se lee: tres por diez elevado a la octava potencia.

En Python, el mismo efecto puede ser logrado de una manera similar - observa lo siguiente:

`3E8`  

La letra `E` (también se puede utilizar la letra minúscula `e` - proviene de la palabra **exponente**) la cual significa _por diez a la n potencia_.

Nota:

- El **exponente** (el valor después de la _E_) debe ser un valor entero;
- La **base** (el valor antes de la _E_) puede ser un valor entero o flotante.

### Codificando Flotantes

Veamos ahora como almacenar números que son muy pequeños (en el sentido de que están muy cerca del cero).

Una constante de física denominada _La Constante de Planck_ (denotada como _h_), de acuerdo con los libros de texto, tiene un valor de: **6.62607 x 10-34**.

Si se quisiera utilizar en un programa, se debería escribir de la siguiente manera:

6.62607E-34  

Nota: el hecho de que se haya escogido una de las posibles formas de codificación de un valor flotante no significa que Python lo presentará de la misma manera.

Python podría en ocasiones elegir una **notación diferente**.

Por ejemplo, supongamos que se ha elegido utilizar la siguiente notación:

0.0000000000000000000001  

Cuando se corre en Python:

      `print(0.0000000000000000000001)`

este es el resultado:

      `1e-22`

Python siempre elige **la presentación más corta del número**, y esto se debe de tomar en consideración al crear literales.

