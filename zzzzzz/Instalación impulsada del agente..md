[[ESET]]
Permite realizar instalaciones remotas desde la consola a cualquier equipo en la red con un sistema operativo compatible.

Para poder llevar adelante instalaciones impulsadas es necesario cumplir con una serie de pre-requisitos (Que comúnmente se cumplen en entornos standar de windows y linux) 

1- La estación de trabajo en la cual se instalara la solución de ESET debe responder a un ping desde el equipo en el cual de ha instalado el servidor ESET Protect.
![[Pasted image 20230612154221.png]]
Si la estación de trabajo y el servidor se hallan dentro de un ambiente mixto de dominio y grupo de trabajo (o si ESET PROTECT se ejecuta bajo windows 2003), la opción de Usar Asistente para compartir (recomendado) debe estar deshabilitada.
![[Pasted image 20230612154538.png]]
La opcion Usar el Asistente para compartir (recomendado) esta ubicada en *Panel de control > Opciones de carpeta > ver*
![[Pasted image 20230612154730.png]]
![[Pasted image 20230612154800.png]]
La estacion de trabajo debe tener activada el recurso compartido ADMIN$ (INICIO > Panel de control > Herramientas administrativas > Administración de equipos > Carpetas compartidas > Recursos compartidos )
EL usuario debe tener permisos de administrador para ejecutar la instalación remota.

## Windows vista Windows 7 Windows Server 2008 
El servicio ESET Protect debería ejecutarse con permisos de Administrador de dominio.
![[Pasted image 20230612160448.png]]
Para configurar permisos de Administrador de dominio para ESET Project se debe acceder a *INICIO > Panel de control > Herramientas Administrativas > Servicios.*
*Clic derecho > Propiedades*
![[Pasted image 20230612160902.png]]
Accede a iniciar sesión y seleccionar esta cuenta.
![[Pasted image 20230612161037.png]]

==El usuario administrador debe tener una contraseña.

![[Pasted image 20230612161520.png]]

Desde el servidor, verifica que puedes acceder en forma remota a la estación de trabajo.
![[Pasted image 20230612161900.png]]

Verifica que la estación de trabajo pueda acceder a IPC utilizando el siguiente comando desde la linea de comando: 
net use \\servername IPC$
servername = nombre del servidor desde el que se ejecuta ESET Protect.

![[Pasted image 20230612162416.png]]

El firewall de la red no debe bloquear la comunicación o los recursos compartidos entre el servidor y la estacion de trabajo.
![[Pasted image 20230612162606.png]]
El servidor ESET Protect debe permitir la recepción de datos a través de los puertos 2221- 2224., Si el servidor tiene bloqueado alguno de estos puertos, la comunicación con la estación de trabajo no será posible.

==Una posible forma de validación de la disponibilidad de un puerto es intentando realizar una conexión telnet al mismo.

Para sistemas operativos Windows se debe verificar lo siguiente:
1 Las estaciones cliente serán visibles en ambos servidores y también sus conexiones 
2 "compartir impresoras y archivos para redes Microsoft" debe estar habilitado *Panel de control > Conexiones de red > Propiedades*
3 El servicio "remote procedure call (RCP)" debe encontrarse en ejecución en la estación de trabajo.
4 El servivio "Remote Registry" debe encontrarse en ejecución en la estación de trabajo 
5 El servivio "RCP Locator" debería estar configurado en manual y no necesita encontrarse en ejecución.

## Instalacion del agente
![[Pasted image 20230612165539.png]]
*Menu de vínculos rápidos > otras opciones de implementación*
![[Pasted image 20230612165713.png]]

Al ingresar allí aparece un cuadro de dialogo con las distintas opciones de la instalación de agente , en particular ,dentro de implementación remota, la tarea del servidor *instalacion de agente > crear tarea*

