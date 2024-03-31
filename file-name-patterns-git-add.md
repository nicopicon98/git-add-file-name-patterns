# Patrones de nombres de archivo para `git add`

Git es un sistema de control de versiones distribuido que permite a los desarrolladores colaborar en proyectos de software. Uno de los comandos más utilizados en Git es `git add`, que agrega cambios en el directorio de trabajo al área de preparación (staging area) para ser incluidos en el próximo commit.

### Agregar todos los archivos

```sh
git add .
```

Esto agregará todos los archivos modificados y nuevos en el directorio actual al área de preparación.

o

```sh

git add -A
```

o 

```sh

git add --all
```

o 

```sh

git add -u
```

o 

```sh

git add *
```

La diferencia entre `git add .` y `git add -A` es que el primero no agrega archivos eliminados, mientras que el segundo sí lo hace. `git add -u` solo agrega archivos modificados o eliminados, pero no nuevos archivos. `git add *` agrega todos los archivos en el directorio actual, pero no los que están en subdirectorios. 

Si deseo agregar todos los archivos, incluyendo los que están en subdirectorios, puedo usar:

```sh

git add */*
```

## Agregar archivos específicos

### Agregar todos los archivos que comienzan con "init":

```sh
git add init*
```
Esto agregará archivos como init-config.js, initialize.py, etc., en el directorio actual.

Agregar todos los archivos .js que se encuentran en cualquier subdirectorio dentro de src/:

git add src/**/*.js
Esta sintaxis es útil para repositorios con estructuras de directorios profundas.

Agregar todos los archivos que terminan en .test.js para agregar tests específicos de JavaScript:

git add *test.js
Ideal para cuando solo quieres stagear tus tests después de hacer cambios o añadir nuevos.

Agregar todos los archivos excepto aquellos que terminan en .log (usando Git Bash o un shell Unix-like):

git add . && git reset -- '*.log'
Primero agregas todo, luego excluyes los archivos .log del stage.

Agregar archivos modificados que no sean nuevos (no untracked):

git add -u
Esto solo agrega al stage archivos que ya estaban siendo rastreados y que han sido modificados, excluyendo nuevos archivos (untracked).

Agregar todos los archivos README.md en cualquier parte del repositorio:

git add **/README.md
Útil para actualizar descripciones o documentación del proyecto en varios lugares.

Agregar todos los archivos modificados o eliminados, pero no nuevos archivos, en un subdirectorio específico (ej. docs/):

git add -u docs/
Esto se enfoca en actualizar la documentación existente sin añadir nuevos archivos a la documentación.

Agregar todos los archivos cuyos nombres contienen un número:

git add *1* *2* *3* *4* *5* *6* *7* *8* *9* *0*
Añade archivos como chapter1.md, 2020-logs.txt, etc., útil para cuando los nombres de archivo siguen un patrón numérico.

Agregar todos los archivos Python modificados recientemente, limitando a los 5 más recientemente modificados (usando Unix-like commands):

git ls-files -m | grep '\.py$' | xargs stat --format="%Y %n" | sort -n | cut -d' ' -f 2- | tail -n 5 | xargs git add
Este comando es una combinación de comandos Unix y Git para filtrar, ordenar por fecha de modificación, y limitar la cantidad de archivos.

Agregar todos los archivos excepto aquellos en un directorio específico (por ejemplo, excluyendo node_modules/):

git add $(git ls-files -o --exclude-standard | grep -v '^node_modules/')
Utiliza git ls-files para listar todos los archivos no rastreados (excluyendo los ignorados por .gitignore), filtra aquellos en node_modules/, y los agrega.