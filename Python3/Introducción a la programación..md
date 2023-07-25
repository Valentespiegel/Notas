
### Cómo funciona un programa de computadora?

Las computadoras pueden realizar tareas muy complejas, pero esta habilidad no es innata. La naturaleza de una computadora es bastante diferente.
Solo puede ejecutar operaciones extremadamente simples. Por ejemplo, una computadora no puede comprender el valor de una función matemática complicada por sí misma, aunque esto no está fuera del alcance de la posibilidad en un futuro cercano.
Las computadoras contemporáneas solo pueden evaluar los resultados de operaciones muy fundamentales. , como sumar o dividir, pero pueden hacerlo muy rápido y pueden repetir estas acciones prácticamente cualquier cantidad de veces.

Imagina que quieres saber la velocidad media que has alcanzado durante un viaje largo. Conoces la distancia, conoces el tiempo, necesitas la velocidad.,
Naturalmente, la computadora podrá calcular esto, pero la computadora no es consciente de cosas como la distancia, la velocidad o el tiempo. Por lo tanto, es necesario instruir a la computadora para:

    aceptar un número que represente la distancia;
    aceptar un número que represente el tiempo de viaje;
    divide el valor anterior por el segundo y almacenar el resultado en la memoria;
    mostrar el resultado (que representa la velocidad promedio) en un formato legible.

Estas cuatro simples acciones forman un programa. Por supuesto, estos ejemplos no están formalizados y están muy lejos de lo que la computadora puede entender, pero son lo suficientemente buenos para ser traducidos a un idioma que la computadora pueda aceptar.

---
### Lenguajes naturales vs lenguajes de programación.

Un lenguaje es un medio (y una herramienta) para expresar y registrar pensamientos. Hay muchos lenguajes a nuestro alrededor. Algunos de ellos no requieren ni hablar ni escribir, como el lenguaje corporal; es posible expresar tus sentimientos más profundos muy precisamente sin decir una palabra., Otro lenguaje que utilizas cada día es tu lengua materna, que utilizas para manifestar tu voluntad y reflexionar sobre la realidad. Las computadoras también tienen su propio lenguaje, llamado lenguaje **máquina**, que es muy rudimentario.

==Alfabeto.

un conjunto de símbolos utilizados para formar palabras de un determinado lenguaje (por ejemplo, el alfabeto latino para el inglés, el alfabeto cirílico para el ruso, el kanji para el japonés, y así sucesivamente)

==Lexico.

(también conocido como diccionario) un conjunto de palabras que el lenguaje ofrece a sus usuarios (por ejemplo, la palabra "computadora" proviene del diccionario en inglés, mientras que "cmoptrue" no; la palabra "chat" está presente en los diccionarios de inglés y francés, pero sus significados son diferentes)

==Sintaxts.

un conjunto de reglas (formales o informales, escritas o interpretadas intuitivamente) utilizadas para precisar si una determinada cadena de palabras forma una oración válida (por ejemplo, "Soy una serpiente" es una frase sintácticamente correcta, mientras que "Yo serpiente soy una" no lo es)

==Semantica.

un conjunto de reglas que determinan si una frase tiene sentido (por ejemplo, "Me comí una dona" tiene sentido, pero "Una dona me comió" no lo tiene)

---
### Lenguaje máquina vs. lenguaje de alto nivel

Necesitamos un lenguaje en el que los humanos puedan escribir sus programas y un lenguaje que las computadoras pueden usar para ejecutar los programas, uno que es mucho más complejo que el lenguaje de máquina y, sin embargo, mucho más simple que el lenguaje natural., Estos lenguajes a menudo se denominan lenguajes de programación de alto nivel. Son al menos algo similares a los naturales en que usan símbolos, palabras y convenciones legibles para los humanos. Estos lenguajes permiten a los humanos expresar comandos a las computadoras que son mucho más complejos que los que ofrecen las IL.
Un programa escrito en un lenguaje de programación de alto nivel se denomina **código fuente** ( en contraste con el código máquina ejecutado por las computadoras). Del mismo modo, el archivo que contiene el código fuente se denomina **archivo fuente**.

---

### Compilación vs. Interpretación

La programación informática es el acto de componer los elementos del lenguaje de programación seleccionado en el orden que provocará el efecto deseado. El efecto podría ser diferente en cada caso específico – depende de la imaginación, el conocimiento y la experiencia del programador.

Por supuesto, dicha composición tiene que ser correcta en muchos sentidos:

- **alfabéticamente** – un programa debe estar escrito en un alfabeto reconocible, como romano, cirílico, etc.
- **léxicamente** – cada lenguaje de programación tiene su diccionario y hay que dominarlo; afortunadamente, es mucho más simple y pequeño que el diccionario de cualquier idioma natural;
- **sintácticamente** – cada idioma tiene sus reglas y hay que obedecerlas;
- **semánticamente** – el programa tiene que tener sentido.

==**Compilación** - el programa fuente se traduce una vez (sin embargo, este acto debe repetirse cada vez que se modifique el código fuente) al obtener un archivo (por ejemplo, un _.exe_ si el código está destinado a ejecutarse en MS Windows) que contiene el código máquina. Ahora se puede distribuir el archivo en todo el mundo; el programa que realiza esta traducción se llama **compilador** o **traductor**.

ventajas

- la ejecución del código traducido suele ser más rápida;
- solo el usuario debe tener el compilador; el usuario final puede usar el código sin él;
- el código traducido se almacena usando lenguaje máquina; como es muy difícil de entender, es probable que tus propios inventos y trucos de programación sigan siendo tu secreto

Desventajas.

- la compilación en sí puede ser un proceso que consume mucho tiempo; es posible que no puedas ejecutar su código inmediatamente después de realizar una modificación;
- debes tener tantos compiladores como plataformas de hardware donde desees que se ejecute tu código.

==**Interpretación** - tú o cualquier usuario del código puede traducir el programa fuente cada vez que se debe ejecutar. El programa que realiza este tipo de transformación se denomina **intérprete**, ya que interpreta el código cada vez que se pretende ejecutar. También significa que no puedes simplemente distribuir el código fuente tal cual, porque el usuario final también necesita el intérprete para ejecutarlo.

Ventajas.

- puedes ejecutar el código tan pronto como lo completes; no hay fases adicionales de traducción;
- El código se almacena usando un lenguaje de programación, no un lenguaje máquina; esto significa que se puede ejecutar en computadoras que usan diferentes lenguajes máquina; no compila tu código por separado para cada arquitectura diferente.

Desventajas
- no esperes que la interpretación acelere tu código a alta velocidad: tu código compartirá el poder de la computadora con el intérprete, por lo que no puede ser realmente rápido;
- tanto tu como el usuario final deben tener el intérprete para ejecutar tu código.