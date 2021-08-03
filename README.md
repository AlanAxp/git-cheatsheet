# git cheat sheet (Para dummies! 😉)

## Basico

Los comandos importantes que siempre debes tener a la mano

1. En el folder donde tienes creado el proyecto, abre una terminal y para iniciar git, solo escribe:

```basch
git init
```
2. Para anadir los archivos al staging area:

```bash
git add <file>
```

Anadir todos los archivos de una vez:

```bash
git add .
```

3. Para ignorar archivos al ejecutar `git add .`, y que no esten en el repositorio local/remoto crear un archivo llamado `.gitignore` en la raiz del proyecto.

```bash
# files
/file_I_want_to_ignore.rs 
/file_I_want_to_ignore2.py

# folders
/folder-I-want-to-ignore/
/folder/I/want/to/ignore/
```

4. Ver el estado de los archivos que estan en tu repositorio

```bash
git status
```


5. Cuando todo este correcto podemos hacer entonces el commit (Guardar los cambios en el staging area)

```bash
git commit -m "Ahora agregue esta modificacion "
```

La bandera `-m` significa que pasaras un mensaje que describa dichos cambios (tu futuro yo lo agradecera 😉)


6. Este proceso podra ocurrir repetidas veces conforme el proyecto crece. Entonces para poder ver el historial de cambios que se han realizado usamos

```bash
git log 
```
o de forma compacta

```bash
git log --oneline
```

## Ramas (branchs)

El proyecto empezara a crecer y en un punto querremos modificarlo sin querer danar alguna componente que ya funciona o para implementar algo nuevo sin temor de perder lo que ya teniamos

1. Para crear una rama en la cual podamos hacer todas las modificaciones, manteniendo segura esa version del proyecto, haremos


```bash
git branch <nombreNuevaRama>
```

Pero no tan rapido, antes de hacer una modificacion debemos asegurarnos que estamos en la rama correcta.

2. Para cambiar a otra rama del repositorio (este proceso se repetira tanto como lo necesites)

```bash
git checkout <nombreNuevaRama>
```

3. Para poder ver todas las ramas existentes en el repositorio local

```bash
git branch
```

### Borrar ramas

Si algo salio mal y la rama que hiciste arruina todo y quieres borrarlo de tu mente y de la faz de la tierra, entonces

4. Para borrar una rama en el repositorio local

```bash
git branch -d <ramaQueDesaparecera>
```

En el caso en el que no quierras borrar toda la rama, y solo regresar a un punto en el que el proyecto funcionaba bonis, podemos regresar a un commit especifico

5. Para regresar en el tiempo, a un commit especifico

```bash
git checkout <commitId>
```

6. Si quieres ver las diferencias entre commits, deberas ejecutar

```bash
git diff <commitId1> <commitId2>
```

7. Para revertir los cambios y fijar ese commit como punto de partida

```bash
git add .
git commit -m "Regresando al commit <commitId>"
git push
```
8. En el caso que solo estabas revisando el pasado del codigo sin querer revertir nada, puedes regresar al "presente" escribiendo

```bash
git checkout master
```

9. Para regresar a los cambios del ultimo commit 

```bash
git restore <file>
```

### Merges

Si en el caso contrario, el desarrollo en la nueva rama fue satisfactorio, y quieres que forme parte de la rama master (o de cualquier otra), debemos ejecutar los siguientes pasos

1. Primero deberas estar parado en la rama en la cual quieres "recibir" los cambios

```bash
git checkout <ramaQueRecibe>
```

2. Ejecutar el merge a la rama

```bash
git merge <ramaQueLLega>
```

### Renombrar rama

Si quieres cambiar el nombre de una rama que ya creaste

(Si estas parado en la rama que quieres renombrar)

```bash
git branch -m  <nuevoNombre>
```

(Si estas parado en una rama aparte)
```bash
git branch -m  <viejoNombre> <nuevoNombre>
```

## Repositorio remoto (GitHub/GitLab)

Pero... si tu computadora explota?

Nos gustaria estar seguros que tenemos un respaldo de nuestro trabajo en caso de que no podamos acceder a nuestras computadoras

Tanto en <a href="https://github.com/" target="_blank">GitHub</a> como en <a href="https://gitlab.com/" target="_blank">GitLab</a> puedes crear un repositorio remoto y clonar o solo clonar un repositorio ajeno y hacer

```bash
git clone <linkRepositorioRemoto>
```

1. Para subir cada commit que realices en tu repositorio deberas hacer lo que sigue

```bash
git add .
git commit -m "Al repo remoto alv"
git push -u origin <Rama>
```

(`origin` es el nombre predeterminado del repositorio git remoto desde el que clonaste.)

2. Para "descargar" los cambios que se hicieron al repo remoto

```bash
git pulll
```

Si está trabajando en una computadora y eliminas un archivo a un repositorio, cuando se haga push, ya no aparecerá. Pero si está trabajando desde otra computadora y desea eliminar los archivos que ya no están siendo rastreados por git, puedes hacer

```bash
git clean -fd
```

Si deseas actualizar el repositorio y estas ocupando otra computadora, o quieres estar seguro de que estará en el ultimo commit, ejecuta

```bash
git fetch  --all
git reset --hard origin/<ramaDelCommit>
```

Si quires eliminar una rama y que ya no aparezca en el repositorio remoto

```bash
git push origin --delete <nombreRama>
```

Si deseas cambiar el nombre de una rama que está en un repositorio remoto simplemente se debe eliminar esa rama remota y cargar la rama local con el nuevo nombre ... ¡duh!

Cuando estés en otra computadora, no veras todas las ramas que son remotas, pero por supuesto podrás verlas e interactuar con ellas, solo tienes que hacer

```bash
git remote update origin --prune
git branch -a
```
