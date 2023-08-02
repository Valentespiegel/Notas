[[ESET]]
Existen ciertos parámetros que deben ser validados antes de continuar con el Deployment dentro de la organización.

## Administracion de licencias.

==Ya sea en la instalacion de all-in-one,Antivirus oh web Consolé.

## Configuracion del servidor.

Se establece el puerto por el cual la consola va a esta recibiendo conexiones tanto de los agentes como para abrir la consola web por defecto estos puertos son el 2222 o el 2223 y, a pesar de ser editables *la recomendación es dejarlos como vienen preconfigurados*
Adicionalmente, ya viene importado el certificado con el que se establece la seguridad HTTPS en la conexión con la consola de administración.

## Apache HTTP Proxy

Es importante destacar que ESET Protect viene con un Apache HTTP Proxy para manejar las conexiones a internet y la centralización de las actualizaciones de la soluciones de seguridad

==Usar servidor proxy.
usar conexion directa si el proxy HTTP no esta disponible.

## Servidor SMTP
En este apartado se puede configurar el servidor del correo electrónico que va a utilizar la consola de gestión para todos los envíos automáticos (Notificaciones, envió  automático de reportes y cualquier otro mensaje automático que decida programar en la consola)

-Es necesario activar el servidor SMTP 

-Se debe de colocar el nombre del host donde esta ejecutándose el servidor de correo (Puede ser un servidor de correo electrónico propio como Exchange o un servidor de correo en la nube como , por ejemplo una cuenta de gmail)

-Se debe validad con el proveedor de servicio de correo cuales son los datos adecuados de este como lo son los puertos de conexion y el tipo de protocolo de seguridad como lo pueden ser TLS o StarTLS

En base a lo mencionado, se puede configurar toda la conexión al servidor de correo electrónico al colocar un Nombre de usuario y contraseña este debe corresponder, esta debe ser una ya existente o un buzón electrónico creado por la compañía especifico para la consola.

==Se te permite un envió de correo de prueba que permite comprobar si la conexion por consola es exitosa.

==Se puede personalizar ela consola con las visualizaciones que se indique como el logo y nombre de la empresa.

## Politicas.

Antes de empezar un proceso de instalación en masa, es importante validar por un lado las políticas personalizadas y otras incorporadas por defecto de ESET.

son 3 a los  que debemos prestar mas atencion.

==ESET Protect Agent

Utilizar Proxy Global si se va a utilizar un solo servidor para todos los servicios del ESET Project. En esta configuracion se deben verificar que el pueto que estan precargados coincidan con la maquina a la cual esta instalado el HTTP Proxy , Sin embargo, es posible que esta asignación por defecto no sea la adecuada ya que en casos de clientes con entornos distribuidos con mas de una sucursal, es posible que existan equipos que no puedan realizar las conexiones al Apache HTTP Proxy principal.
Por esta razón es importante  validar que esta política solo este asignada a aquellos equipos que tienen conexión, es necesario crear una política de agente distinta para cada sucursal o para cada grupo de equipos que va a utilizar distintos Apache HTTP Proxy., en este caso se utiliza conexión directa.

==Producto de seguridad para windows - uso de proxy HTTP

También es importante validar que la dirección corresponda al servidor Apache Http Proxy que usaran los equipos para conectarse con los servidores de ESET en la nube. De la misma manera, hay que tomar en cuanta los ajustes necesarios en caso de entornos distribuidos., Al igual de ser necesario se requiere una política para cada uno de ellos. Y usar una configuración global del proxy.


## Actualizaciones.

Por defecto viene configurado como "autoseleccionar"  para que escoja cualquiera de los servidores disponibles de ESETn

*El intervalo de conexión es de 6 horas*

==Actualización normal.

Ajuste predeterminado. ESMC descarga las actualizaciones del modulo automáticamente del servidor ESET

==Actualización previa a su lanzamiento

Obtenga acceso a las correcciones mas recientes de los componentes de ESMC. 
*Puede fallar la estabilidad y no se recomienda en sistemas de producción*

==Actualización demorada

Las actualizaciones de los componentes de entregan con variantes de retraso para garantizar una estabilidad máxima.