# GIT

[TOC]

## Qué es git

Git  es un sistema de control de versiones. Se encarga de trackear o tener un seguimiento sobre los cambios que se realizaron en un determinado archivo (o grupo de archivos). Todas las confirmaciones (commits) se guardan en un *repositorio* y algo muy interesante, es que se puede tener más de una versión de un proyecto junto a otra. A esto se lo conoce como *ramas* y git nos permite crear tantas ramas como se considere necesario, y luego volver a unirlas si así se desea.

Lo primero que hay que entender es que git tiene 3 áreas para el código:

1. El directorio en el que estas trabajando, es donde estan los archivos con el código. Ahi podes hacer lo que quieras
2. Staging, index o área de almacenamiento, que contiene los archivos que git tiene que trackear. Ahi es donde git se "fija" los cambios que hiciste y podes ver una comparación entre lo anterior y lo nuevo.
3. El head, o .git ,que es donde esta el codigo commiteado (mas adelante explico esto)

![Git – The Simple Guide | Damien FREMONT](https://damienfremont.files.wordpress.com/2015/09/trees.png)

### Commit

#### Que es

Un commit es, básicamente, una fotografía de la carpeta de nuestro proyecto en un momento determinado. Cuando hacemos un commit, estamos congelando el estado de todos los archivos y subdirectorios, y guardando la imagen en un histórico. Al comenzar a usar Git, un error muy común es tenerlo como un simple sistema de backups: una práctica habitual al principio es pensar en los commits como un CTRL-S masivo sobre todos nuestros archivos. «Voy a ir guardando esto para que no se pierda» nunca debería ser el pensamiento que preceda a la creación de un commit.

Internamente un commit almacena referencias a archivos y directorios, y cada commit nuevo tiene como base el anterior, y ese del anterior, y ese del anterior, asi hasta el primero  que se hizo. 

### Antes del commit

Como se ve en la foto anterior, el primer paso antes de hacer un commit, es agregar el archivo al area de staging (o index) utilizando `git add nombreArchivo`. De esta manera, git va a poder hacer el seguimiento de los cambios que se efectuen en el mismo. Tambien se puede usar `git add *` para agregar todos los archivos nuevos.

**NOTA:**  si el archivo ya existia en el repositorio **no** es necesario agregarlo al .git (ya esta ahí).

Otra cosa que se puede hacer antes de hacer un `commit  `  es ver que cosas van a commitearse, para eso se utiliza `git diff -r HEAD`. El flag `-r` significa "compara con una revision particular" y `HEAD` es "el commit mas reciente".

#### Cada cuanto hacer un commit

¿Cada cuánto tiempo deberíamos crear un commit ? ¿Al final del día? ¿Tres veces a la semana? ¿Después de cada función o método creado? La realidad es que no deberíamos usar una medida temporal. **Deberíamos crear un commit cuando queramos añadir un nuevo hito al listado de cambios del proyecto.** Por lo tanto, tenemos que pensar en cómo será el histórico del proyecto dentro de unas semanas o meses, y decidir si entre toda la maraña de cambios que se han ido registrando debería aparecer un punto con el estado actual de nuestro código.

#### Como hacer un commit

Ahora sí podemos ver *cómo* hacer un commit. Para eso se utiliza el comando `git commit`. En este momento Git nos va a pedir un mensaje que describa el cambio que hicimos. Este mensaje tiene que ser preciso y claro sobre el cambio que se hizo. Esto es **SUPER** importante por si después hay que volver a una versión anterior, es más fácil identificar cuál es esa version si el mensaje de commit fue claro.

Para hacer un commit con el mensaje ya incluido podemos usar el flag `-m` y usarlo de la siguiente manera: `git commit -m "agregue funcion que valida numeros"`.

Si te equivocaste de mensaje o tipeaste algo mal, se puede usar el flag `--amend` de la siguiente manera: `git commit --amend - m "feature: Agregado de funcion que valida numeros enteros"`.

Una **buena practica** es estructurar el mensaje del commit de la siguiente manera:

* Tipo: asunto
* Cuerpo (opcional)

**Tipo** 

- **feat o feature:** Una nueva caracteristica.
- **fix:** Se soluciono un bug.
- **docs:** Se realizaron cambios en la documentacion.
- **style:** Se aplico formato, comas y puntos faltantes, etc. Sin cambios en el codigo.
- **refactor:** Refactorizacion del codigo en produccion.
- **test:** Se añadieron pruebas, refactorizacion de pruebas. Sin cambios en el codigo.
- **chore:** Actualizacion de tareas de build, configuracion del admin. de paquetes. Sin cambios en el codigo.

**Asunto:** no debe contener mas de 50 caracteres, debe iniciar con una letra mayuscula y no terminar con un punto. A la hora de escribir el asunto del commit tenemos que ser imperativos, hay que ser objetivos y otra cosa importante a la que tenemos que acostumbrarnos es a escribirlos en **ingles**.

*Nota:*  cuando hablo de ser imperativos hago referencia a este sencillo ejemplo: usar **change** en lugar de "changed" o "changes". En español seria **cambio** en lugar de "cambié" o "cambios"

**Cuerpo: ** no todos los commits son lo suficientemente complejos como para necesitar de un cuerpo, es opcional y se usan en caso de que el commit requiera una explicacion y contexto. El primer párrafo del cuerpo es el resumen, y los siguienes son en sí el cuerpo. Utilizamos el cuerpo para explicar el ¿qué y por qué? de un commit y no el ¿cómo? Al escribir el cuerpo, requerimos de una linea en blanco entre el titulo y el cuerpo, ademas debemos limitar la longitud de cada linea a no mas de 72 caracteres.

#### Mensaje de ejemplo

```
Type and subject
feature: Summarize changes in around 50 characters or less

Summary
More detailed explanatory text, if necessary. Wrap it to about 72 
characters or so. In some contexts, the first line is treated as the 
subject of the commit and the rest of the text as the body. 

Body
The blank line separating the summary from the body is 
critical (unless you omit the body entirely); 
various tools like `log`, `shortlog` and `rebase` can get 
confused if you run the two together. 

Explain the problem that this commit is solving. 
Focus on why you are making this change as oppose
to how (the code explains that). 

Are there side effects or other unintuitive consequenses of this change?
Here's the place to explain them.
Further paragraphs come after blank lines.
    
If you use an issue tracker, put references to them at the bottom, like this:

Resolves: #123 
See also: #456, #789
```

En español

```
Tipo y asunto
feature: Resumen de la nueva característica en 50 caracteres o menos

Resumen del cuerpo
Si fuera necesario agregar más contenido, acá iría un resumen del cambio que se hizo (aproximadamente 70/80 caracteres).

Cuerpo
Luego de una linea en blanco se puede explicar el problema que se resuelve con este commit. Repito lo mismo de antes, acá no se explica el cómo (eso lo hace el código) se explica el por qué.

Si se necesitaran agregar más párrafos (como las consecuencias del cambio, etc.) se hacen en párrafos nuevos separados por una línea en blanco.

En el caso de utilizar el issue tracker al final del commit hay que poner las referencias de los issues que se están resolviendo. Algo como:

Resuelve: #123 
Ver: #456, #789
```

Los mensajes que puse de ejemplo son largos, pero no siempre es necesario todo eso. Una versión más simple podría ser:

```
feature: Agregado de clase Vehiculo
feature: Add Vehicle class
```

### Ver cambios

#### Status

`git status` muestra una lista de todos los archivos que fueron modificados desde la ultima vez que los cambios fueron guardados

#### Diff

`git diff` muestra todos los cambios del repositorio. Se le puede agregar `nombreArchivo` o `nombreDirectorio` para ver cambios mas puntuales

Supongamos que la salida de `git diff` es:

```
diff --git a/reporte.txt b/reporte.txt
index e713b17..4c0742a 100644
--- a/reporte.txt
+++ b/reporte.txt
@@ -1,4 +1,5 @@
-# Cirujias Dentales Temporada 2017-18
+# Cirujias Dentales Temporada (2017) 2017-18
+# TODO: escribir nuevo resumen
```

* `a` y `b` son "la primera version" y "la segunda version" respectivamente.
* `--- a/report.txt` y `+++ b/report.txt`, cuando una linea es removida lleva adelante un `-` y cuando una linea es agregada lleva un `+`.
* Las lineas que empiezan con `@@` indican *donde* los cambios se estan realizando. En este caso indica que los cambios empiezan en la linea 1, y que ahora tiene 5 lineas donde antes habia 4.
* Las ultimas tres lineas son cosas que se sacaron (`-`) y se agregaron (`+`)

#### Log

El comando `git log` sirve para ver el registro de todos los commits que se hicieron, muestra desde el mas reciente hasta el mas antiguo y se ve algo asi

```c++
commit 0cf36a0dcd5f7334f07465f57e5242493ad587dd
Author: valva-ro <vavarela.rodriguez@gmail.com>
Date:   Wed May 20 00:06:09 2020 -0300

    feature: Agregado 3 categorias nuevas

commit 10e38538776d75d08f8b444003cec22d92576798
Author: valva-ro <vavarela.rodriguez@gmail.com>
Date:   Tue May 19 22:53:46 2020 -0300

    style: Agregado de ; y comentarios

commit 58d0556f1259e7d4be8dd7a02255b8ffedc55c9e
Author: valva-ro <vavarela.rodriguez@gmail.com>
Date:   Tue May 19 17:42:56 2020 -0300

    feature: Agregado de atributo letrasErroneasIngresadas y metodo obtenerLetrasErroneasIng
```

**NOTA:** para ver el registro de un directorio o archivo particular se puede agregar el la ruta `git log ruta`.

El numero largo que acompaña al commit se llama *hash*, y es algo que Git generará a partir del contenido que almacenemos en el valor correspondiente. Esto significa que, a mismo valor, misma clave *hash* generada.

Luego se muestra el autor, la fecha en la que se hizo el commit y el mensaje del mismo.

#### Show

El comando `git show` se utiliza acompañado de los primeros 4 caracteres del *hash* y sirve para mostrar los detalles de ese commit especifico. Seria una unión entre lo que muetra `git log` y `git diff`. Por ejemplo `git show 58d0` (que fue el último commit que hice antes) muestra:

```c++
commit 58d0556f1259e7d4be8dd7a02255b8ffedc55c9e
Author: valva-ro <vavarela.rodriguez@gmail.com>
Date:   Tue May 19 17:42:56 2020 -0300

    Agregado de atributo letrasErroneasIngresadas y metodo obtenerLetrasErroneasIngresadas.
    
    Se agrego el atributo letrasErroneasIngresadas para poder tener un registro de las letras erroneas que ingresó el usuario y de esta manera no restarle una vida al jugador si decidera ingresar una letra repetida

diff --git a/Ahorcado.cpp b/Ahorcado.cpp
index 3f6866d..a348c1d 100644
--- a/Ahorcado.cpp
+++ b/Ahorcado.cpp
@@ -10,6 +10,7 @@
 Ahorcado:: Ahorcado() : palabraAAdivinar(0), palabraSecreta(0) {
     estadoJuego = EMPEZO_JUEGO;
+    letrasErroneas = "";
 }
```

Ahora bien, utilizar el *hash* sería el equivalente a escribir la ruta absoluta. También se puede utilizar la ruta relativa escribiendo `HEAD` que se refiere al commit más reciente. `HEAD~1` es el anterior a ese, `HEAD~2` el anterior y así sucesivamente.

### Como ignorar ciertos archivos

En general cuando estamos programando, creamos archivos de prueba que no queremos agregar al proyecto. O quizas nuestro IDE crea automaticamente ciertos archivos (como CLion que utiliza CMake para compilar proyectos de C/C++). Para que Git no tenga en cuenta esos archivos, hay que crear uno que se llame `.gitignore` en el directorio del repositorio.

Ejemplo de `.gititnore` 

```c++
test
*.txt
```

Luego, Git va a ignorar todos los archivos o carpetas que se llamen `test`, y todos los archivos que terminen en `.txt`. 

## Como sacar archivos del repositorio local

`git clean -n` te muestra una lista de archivos que estan en el repositorio, pero que Git no esta trackeando actualmente.

`git clean -f` borra los archivos que muestra el comando anterior. **Ojo** porque `git clean` funciona solo con archivos (o rutas) que no están siendo trackeados, por lo tanto si los borras **no se pueden recuperar.**

## Como deshacer algo

`git reset` reestablece el HEAD sin tocar el tree de rtabajo.

`git checkout` cambia el tree de trabajo sin tocar el índice

Pero dependiendo de como se llamen o que flags se les agreguen, pueden hacer lo mismo, como por ejemplo 

`git checkout -- rutaDelArchivo`  y `git reset HEAD rutaDelArchivo`

## Resumen comandos básicos en imagen

![Git 簡介- Po-Ching Liu - Medium](https://miro.medium.com/max/1024/0*RHr7xef9NozKrFD7.png)

## Ramas

Las ramas nos permiten tener múltiples versiones de un programa y trackearlas en simultaneo. La rama principal se llama `master` y si bien hay muchas variantes en el uso de ramas, lo más común es tener las siguientes

* **master:** nunca se sube nada directo a esta rama. Se trabaja en ramas separadas y después se mergea
* **develop:** en esta rama es donde vamos a empezar a desarrollar el código, de acá van a salir las ramas *feature*
* **feature:** hay una para cada caracteristica. Una vez que ya está lista la feature se mergea a develop (o a master)

- **fix:** si alguna rama tiene un bug, se saca una nueva para solucionarlo y después se mergea

![image-20200714154417050](https://i.loli.net/2020/07/15/xPBuA7yd6kGXqET.png)



Una vez que se terminó el desarrolo de una rama, es una buena práctica:

1. Abrir un PR (Pull Request) 
2. Que otros miembros del equipo lo revisen y comenten
3. Si alguien del equipo sugirió algún cambio habría que llegar a un acuerdo y ver si se hacen o no modificaciones. En el caso de decidir modificar algo, habría que hacer un commit y un push con esos cambios (esto va a aparecer en el mismo PR, no hace falta abrir uno nuevo)
4. Repetir 2 y 3 hasta que este todo ok y queden todos conformes
5. Aprobar el PR
6. Mergear
7. Borrar la rama utilizada

Por ejemplo, si de master saco una rama `develop-transporte` y después saco de esa una que se llame `feature-validaciones-sube`, cuando termine de desarrollar las validaciones de la sube, tendría que commitear, pushear y abrir un PR para mergear a la rama `develop-transporte`. En este caso no me interesa mergear a `master` todavía porque faltan desarrollar otras cosas relacionadas con el transporte y recién cuando se termine eso se va a mergear `develop-transporte` a `master`. Una vez abierto el PR mis compañeros  deberían revisar el código y decirme si creen o no que hay que modificar cosas. Cuando ya este todo bien, mi equipo va a tener que aprobar el PR para poder mergear a `develop-transporte`. Aprobado el PR, se mergea y después se borra la rama `feature-validaciones-sube`.