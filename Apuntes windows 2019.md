# Apuntes de windows 2019

Configurando VPN con L2TP/IpSec en Windows Server y conectar un cliente

https://www.youtube.com/watch?v=cnCUpK52RTw

___

Instalar IIS y administración remota - Windows Server Core

https://www.youtube.com/watch?v=gglzI_W4rl8&list=PLEmsMMOSNtypei8PRD8vFH5-P99Sn5Kk7&index=35

Hay que instalar con powershell 

Install-windowsFeature Web-Server,Web-Mgmt-Service

una vez instalado ejectuamos:

regedit
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WebManagement\Server\
Cambiamos la clave EnableRemoteManager : 1

sc config wmsvc start=auto

net start wmsvc

shutdown -l




___
