---
Titulo: "Apuntes Powershell para window core."
---

# Apuntes Powershell para window core.
- [Apuntes Powershell para window core.](#apuntes-powershell-para-window-core)
    - [Remotely managing your Server Core using WinRM and WinRS](#remotely-managing-your-server-core-using-winrm-and-winrs)
    - [Server Core 2019: Installing Features on Demand (FOD)](#server-core-2019-installing-features-on-demand-fod)
    - [Remotely Manage a Non-Domain Hyper-V Server from Windows 10](#remotely-manage-a-non-domain-hyper-v-server-from-windows-10)
    - [Change network location type with PowerShell in Windows 10](#change-network-location-type-with-powershell-in-windows-10)
    - [REMOTELY MANAGING HYPER-V SERVER IN A WORKGROUP OR NON-DOMAIN](#remotely-managing-hyper-v-server-in-a-workgroup-or-non-domain)
    - [Enable PowerShell Remoting on the PC You Want to Access Remotely](#enable-powershell-remoting-on-the-pc-you-want-to-access-remotely)
    - [Putting the ".NET" into "Kubernetes"](#putting-the-net-into-kubernetes)
    - [Installing IIS on nano server container](#installing-iis-on-nano-server-container)
    - [Install and manage IIS with SSL using PowerShell](#install-and-manage-iis-with-ssl-using-powershell)
    - [Automating IIS Feature Installation with Powershell](#automating-iis-feature-installation-with-powershell)
  - [Como crear archivos y folder en powershell](#como-crear-archivos-y-folder-en-powershell)
    - [Create a file in the current directory](#create-a-file-in-the-current-directory)
    - [Create a directory](#create-a-directory)
    - [Create a directory in a different directory](#create-a-directory-in-a-different-directory)
    - [Remove a directory](#remove-a-directory)
    - [Read and write web config file](#read-and-write-web-config-file)
- [get the directory of this script file](#get-the-directory-of-this-script-file)
- [get the full path and file name of the App.config file in the same directory as this script](#get-the-full-path-and-file-name-of-the-appconfig-file-in-the-same-directory-as-this-script)
- [initialize the xml object](#initialize-the-xml-object)
- [load the config file as an xml object](#load-the-config-file-as-an-xml-object)
- [iterate over the settings](#iterate-over-the-settings)
- [save the updated config file](#save-the-updated-config-file)
    - [Politicas de ejecucion de powershell](#politicas-de-ejecucion-de-powershell)
    - [Working with git from powershell](#working-with-git-from-powershell)


***Articulos para configuracion remota de windows server core:***

### Remotely managing your Server Core using WinRM and WinRS

https://dirteam.com/sander/2008/02/23/remotely-managing-your-server-core-using-winrm-and-winrs/

### Server Core 2019: Installing Features on Demand (FOD)

https://sid-500.com/2019/01/19/server-core-2019-installing-features-on-demand-fod/

### Remotely Manage a Non-Domain Hyper-V Server from Windows 10

https://tweaks.com/windows/67216/remotely-manage-a-nondomain-hyperv-server-from-windows-10/

### Change network location type with PowerShell in Windows 10

https://winaero.com/blog/network-location-type-powershell-windows-10/

### REMOTELY MANAGING HYPER-V SERVER IN A WORKGROUP OR NON-DOMAIN

https://timothygruber.com/hyper-v-2/remotely-managing-hyper-v-server-in-a-workgroup-or-non-domain/

### Enable PowerShell Remoting on the PC You Want to Access Remotely

https://www.howtogeek.com/117192/how-to-run-powershell-commands-on-remote-computers/

### Putting the ".NET" into "Kubernetes"

https://www.youtube.com/watch?v=GBOPBfcJ2zM


### Installing IIS on nano server container

https://www.youtube.com/watch?v=c3UfTBumehU

### Install and manage IIS with SSL using PowerShell

https://4sysops.com/archives/install-and-manage-iis-with-ssl-using-powershell/


Instalar todo el role iis:
<code>
   Install-WindowsFeature -name "Web-Server" -IncludeAllSubFeature ‑IncludeManagementTools
</code>

<code>
   Get-WindowsFeature | Where { \\$_.installed -eq $True}
</code>

<code>
UnInstall-WindowsFeature -Name NET-Framework-45-Features -whatif
</code>

<code>
get-windowsfeature | select Name | sort name
</code>

<code>
$servers = ('server1', 'server2')
PS C:\> foreach ($server in $servers) {Install-WindowsFeature -ConfigurationFilePath D:\ConfigurationFiles\ADCSConfigFile.xml -ComputerName $server}
</code>

<code>
Get-WindowsOptionalFeature -Online
Get-WindowsOptionalFeature -Online -FeatureName *Hyper-V*
</code>

<code>
Enable-WindowsOptionalFeature -Online -FeatureName "Hearts" -All
</code>



<code>
get-website
get-WebBinding
</code>
_____

### Automating IIS Feature Installation with Powershell

https://weblog.west-wind.com/posts/2017/may/25/automating-iis-feature-installation-with-powershell

<code>
Set-ExecutionPolicy Bypass -Scope Process
</code>

~~~
Enable-WindowsOptionalFeature -Online -FeatureName IIS-WebServerRole
Enable-WindowsOptionalFeature -Online -FeatureName IIS-WebServer
Enable-WindowsOptionalFeature -Online -FeatureName IIS-CommonHttpFeatures
Enable-WindowsOptionalFeature -Online -FeatureName IIS-HttpErrors
Enable-WindowsOptionalFeature -Online -FeatureName IIS-HttpRedirect
Enable-WindowsOptionalFeature -Online -FeatureName IIS-ApplicationDevelopment

Enable-WindowsOptionalFeature -online -FeatureName NetFx4Extended-ASPNET45
Enable-WindowsOptionalFeature -Online -FeatureName IIS-NetFxExtensibility45

Enable-WindowsOptionalFeature -Online -FeatureName IIS-HealthAndDiagnostics
Enable-WindowsOptionalFeature -Online -FeatureName IIS-HttpLogging
Enable-WindowsOptionalFeature -Online -FeatureName IIS-LoggingLibraries
Enable-WindowsOptionalFeature -Online -FeatureName IIS-RequestMonitor
Enable-WindowsOptionalFeature -Online -FeatureName IIS-HttpTracing
Enable-WindowsOptionalFeature -Online -FeatureName IIS-Security
Enable-WindowsOptionalFeature -Online -FeatureName IIS-RequestFiltering
Enable-WindowsOptionalFeature -Online -FeatureName IIS-Performance
Enable-WindowsOptionalFeature -Online -FeatureName IIS-WebServerManagementTools
Enable-WindowsOptionalFeature -Online -FeatureName IIS-IIS6ManagementCompatibility
Enable-WindowsOptionalFeature -Online -FeatureName IIS-Metabase
Enable-WindowsOptionalFeature -Online -FeatureName IIS-ManagementConsole
Enable-WindowsOptionalFeature -Online -FeatureName IIS-BasicAuthentication
Enable-WindowsOptionalFeature -Online -FeatureName IIS-WindowsAuthentication
Enable-WindowsOptionalFeature -Online -FeatureName IIS-StaticContent
Enable-WindowsOptionalFeature -Online -FeatureName IIS-DefaultDocument
Enable-WindowsOptionalFeature -Online -FeatureName IIS-WebSockets
Enable-WindowsOptionalFeature -Online -FeatureName IIS-ApplicationInit
Enable-WindowsOptionalFeature -Online -FeatureName IIS-ISAPIExtensions
Enable-WindowsOptionalFeature -Online -FeatureName IIS-ISAPIFilter
Enable-WindowsOptionalFeature -Online -FeatureName IIS-HttpCompressionStatic

Enable-WindowsOptionalFeature -Online -FeatureName IIS-ASPNET45

~~~

To see all the features available related to IIS you can use:
~~~
Get-WindowsOptionalFeature -Online | where FeatureName -like 'IIS-*'
~~~

Check for Installed Features:
~~~
Get-WindowsOptionalFeature -Online | where {$_.state -eq "Enabled"} | ft -Property featurename
~~~
Check for Features available but Not Installed
~~~
Get-WindowsOptionalFeature -Online | where {$$_.state -eq "Disabled"} | ft -Property featurename
~~~

~~~
Disable-WindowsOptionalFeature -Online -FeatureName IIS-DirectoryBrowsing
~~~

Create an IIS Application Pool and Web Site


~~~
Import-Module WebAdministration 
~~~

To create an Application Pool:
~~~
New-WebAppPool -name "NewWebSiteAppPool"  -force
appPool = Get-Item IIS:\AppPools\SUMO_Atlas
appPool.processModel.identityType = "NetworkService"
appPool.enable32BitAppOnWin64 = 1
appPool | Set-Item
~~~

~~~
$site = $site = new-WebSite -name "NewWebSite" 
                            -PhysicalPath "c:\Web Sites\NewWebSite" 
                            -HostHeader "home2.west-wind.com"
                            -ApplicationPool "NewWebSiteAppPool" 
                            -force
~~~

~~~
New-WebBinding -Name "Default Web Site" -IP "*" -Port 443 ‑Protocol https
~~~

~~~

New-Website -Name "SUMO_Atlas" -PhysicalPath "c:\SUMO\WebSites" -ApplicationPool "SUMO_Atlas" -port 8084 -force

$newCert = New-SelfSignedCertificate -dnsname "WRSWATD01.sareb.srb" -KeyLength 2048 -CertStoreLocation Cert:\LocalMachine\My -NotAfter (Get-Date).AddYears(21)

New-WebBinding -Name "SUMO_Atlas" -IP "*" -Port 443 -Protocol https

$binding = Get-WebBinding -Name "SUMO_Atlas" -Protocol "https"

$binding.AddSslCertificate($newCert.GetCertHashString(), "my")

~~~




~~~
get-WebBinding
~~~

~~~
get-iisapppool
$AppPool = Get-IISAppPool -Name TestPool
$AppPool.Recycle()
~~~

## Como crear archivos y folder en powershell




### Create a file in the current directory
~~~
New-Item -Path . -Name "testfile1.txt" -ItemType "file" -Value "This is a text string."
~~~

### Create a directory

~~~
New-Item -Path "c:\" -Name "logfiles" -ItemType "directory"
~~~

### Create a directory in a different directory

The name of the new directory item, "Scripts", is included in the value of Path parameter, instead of being specified in the value of Name. As indicated by the syntax, either command form is valid.
~~~
New-Item -ItemType "directory" -Path "c:\ps-test\scripts"
~~~

### Remove a directory
~~~
Remove-Item 'D:\temp\Test Folder1'
Remove-Item 'D:\temp\Test Folder' -Recurse
~~~

### Read and write web config file

~~~
notepad (Get-WebConfigFile 'IIS:\Sites\Default Web Site')
~~~

~~~
# get the directory of this script file
$currentDirectory = [IO.Path]::GetDirectoryName($MyInvocation.MyCommand.Path)
# get the full path and file name of the App.config file in the same directory as this script
$appConfigFile = [IO.Path]::Combine($currentDirectory, 'App.config')
# initialize the xml object
$appConfig = New-Object XML
# load the config file as an xml object
$appConfig.Load($appConfigFile)
# iterate over the settings
foreach($connectionString in $appConfig.configuration.connectionStrings.add)
{
    # write the name to the console
    'name: ' + $connectionString.name
    # write the connection string to the console
    'connectionString: ' + $connectionString.connectionString
    # change the connection string
    $connectionString.connectionString = 'Data Source=(local);Initial Catalog=MyDB;Integrated Security=True'
}
# save the updated config file
$appConfig.Save($appConfigFile)
~~~

### Politicas de ejecucion de powershell

~~~
 Set-ExecutionPolicy -Scope LocalMachine -ExecutionPolicy RemoteSigned -Force
~~~

~~~
Set-ExecutionPolicy Unrestricted
~~~

### Working with git from powershell

~~~
Install-Module -Name posh-git -Force
Get-Module -Name posh-git -ListAvailable
~~~

Sql powershell

How substitute variable in PowerShell SQL query
https://stackoverflow.com/questions/53855001/how-substitute-variable-in-powershell-sql-query

~~~
function SQLQueryWriteToFile([string]$SQLquery, [string]$extractFile, [string]$facility)
{
   #create sql connection to connect to the sql DB
   $sqlConnection = New-Object System.Data.SqlClient.SqlConnection

   $sqlConnection.ConnectionString = "Server=blah;Database=blah_Test;User ID=blah;Password=blah" 
   $sqlConnection.Open()

   #Create a SqlCommand object to define the query
   $sqlCmd = New-Object System.Data.SqlClient.SqlCommand
   $sqlCmd.CommandText = $SQLquery
   $sqlCmd.Connection = $sqlConnection

   #create a SqlAdapter that actually does the work and manages everything
   $sqlAdapter = New-Object System.Data.SqlClient.SqlDataAdapter
   $sqlAdapter.SelectCommand = $sqlCmd
   $sqlAdapter.SelectCommand.CommandTimeout=300  #set timeout for query execution to 5 minutes (60x5=300)

   #create an empty dataSet for the query to fill with its results
   $dataSet = New-Object System.Data.DataSet

   #execute the query and fill the dataSet (then disconnect)
   $sqlAdapter.Fill($dataSet)
   $sqlConnection.Close()

   #dump the data to csv
   $DataSet.Tables[0] | Export-Csv $extractFile #this may not be comma delimited...need to check

} 

#start here

$SQLquery_Privilege = @"
SELECT *

 FROM "blah_Test".dbo.usr_Person_by_Privileges

WHERE 
       Status in ('Active')  
       and Facility = '$[facility]'
       and Last not like ('%test%')
       and Last not like ('%Test%')

--ORDER BY Last
"@
~~~