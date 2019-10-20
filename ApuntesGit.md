#Apuntes Git
___
Pasos para crear una nueva rama

Primero bajarnos a nuestro local, los ultimos cambios
<pre>
git pull
</pre>
Creamos a nueva rama en nuestra maquina local
<pre>
git checkout -b nombre de la nueva rama
esto es una atajo a:
git branch nombre nueva rama(crear nueva rama)
git checkout nombre nueva rama(situarse en la nueva rama)
</pre>
Hacer push de la rama en github
<pre>
git push origin nombre nueva rama
</pre>
Queremos ver todas las ramas creadas
<pre>
git branch -a
</pre>



___
Crear un repositorio local y subir los cambios
<pre>
git init

git add .
git commit -m "first commit"

git remote add origin https://github.com/andrespallareslopez/prueba45.git
git push -u origin master

</pre>
___
CREAR RAMAS CON GIT

Vamos a crear una nueva rama
<pre>
git branch test
</pre>
Cambiar de rama activa
<pre>
git checkout test
</pre>
Si acabamos con la rama test el comando para borrar la rama
<pre>
git branch -d test
</pre>

Si hubiera algun error y hubiera que forzar el borrado
<pre>
git branch -D test
</pre>
Para eliminar el repositorio remosto git push origin
<pre>
git push origin :test
</pre>

___
MEZCLANDO RAMAS
Para realizar la mezcla de la rama nuevafuncionalidad dentro de master vamos a situarnos en la rama mater y a mezclar ambas:
<pre>
git checkout master
git merge nuevafuncionalidad
</pre>
Una vez mergeado ya no necesitamos la rama creada nuevafuncionalidad, entoces la podemos borrar:
<pre>
git branch -d nuevafuncionalidad
</pre>
Todo esto ocurre en nuestro local
___
Subiendo ramas al repositorio remoto
<pre>
git push origin nombre de la nueva rama
</pre>
para borrar una rama remota
<pre>
git push origin :rama_a_borrar
</pre>
___
¿que es una pull request?

Una Pull Request es la acción de validar un código que se va a mergear de una rama a otra. En este proceso de validación pueden entrar los factores que queramos: Builds (validaciones automáticas), asignación de código a tareas, validaciones manuales por parte del equipo, despliegues, etc

___


___
Clonar o bajar un repositorio

<pre>
git clone https://github.com/andrespallareslopez/mynotes.git
</pre>

Añadir el nombre de un archivo

<pre>
git add <span>nombre de archivo</span>
</pre>

Ver el estatus del archivo
<pre>
  git status
</pre>

Eliminar el archivo
<pre>git rm nombre del archivo</pre>

Confirmar los cambios (Commit)

<pre>git commit -m 'comentario'</pre>

Ver los logs de git
<pre>git log</pre>

Enviar los cambios que se han hecho en la rama principal de los repositorios que estan 
asociados con el directorio que se esta trabajando.

Basicamente lo que realiza un push es publicar lo que se encuentra en nuestro servidor 
local y llevarlo al servidor remoto de Github.

<pre>
git push origin master
</pre>
El pull trae los cambios de nuestro repositorio remoto y los actualiza al repositorio local.
<pre>
git pull
</pre>
El comando git se usa para conectar a un repositorio remoto.
<pre>
git remote add origin 'ip o dns'
git remote -v
</pre>
Crear una rama (branch) con la option -b
<pre>
git checkout -b nombrerama
</pre>
o para cambiar de una rama a otra tambien se utiliza *checkout*
<pre>git checkout nombre rama</pre>
Este comando se usa pra listas , crear o borrar ramas. Para listar
todas las ramas se usa:
<pre>git branch</pre>
para borrar la rama
<pre>git branch -d nombre rama</pre>
Tambien podemos crear una rama con *branch*
<pre>git branch nombre rama</pre>




