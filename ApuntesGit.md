#Apuntes Git

Crear un repositorio local
<pre>
git init

git add .
git commit -m "first commit"

git remote add origin https://github.com/andrespallareslopez/prueba45.git
git push -u origin master

</pre>

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




