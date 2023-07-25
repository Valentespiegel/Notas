## Sincronización con el directorio activo.

La consola esta diseñada para que , si el servidor donde instalemos ESET Protect esta unido a algún dominio, automáticamente el ESET Protect va a sincronizarse con el Directorio activo.
Por lo tanto dentro de las pestaña Equipos de vera replicada toda la estructura organizacional del Directorio Activo junto a los equipos registrados que contenga.

==Es recomendable verificar si esos equipos registrados en el Directorio Activo existen existen realmente, y que no haya equipos que estén conectados a la red sin estar registrados.

En caso de que el servidor en donde esta instalado ESET Protect no pertenezca al dominio de el cliente , se puede envíar una sincronización manual con el Directorio activo , programando una tarea atraves de *Tareas > Tareas de servidor*

Existe una tarea denominada sincronización de grupos estáticos y atreves de esta es posible sincronizar manualmente con el Directorio Activo.

## Importación manual.
En los casos en los que no se cuenta con un Directorio Activo, ESET Protect brindo posibilidad de añadir equipos de otras maneras.
*Equipos>Agregar nuevo*
Se pueden agregar equipos de escritorios, laptops o dispositivos moviles.

El apartado *Agregar equipos* brinda 2 opciones:

La primera posibilidad consiste e ingresar los equipos de a uno, colocando la IP del equipo o el nombre (en el caso de tener un DNS configurado correctamente)
Tambien se puede importar un archivo CSV.

==Importante
Si bien se puede decidir a que grupo pertenecen los equipos posteriormente, de no contar con un Directorio Activo y por ende , no tener forma de organizarlos se suguiere que al importar los equipos por lotes, manualmente o atravez de un CSV, se defina de una vez a que grupo de la empresa pertenecen.

Existe la posibilidad de definir la acción a realizar en caso de detectarse un conflicto (Que un equipo que se intente añadir ya se encuentre registrado)
las 2 opciones son:

-Preguntar cuando se detecta.
-Omitir dispositivos conectados.
-Mover dispositivos duplicados a un grupo.
-Crear dispositivos duplicados.

## Utilización del sensor RD
Es un componente que permite detectar equipos conectados a la red del cliente y arroja un reporte que puede ser visualizado desde el Dashboard de ESET Protect.

Dentro del reporte habrá una relaciona entre equipos conocidos y equipos no autorizados es decir aquellos que no estan siendo administrados por ESET Protect.