![[Pasted image 20230612170033.png]]
Otra posible forma es dirigirse a *Tareas > Tareas de servidor > implementación de agente*
![[Pasted image 20230612170155.png]]
También es posible iniciar un agente de instalación directamente sobre el equipo. En caso de tener un equipo no administrado , al hacer clic sobre el dentro del menu contextual se despliega una acción denominada *instalar agente*.
![[Pasted image 20230612170710.png]]

1 Nombre de la tarea 
Nombre descriptivo de la acción que se esta llevando a cabo. por ejemplo: instalación impulsada del agente.
2 Descripcion 
Detalles de la tarea
3Tipo de tarea 
implementación de agente
4Ejecucion inmediata
Esta opción permite que la tarea se dispare de inmediato
5Configurar desencadenador
Permite definir el desencadenador una vez configurada la tarea

Configuración de la tarea 
Se debe determinar que tipo de agente va a instalarse. La consola ha sido diseñada para realizar una resolución automática del agente que va a ser instalado en el equipo. En otras palabras, la consola se encarga de determinar si el equipo es Windows, Linux oh Mac

Adicionalmente ,detecta si la arquitectura del equipo es de 32 o 64 bits , y en base a ello instala el agente dependiendo de cual sea la plataforma.

De este modo, el usuario no tiene la necesidad de preocuparse sobre a que tipo de equipos va a enviar la tarea. De todas maneras, es posible quitar esta opción y en este caso es el usuario que definir que tipo de agente se instala tomando en cuanta el equipo destino.
![[Pasted image 20230612172118.png]]
Luego de configurar el tipo de agente (en general se recomienda mantener la resolución automática), se deben seleccionar los equipos que estarán recibiendo la tareas (destino)
Es posible incluir maquina por maquina, parte de la organización ,un grupo , dinámicos ,etc.
![[Pasted image 20230612172600.png]]
Una vez que se decide en que maquina oh en que grupo de maquinas se desea instalar el agente, en el campo Nombre del Host se debe indicar cual es el servidor en el que el agende deberá reportar.

Si bien es un parámetro opcional, se sugiere definirlo siempre, preferiblemente colocando la IP del servidor oh su nombre en caso de trabajas con IPs dinámicas

En la mayoría de los casos se tratara de in servidor ESET Protect; sin embargo,cuand0 se cuanta con una arquitectura distribuida puede  ser un servidor APACHE HTTP Proxy (dependiendo de si estos agentes reportarían al cliente ESET Protect directamente o atreves de un proxy HTTP, por ejemplo en alguna sucursal)

En caso de dejar esta opción en blanco., automáticamente se utiliza el nombre del la maquina donde ESET Protect esta instalado.

Es importante garantizar que no haya discrepancias entre el FQDN del equipo y la forma en que en realidad es identificada por el DNS del cliente. por esto mismo, se sugiere utilizar la IP.
Por lo contrario, si se trabajo por grupos de trabajo, es necesario utilizar la contraseña del administrador local. Este es el único usuario que puede realizar la instalación del agente en forma remota.

## Configuracion de certificados

![[Pasted image 20230612173835.png]]
A continuación se hace alusión a la configuración de certificados que permite seleccionar que certificados van a utilizarse en la comunicación cifrada entre el agente y ESET Protect.

Todos los certificados suelen ser creados durante la instalación del servidor de la administración remota. En este caso se deben seleccionar los certificados que están almacenados en los repositorios de la consola y acceder al que se denomina certificado de agente.

Si durante la creación de estos certificados haz definido una contraseña para ellos , debes colocarla en el campo "Frase de contraseña"
![[Pasted image 20230612174509.png]]
Luego de establecer estos parámetros , es necesario definir el desencadenador en caso de que no se haya marcado inicialmente, ejecuta la tarea inmediatamente liego de finalizar.

Luego de que se configuren todos los datos, puede verse un resumen de la información ingresada. El botón Finalizar da inicio a la tarea de implementación de agente permite visualizar su ejecución.
El resultado nos arroja correctos y erroneos.







