# Apuntes windows server core

Iniciación al trabajo con Server Core - Windows Server


https://www.youtube.com/watch?v=l67XfaBSm6E



____


Installing a new Server Core Domain Controller into an existing Domain/Forest

https://www.youtube.com/watch?v=zPvGNBsyFcg


____

para tener la unidad Z: en virtualbox tenemos que tener en el apartado "Almacenamiento" de virtualbox en SATA 1 el VBoxGuestAdditions.iso establecido

Para activar la deteccion de las maquinas y que se vea a traves de Red seguir este video:



- Centro de redes y recursos compartidos, para levantar la pantalla desde la linea de comandos

Windows 10 No Detecta Equipos en la Red [Solucion 2021]

https://www.youtube.com/watch?v=_podte1whTg

Habria que agregar desde roles y caracteristicas el servicio de impresion y documentos y dentro de este role esta compartir archivos SMB/CIFS elegir el "Cliente"

Tambien en el apartado de tarjetas de red, eligiendo la tarjeta de red correspondiente y eligiendo Internet Protocol version 4(TCP/IP) en el boton avanzadas y luego en la pestaña wins y dentro seleccionar el radio button "Enable NetBios over TCP/IP"

Esto que comento arriba lo podemos hacer con powershell de la siguiente manera:

<pre>
$adapter=(gwmi -computer srvf1 win32_networkadapterconfiguration | where {$_.servicename -like "nombre del servcicio adaptador"})

$adapter.settcpipnetbios(1)
</pre>

sacado de internet el powershell de arriba del siguiente link:

https://gheywood.wordpress.com/2012/03/16/changing-netbios-over-tcpip-with-powershell/



<pre>
control.exe /name Microsoft.NetworkAndSharingCenter
</pre>

- Como activar network discovery

- Para virtualbox la tecla host es la tecla derecha "CTRL"

- Para configurar inicialmente windows server core hay que correr powershell y luego correr el comando:

<pre>
sconfig
</pre>

- Para virtualbox la tecla host es la tecla derecha "CTRL"



- Public Network profile, activarlo

<pre>
en ingles

Set-NetFirewallRule -DisplayGroup "File And Printer Sharing" -Enabled True -Profile Any

en español

Set-NetFirewallRule -DisplayGroup "Compartir archivos e impresoras" -Enabled True -Profile Any

Set-NetFirewallRule -DisplayGroup "Detección de redes" -Enabled True -Profile Any
</pre>

- Para permitir administracion remota:

<pre>
Configure-SMRemoting –Enable

Enable-NetFirewallRule -DisplayGroup “Windows Remote Management”

Configure-SMRemoting -Get

Enable-PSRemoting –force
</pre>

- Para poder trabajar con las reglas de firewall:

<pre>
Import-Module -Name 'NetSecurity'
</pre>



<pre>
Enable-NetFireWallRule -DisplayName “Windows Management Instrumentation (DCOM-In)”
Enable-NetFireWallRule -DisplayGroup “Remote Event Log Management”
Enable-NetFireWallRule -DisplayGroup “Remote Service Management”
Enable-NetFireWallRule -DisplayGroup “Remote Volume Management”
Enable-NetFireWallRule -DisplayGroup “Remote Scheduled Tasks Management”
Enable-NetFireWallRule -DisplayGroup “Windows Firewall Remote Management”
Enable-NetFirewallRule -DisplayGroup "Remote Administration"
</pre>


- Consultar Reglas de firewall:

Tener en cuenta que si instalamos la version en español tenemos que encontrar los nombres en español.

<pre>
Get-NetFirewallRule -DisplayGroup "Network Discovery" | ft

Get-NetFirewallRule | Select-Object DisplayName,DisplayGroup

Get-NetFirewallRule | Select-Object DisplayName,DisplayGroup | Where-object {$_.DisplayGroup -like "*red*"}

Get-NetFirewallRule | Select-Object DisplayName,DisplayGroup | Where-object {$_.DisplayGroup -like "*Compartir*"}

</pre>

Consultar los servicios:

<pre>
Get-Service 



</pre>








___






