---
Titulo: "Apuntes Kubernetes"
---

# Apuntes KuberneteS


(Win 10)
Podemos bajar nuestro instable de kubernetes minikube en el directorio Minikube_home para ejecutar y levantar kubertes.
Si es la primera vez dentro de este directorio se bajar archivos y establecera cosas.


En nuestra maquina local cuando instalemos kubernetes(minikube) tenemos que establecer la variable de entorno de MINIKUBE_HOME
 a disco c: porque si lo hacemos a otra unidad D: o E: vamos a tener problemas 

El ejecutable de minikube tambien nos lo podemos bajar y ponerlo en un directorio espeficico y registrar dicho direcctorio en variables de entorno.

**How to set up Kubernetes on Windows 10 with Docker for Windows and run ASP.NET Core**


https://www.hanselman.com/blog/HowToSetUpKubernetesOnWindows10WithDockerForWindowsAndRunASPNETCore.aspx

**04. Deploying into local Kubernetes in Windows 10 and Docker for Windows development environment**

https://github.com/dotnet-architecture/eShopModernizing/wiki/04.-Deploying-into-local-Kubernetes-in-Windows-10-and-Docker-for-Windows-development-environment

**Getting Started With Kubernetes On Windows 10 Using HyperV And MiniKube**

https://www.c-sharpcorner.com/article/getting-started-with-kubernetes-on-windows-10-using-hyperv-and-minikube/

**Minikube on Windows 10 with Hyper-V(importante)**

En este articulo nos muestra como instalar y arrancar minikube en linea de comandos con hyperv

https://medium.com/@JockDaRock/minikube-on-windows-10-with-hyper-v-6ef0f4dc158c


**Arrancar un minikube**

~~~
minikube start --vm-driver="hyperv"

minikube start --vm-driver=hyperv --hyperv-virtual-switch="primaryswitch"
~~~

Con este comando creara un directorio a partir de la variable de entorno que hemos definido, si es la primera vez se bajara una imagen y
definira cosas.

Como decimos a principio de este documento tenemos que hacer todo esto en c:


**Comprobar minikubes**

~~~
minikubes status
~~~
Informacion del cluster
~~~
kubectl cluster-info
~~~

Parar un cluster

~~~
minikube stop
~~~

Si esta instruccion no funcionara meterse dentro de hyperv y dentro del cluster autentificarse como root
y poner *poweroff*

Como mostrarnos todos los addons activos en un cluster:

~~~
minikube addons list
~~~
Como mostrarnos el dashboard en navegador

~~~
minikube dashboard
~~~
____
Mostrar logs de kubernetes de un pod
~~~
kubectl log nginx(<-nombre del contenedor creado en kubernetes)
~~~


Putting the ".NET" into "Kubernetes"

https://www.youtube.com/watch?v=GBOPBfcJ2zM


