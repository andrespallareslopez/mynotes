# Apuntes Packer

Tenemos tambien otra herramienta basada en packer llamada Azure Image Builder.

Este tutorial esta basado en la herramienta packer para crear imagenes, no en azure image builder.

Creacion de una imagen con windows server en azure con packer





___

Automation with Hashicorp Packer #9: Azure Image & multiple providers

https://www.youtube.com/watch?v=JzFS8l0xNRQ&list=PL8VzFQ8k4U1Jp6eWgHSXHiiRWRvPyCKRj&index=10

____

How to use Packer to build a Windows Server Image for Azure

https://gmusumeci.medium.com/how-to-use-packer-to-build-a-windows-server-image-for-azure-52b1e14be2f2


___

Crea imágenes customizadas de máquinas virtuales de Azure con Packer

https://recetasdevops.com/crea-imagenes-customizadas-de-maquinas-virtuales-de-azure-con-packer/


Arrancar la consola en modo administrador

Para poder ejecutar comandos sin ningun problema
<pre>
Set-ExecutionPolicy Bypass -Scope Process -Force

</pre>
Nos autenticamos

<pre>
az login
</pre>

comprobamos los datos de la cuenta y sus parametros, que nos haran falta
<pre>
az account show
</pre>


creamos un grupo de recursos:

<pre>
az group create -n packer -l francecentral
</pre>

borrar un grupo de azure
<pre>
az group delete -n nombregrupo
</pre>


Obtener las maquinas virtuales  con sistema operativo microsoft

<pre>
az vm image list --publisher Microsoft --location francecentral -o table
</pre>

Obtener el sku

<pre>

</pre>








___





