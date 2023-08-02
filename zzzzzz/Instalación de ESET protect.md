
[[ESET]]
[[Captura de pantalla 2023-06-09 130947.png]]
### ==1.) Descargar el .OVA de la Web Console y ejecutarlo en virtualbox.

![[Captura de pantalla 2023-06-09 131217.png]]

![[Captura de pantalla 2023-06-09 131301.png]]
### ==2.) Aceptamos Acuerdos de licencia , certificados y teniendo en cuenta las especificaciones del equipo modificar núcleos de procesador y memora RAM a la maquina virtual.

![[Captura de pantalla 2023-06-09 131602.png]]
### ==3.)Desde Windows CMD aplicando el comando ipconfig tenemos acceso a la información de la tarjeta de red la cual nos va a servir a continuación.

![[Captura de pantalla 2023-06-09 131739.png]]

### ==4.)Algunas configuraciones de pc tienen el DHCP desactivado, a lo cual nos toca a nosotros asignar los sigientes valores.

Direccion IPv4 "Nos ayudara a calcular alguna ip disponible en el segmento de red"
Mascara de subred 
Puerta de enlace predeterminado 
DNS "8.8.8.8"

![[Captura de pantalla 2023-06-09 131837.png]]


![[Captura de pantalla 2023-06-09 131904.png]]
### ==5.) Esta informacion debe ser registrada en la maquina virtual, la cual empezara con variados procesos asta que nos entregue el acceso desde nuestro navegador con la IP fabricada que en esta ocacion fue 192.168.20.177

![[Captura de pantalla 2023-06-09 132111.png]]

### ==6.) Continuamos aceptando los riesgos en Avanzado y continuar.

Dirección IPv4 "192.168.20.177"
Mascara de subred "255.255.255.0"
Puerta de enlace predeterminada "129.168.20.254"
DNS "8.8.8.8"

![[Captura de pantalla 2023-06-09 132210.png]]

### ==7.) La Web nos muestra campos a rellenar como por ejemplo HOSTNAME y PASSWORD asi como las espesificaciones de red que hace un mometo capturamos gracias al cmd

### ==8.) Después la maquina se reiniciara multiples veces hasta que  se ejecute de manera como se muestra en la siguiente imagen., esto ya es una señar de acceso.


![[Captura de pantalla 2023-06-09 133417.png]]

![[Captura de pantalla 2023-06-09 133554.png]]

### ==9.) La Web console nos pide el hostname y password que ya antes fabricamos.


![[Captura de pantalla 2023-06-09 133637.png]]

![[Captura de pantalla 2023-06-09 133657.png]]

### ==10.) Ya dentro del Dashboard de ESET como practica de seguridad se recomienda exportar los certificados pares y la autoridad de certificacion y almacenar en un lugar seguro para su posible recuperacion.
