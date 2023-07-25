Es un complemento para administrar el cifrado de disco completo en sus estaciones de windows, el cual te brinda una capa de seguridad adicional en el inicio de sesión de los equipos al cifrar el disco oh incluso una unidad completa del sistema.

*Políticas > ESET Full Disk Encryption > configuración > opciones de cifrado > habilitar cifrado*
esto habilita oh deshabilita el cifrado en la estación de trabajo administrada.
Podemos elegir en  cifrar solo el disco de arranque o cifrar todos los discos.

Según el hardware disponible del usuario ya sea TMP o OPAL

El TPM se utiliza para proteger la integridad y la confidencialidad de los datos almacenados en el dispositivo. Proporciona un entorno aislado y seguro donde se pueden realizar operaciones criptográficas, como el cifrado y la generación de claves, sin que los datos sean accesibles desde fuera del chip.

OPAL se basa en el estándar de Autenticación y Privacidad del Disco Duro (ATA) de TCG (Trusted Computing Group). Utiliza un chip de seguridad integrado en el propio dispositivo de almacenamiento, llamado Unidad de Autenticación Opal (OUA), para gestionar el cifrado y la seguridad de los datos.

Esto ultimo requerirá de la fabricación de una contraseña.

## Instalación desde ESET Protect.

1 Crear un instalador todo en uno

*Instaladores > crear instalador  > instalador todo en uno* > básico >cifrado de disco completo > continuar

Se tiene que seleccionar la licencia de EFDE que deseamos usar, así como el producto oh la versión que incluiremos en el instalador y el idioma del el producto., se determinan políticas nombre y descripción antes de descargar.

## Tarea de instalación de software.

Otra opción que tenemos es utilizar una tarea de instalación de software en equipos que ya se encuentre administrados.
*Tareas > Nueva > Tarea del cliente*
Se especifica nombre y descripción de la tarea  
*Nombre > Descripción > categoría de tarea > sistema operativo >instalación de software*
En la sección de configuración seleccionamos la licencia EFDE vigente, después elegimos el paquete de instalación del producto y por ultimo la licencia y se crea el desencadenador que se puede ejecutar en ese momento oh cuando se le indique.

## Uso del asistente de cifrado desde ESET Protect.
Otra alternativa que podemos usar, es iniciar el cifrado en un cliente que ya se encuentra  administrado en nuestra consola.
*Equipos > menú contextual > habilitar cifrado*
*Mostrar detalles > vista general > mosaico de cifrado  cifrar equipo*
se determina licencia y política.

