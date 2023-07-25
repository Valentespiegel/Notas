### DarkHole 2
[[DarkHole 2]]

Information Leakage
Github Project Enumeration
SQLI (SQL Injection)
Chisel (Remote Port Forwarding) + Abusing Internal Web Server
Bash History - Information Leakage [User Pivoting]
Abusing Sudoers Privilege [Privilege Escalation]

---

### Inferno & Masashi
[[Inferno & Masashi]]

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

---
### Wpwn 
[[Wpwn y DMV (Pivoting Lab)]]

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

### DMV 

Enumeración web  
Explotación de la utilidad web Youtube-dll (Inyección de comandos + SOCAT para saltar a la nueva subred) 
Explotación de PwnKit CVE-2021-4034 [Escalada de privilegios]

---

## Cereal

[[Cereal]]

==1. Enumeración FTP: 

Es un proceso de recopilación de información para identificar y obtener detalles sobre los servicios FTP (Protocolo de Transferencia de Archivos) que pueden estar en ejecución en un sistema o servidor. Esta enumeración puede revelar información como usuarios disponibles, directorios accesibles, permisos de archivos y otras configuraciones relacionadas con el servicio FTP.
   
==2. Hospedaje Virtual: 

El hospedaje virtual, o Virtual Hosting en inglés, se refiere a la práctica de alojar múltiples sitios web en un mismo servidor físico. Esto se logra mediante la configuración de reglas de enrutamiento que permiten que varios dominios compartan los recursos del servidor, como la potencia de procesamiento, el espacio en disco y la memoria.

==3. Enumeración de Subdominios: 

Es un proceso de búsqueda y listado de subdominios asociados a un dominio principal. Los subdominios son parte del dominio principal y permiten organizar y separar contenido específico. Esta técnica es comúnmente utilizada para mapear la superficie de ataque de un objetivo y descubrir posibles puntos de entrada adicionales.

==4. Divulgación de Información - Descubrimiento de Archivos de Respaldo: 

En este contexto, la divulgación de información se refiere al descubrimiento accidental o intencional de archivos de respaldo en un servidor. Estos archivos de respaldo podrían contener información sensible o datos confidenciales que no deberían estar accesibles públicamente. Los atacantes pueden utilizar esta información para obtener una ventaja en futuros ataques.
    
==5. Ataque de Deserialización PHP [RCE]: 

Es un tipo de ataque que explota vulnerabilidades en el proceso de deserialización de datos en aplicaciones web PHP. Los atacantes manipulan los datos serializados para ejecutar código malicioso en el servidor, lo que puede conducir a una ejecución remota de código (RCE) y, potencialmente, a la toma de control del sistema.
    
==6. Enumeración de Tareas Programadas (pspy): 

Esta técnica implica investigar y listar las tareas programadas (cron jobs en sistemas basados en Unix/Linux) configuradas en un sistema. Esto puede revelar cron jobs maliciosos o tareas automatizadas que podrían ser utilizadas para actividades malintencionadas.
    
==7. Abuso de Tarea Programada (Chown Symlink) [Escalada de Privilegios]: 

Se refiere a la explotación de una vulnerabilidad en un script de tarea programada (cron job) para lograr una escalada de privilegios en un sistema. En este caso, se menciona el "Chown Symlink", que posiblemente se refiere a la creación de enlaces simbólicos (symlinks) y cambiar sus propietarios (chown) para obtener acceso no autorizado a recursos o directorios con privilegios elevados.

---
