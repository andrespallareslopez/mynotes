---
Titulo: "Apuntes Azure"
---

# Apuntes Azure


**Hybrid Connections Azure WebApp**

https://www.youtube.com/watch?v=yr03uvJR3BM

trata de como conectarse a un app services desde otra red diferente a la de azure por ejemplo conexiones locales http://localhost:5000, tal vez desde tu maquina local

___

**Creating Scalable WCF Service for Azure Service Fabric**

https://www.dotnetcurry.com/windows-azure/1342/create-wcf-service-azure-service-fabric


**WCF con netTcpBinding en Microsoft Azure**

https://www.returngis.net/2019/11/wcf-con-nettcpbinding-en-microsoft-azure/


**Desplegar un servicio web con WCF en Azure App Service**

https://www.returngis.net/2019/11/desplegar-un-servicio-web-con-wcf-en-azure-app-service/

Los servicios WCF para poder trabajar en azure app services tienen que estar en https

___

Host WCF Service in Azure App Service

https://aspdotnetcodehelp.wordpress.com/2017/11/13/hosting-wcf-in-azure-app-service/

___

Introduction to highly scalable web api using Service Fabric

https://www.youtube.com/watch?v=dvnZxF0E28I&list=PLQPgqnK4E_goI0EltuzCpCkhpfNcQ5f__&index=9

___




Deploy Multiple Web Applications Into Single Azure Web App

https://www.youtube.com/watch?v=KIfftk5897s

___

Cómo configurar una VPN Sitio a Sitio de OnPrem a la nube Azure en 10 pasos

https://www.youtube.com/watch?v=-XhhlojFFxY

___

https://www.youtube.com/watch?v=5NMcM4zJPM4

AZ-900 Episodio 10 | Servicios de redes | Red virtual, puerta de enlace VPN, CDN, equilibrador de carga, aplicación GW

Virtual network

-subnet

-subnet

vnet peering o vpn gateway allow cross Vnet Communication

Azure tiene para hacer un diagrama de tu infraestructura


___

Azure Virtual Network Step by Step

https://www.youtube.com/watch?v=ADdGZEfmNzQ


___

Azure Virtual Network Overview

https://www.youtube.com/watch?v=7rzawA--r20


____

Conecte su red local a Azure mediante ExpressRoute

https://www.youtube.com/watch?v=C6uglNSRlY8


___

Azure Networking For Beginners | Learn Azure Networking Basics | K21Academy

https://www.youtube.com/watch?v=feQvnIUJ3Iw

yo creo que el mejor para entender las subredes dentro de un virtual network tiene parte practica



___

Azure Private Endpoint & Private Link explained in plain English with a story & demo in 5 minutes

https://www.youtube.com/watch?v=vVDql7IKneg

___

Azure Private Endpoints (Private Link) with services like App Services, SQL, and Storage Accounts

https://www.youtube.com/watch?v=8Zof54j8qWk


___

Azure Site-to-Site VPN quick setup

https://www.youtube.com/watch?v=hKgEjqTp8MI


___

Site-to-Site Azure VPN with a Windows RRAS Server

https://www.youtube.com/watch?v=QQ40gxxxT8Y

En este tutorial muestra como crear un azure virtual private network gateway y como conectarlo a un windows RRAS Server en una red domestica con un router/modem normal


___

Connect Local Computer to Azure Network VM Using RDP over Point to Site VPN - Hands On Demo!

https://www.youtube.com/watch?v=oYmn17S2E_s&t=1406s

Crear un azure virtual network gateway y descargar el cliente para crear una conexion VPN entre tu maquina local y la red "virtual network" que hayas creado en tu cuenta azure

___

How to setup Site to Site (S2S) VPN from local OnPrem to Azure Cloud in 10 steps

https://www.youtube.com/watch?v=MorG47BTttU

En este tutorial crea un virtual private network gateway que conecta con una red on-premise local a traves de un servidor windows 2019 on-preimise con RASS configurado y luego crea una maquina virtual en azure y una vez configurado la parte de azure VPN gateway y el servidor windows server RASS, los conecta sitio a sitio y luego desde la red local onpremise con el RASS activado a traves del windows server conecta a traves de la red de azure a la maquina virtual en azure.

___

How to Configure Azure Point to Site VPN Step By Step | Azure Point to Site VPN Certificate | AZ P2S

https://www.youtube.com/watch?v=Gb3YE-0gBWQ

crea dos tipos de certificado; uno el root o principal para luego utilizar este certificado para firmar y crear otros certificados

con powershell:

$cert = New-SelfSignedCertificate -Type Custom -keyspec Signature -Subject "CN=P2SRootNew" -keyExportPolicy Exportable -hashAlgorithm sha256 -keyLength 2048 -CertStoreLocation "Cert:\CurrentUser\My" -keyUsageProperty Sign -keyUsage CertSign

New-selfSignedCertificate -Type Custom -DnsName P2SChildCertNew -keySpec Signature -Subject "CN=P2SChildCertNew" -keyExportPolicy Exportable -hashAlgorithm sha256 -keyLength 2048 -CertStoreLocation "Cert:\CurrentUser\My" -Signer $cert -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.2")


___

Curso y redes en microsoft Azure

1-Introducción al curso (Redes en Azure)

https://www.youtube.com/watch?v=2839dEa6pF0&list=PLWDmZWXFtqIqh2Hzh_Z3tzUvA-UjOODTD&index=1


2-Crear una cuenta en Azure (Redes en Azure)

https://www.youtube.com/watch?v=Ab2bu1PuSNE&list=PLWDmZWXFtqIqh2Hzh_Z3tzUvA-UjOODTD&index=2

3 - Portal de Azure (Redes Azure)

https://www.youtube.com/watch?v=eW3J-CyTf8A&list=PLWDmZWXFtqIqh2Hzh_Z3tzUvA-UjOODTD&index=3

4 - Creación de primera red virtual (Redes Azure)

https://www.youtube.com/watch?v=U1_qnfhNR2M&list=PLWDmZWXFtqIqh2Hzh_Z3tzUvA-UjOODTD&index=4

5 - Primer servidor web (Redes Azure)

https://www.youtube.com/watch?v=7cRHzqfjEpw&list=PLWDmZWXFtqIqh2Hzh_Z3tzUvA-UjOODTD&index=5


____

Azure Point-to-Site VPN with Certificate Based Authentication

https://www.youtube.com/watch?v=Yshpo6V1qUQ

point to site connections into azure v-net

- Create a V-net Gateway
- Create a Root Certificate
- Create Client Certificates
- Export Certificates
- Configure  the  gateway for Point-to-site Connections
- Configure the client
- Revoke a Certificate


___

Tutorial de Azure Active Directory (AD, AAD) | Servicio de gestión de identidades y accesos

https://www.youtube.com/watch?v=Ma7VAQE7ga4


___








