---
Titulo: "Apuntes ADFS"
---
Instalar un servidor de dominio, bosque

13 Windows Server 2016 - Instalación del Rol de Active Directory

https://www.youtube.com/watch?v=_m5jfVdQz9k&list=PLXFOGHLLtDHtBeEeUQYmHx3GY5p-C4JIi&index=14

Active directory y dns van de la mano
___


windows server 2016 active directory

https://www.youtube.com/watch?v=BfnZTrkmrfk&list=PLXFOGHLLtDHtBeEeUQYmHx3GY5p-C4JIi&index=15



___

70-410 Objective 5.1 - Installing an Active Directory Domain Controller on Windows Server 2012 R2 La


https://www.youtube.com/watch?v=k1yL2UNME-U


___

ADFS - Active Directory Federation Service - Installation

https://www.youtube.com/watch?v=9eq3IeDAkvA&list=PL8wOlV8Hv3o9uHl0XFfI6_katp6BXNVjb&index=3


___

How to install and configure ADFS on Windows Server

https://www.youtube.com/watch?v=jlF9PRiCH9s


Este es el mas sencillo de configurar, el mas simple para tener un ADFS

Crea un certificado a traves del servidor web iis, autofirmado, que luego lo exporta, para que lo coja el servidor ADFS.

Despues de configurar hay que esperarse un poco porque si entramos a la herramienta cliente de ADFS nos da un error de no puede conectarse a una base de datos especial, hay que darle tiempo, cuando recien creado


set-adfsproperties -EnableIdpInitiatedSignonpage $True
___





