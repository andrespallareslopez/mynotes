# Apuntes windows server core

Iniciación al trabajo con Server Core - Windows Server


https://www.youtube.com/watch?v=l67XfaBSm6E



____


Installing a new Server Core Domain Controller into an existing Domain/Forest

https://www.youtube.com/watch?v=zPvGNBsyFcg


____

- Centro de redes y recursos compartidos

<pre>
control.exe /name Microsoft.NetworkAndSharingCenter
<pre>

- Como activar network discovery

- Para virtualbox la tecla host es la tecla derecha "CTRL"

- Para configurar inicialmente windows server core hay que correr powershell y luego correr el comando:

<pre>
sconfig
<pre>

- Para virtualbox la tecla host es la tecla derecha "CTRL"



- Public Network profile, activarlo

<pre>
Set-NetFirewallRule -DisplayGroup "File And Printer Sharing" -Enabled True -Profile Any
<pre>

- Para permitir administracion remota:

<pre>
Configure-SMRemoting –Enable

Enable-NetFirewallRule -DisplayGroup “Windows Remote Management”

Configure-SMRemoting -Get

Enable-PSRemoting –force
<pre>

- Para poder trabajar con las reglas de firewall:

<pre>
Import-Module -Name 'NetSecurity'
<pre>



<pre>
Enable-NetFireWallRule -DisplayName “Windows Management Instrumentation (DCOM-In)”
Enable-NetFireWallRule -DisplayGroup “Remote Event Log Management”
Enable-NetFireWallRule -DisplayGroup “Remote Service Management”
Enable-NetFireWallRule -DisplayGroup “Remote Volume Management”
Enable-NetFireWallRule -DisplayGroup “Remote Scheduled Tasks Management”
Enable-NetFireWallRule -DisplayGroup “Windows Firewall Remote Management”
Enable-NetFirewallRule -DisplayGroup "Remote Administration"
<pre>


- Consultar Reglas de firewall:

Tener en cuenta que si instalamos la version en español tenemos que encontrar los nombres en español.

<pre>
Get-NetFirewallRule -DisplayGroup "Network Discovery" | ft

Get-NetFirewallRule | Select-Object DisplayName,DisplayGroup

Get-NetFirewallRule | Select-Object DisplayName,DisplayGroup | Where-object {$_.DisplayGroup -like "*red*"}

Get-NetFirewallRule | Select-Object DisplayName,DisplayGroup | Where-object {$_.DisplayGroup -like "*Compartir*"}

<pre>










___






