---
Titulo: "Apuntes Docker"
---

# Apuntes Docker

**Comandos:**



~~~
docker info

docker-machine create -d hyperv --hyperv-virtual-switch "<NameOfVirtualSwitch>" <nameOfNode>
~~~

Otro ejemplo:
~~~
docker-machine create -d hyperv --hyperv-virtual-switch "Primary Virtual Switch" manager1
~~~
***Arrancar maquinas virtuales***
~~~
docker-machine start machine1
~~~
***Parar maquinas virtuales***
~~~
docker-machine stop machine1
~~~
***Listar maqinas virtuales***
~~~
docker-machine ls
~~~
***Conectar a una machina virtual***
~~~
docker-machine ssh machine1
~~~

***Bajar una imagen docker***
~~~
docker pull phusion/baseimage
~~~

***Crear una una instancia de docker e introducirse dentro de dicha instancia***
~~~
docker run --name=ubuntu-dev -it  ubuntu /bin/bash
~~~
~~~
docker run --name=ubuntu-dev-3 -d ubuntu
(Genera un nombre aleatorio de container)
~~~
Ejecutar una instancia de docker
~~~
docker exec -it ubuntu-dev /bin/bash
~~~

otra manera mas directa, genera una instancia y entras directamente a la instancia(genera un nombre aleatorio no hemos puesto el parameter --name)
~~~
docker run --interactive --tty ubuntu bash
~~~

***Lista de containers***

~~~
docker ps -a
docker container ls -all
~~~

Tutorial Docker - Comunicacion entre 2 Contenedores (Apache + MYSQL + PHP)

https://www.youtube.com/watch?v=EVUNz9UxQLA

