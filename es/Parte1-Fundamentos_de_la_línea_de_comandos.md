# Parte1-Fundamentos_de_la_línea_de_comandos.md

# **Conceptos básicos de la línea de comandos**

## **¿Qué es la Interfaz de Línea de Comandos?**

Debajo de la maravillosa Interfaz Gráfica de Usuario ("GUI") de Mac se encuentra un método poderoso y flexible de trabajar directamente con archivos y la web. Esto es conocido como la "interfaz de línea de comandos", o a veces "CLI".

Puede parecer geek al principio, y su profundidad puede ser intimidante, pero no necesitas aprender todo para que la línea de comandos te sea bastante útil. En particular, para aprender a programar aplicaciones web o clientes de manera efectiva en Mac, necesitarás tener algo de comodidad con los conceptos básicos de la línea de comandos de Mac.

## **El Terminal, la Consola, el Shell y la Línea de Comandos**

Primero, deberías aprender cómo iniciar la aplicación incorporada que ejecuta el CLI de Mac, llamada *Terminal*. Para lanzarla, en lugar del método GUI habitual de abrir el directorio Aplicaciones/Utilidades y hacer doble clic en la aplicación Terminal, en cambio, deberías aprender a lanzar el Terminal únicamente utilizando tu teclado.

Escribe **`command + spacebar`** y luego escribe **`terminal`** y presiona return. De hecho, ni siquiera necesitas escribir la palabra completa, generalmente con las primeras letras **`ter`** o **`term`** es suficiente.

Cuando el Terminal se abre por primera vez, deberías ver una pequeña ventana con este texto en ella:

```markdown
Last login: {alguna fecha} on console
COMPUTERNAME:~ USERNAME$ 🁢
```

La ventana que ves es creada por la aplicación *Terminal*, que más correctamente es una forma de *emulador de terminal* y su contenido (cualquier comando y el texto de salida de comandos anteriores) es conocido como *consola*. Estas palabras provienen de los días en que tenías una pantalla CRT verde y un teclado: la máquina en su conjunto era el *terminal*, y el contenido de la pantalla era la *consola*. Nuestro *emulador de terminal* nos proporciona la experiencia de escribir en un antiguo terminal desde la comodidad de nuestro sistema operativo gráfico moderno.

El texto antes y hasta el $ es conocido como *prompt*. La *línea de comandos* es todo después del prompt actual, y es la parte de la consola donde puedes escribir.

El símbolo 🁢 es la ubicación de tu *cursor de texto* en la línea de comandos. Todo lo que escribas aparecerá debajo del cursor de texto y el cursor de texto se moverá al siguiente lugar.

Todo el texto que ves en la consola fue creado por lo que se conoce como la aplicación *shell* (Mac por defecto usa la aplicación shell conocida como *bash*).

A menudo las palabras terminal, consola, línea de comandos, shell o bash se usan indistintamente, pero cada una de estas son ligeramente diferentes.

Algún día tal vez quieras cambiar a aplicaciones de Terminal más sofisticadas (*iTerm* es popular), o cambiar a un shell de texto más sofisticado (*tsch* es popular), o ambos. Para el propósito de este tutorial *Intro a la Línea de Comandos* solo estaremos usando la aplicación Mac *Terminal* por defecto, y el shell de línea de comandos de texto *bash*.

## **Ejecutando un Comando**

Si ahora escribes el texto **`ls -l ~`** verás el texto aparecer a la derecha del $. Este es tu *comando*. Escribe return para *ejecutar* tu comando.

```markdown
COMPUTERNAME:~ USERNAME$ ls -l ~
total 0
drwx------+  3 USERNAME  staff   102 Oct 21 18:44 Desktop
drwx------+  3 USERNAME  staff   102 Oct 21 18:44 Documents
drwx------+  3 USERNAME  staff   102 Oct 21 18:44 Downloads
drwx------@ 43 USERNAME  staff  1462 Apr 12 00:15 Library
drwx------+  3 USERNAME  staff   102 Oct 21 18:44 Movies
drwx------+  3 USERNAME  staff   102 Oct 21 18:44 Music
drwx------+  3 USERNAME  staff   102 Oct 21 18:44 Pictures
drwxr-xr-x+  5 USERNAME  staff   170 Oct 21 18:44 Public
COMPUTERNAME:~ USERNAME$ 🁢
```

Casi todos los comandos siguen un patrón común con 3 partes principales. El programa, las opciones y los argumentos, cada uno separado por espacios.

El programa es el verbo, en este caso la primera parte **`ls`**, que es corto para *listar*, que nos mostrará una lista de archivos.

Las opciones son como el adverbio, y modifican cómo se ejecuta el programa. Las opciones casi siempre comienzan con un guion. En este ejemplo **`-l`** significa *largo*, así que el comando **`ls`** ahora nos mostrará más información detallada en lugar de solo los nombres de los archivos.

Los argumentos son lo que queda, y son los objetos de nuestro comando. Describen lo que queremos que nuestro programa actúe. En este caso estamos usando un nombre especial abreviado para nuestro directorio hogar **`~`**.

Combinados, estas tres partes le dicen al computador listar, en forma larga, el contenido de tu directorio hogar.

## **El Directorio Actual**

Cuando ingresas muchos comandos sin ningún argumento, actuarán por defecto en el directorio actual (también conocido como carpeta). ¿Qué es el directorio actual? Escribe **`pwd`**.

```markdown
COMPUTERNAME:~ USERNAME$ pwd
/Users/USERNAME
COMPUTERNAME:~ USERNAME$ 🁢
```

El comando **`pwd`** es corto para 'present working directory' que básicamente significa "¿Dónde estoy ahora?". El resultado de **`pwd`** es el *camino* a donde cualquier comando sin argumentos actuará por defecto.

```markdown
COMPUTERNAME:~ USERNAME$ ls
Desktop		  Downloads	  Movies		Pictures
Documents	  Library		  Music		  Public
COMPUTERNAME:~ USERNAME$ 🁢
```

Nota que el comando **`ls`** nos mostró un directorio adicional que no puedes ver desde la GUI de Finder de Mac: el directorio Library. Puede haber otros archivos invisibles. Podemos ver estos agregando al comando **`ls`** una opción, en este caso **`-a`**. Juntos el comando y la opción **`ls -a`** significan 'listar todo'.

```markdown
COMPUTERNAME:~ USERNAME$ ls
.			  			  		Desktop			Movies
..									Documents		Music
.CFUserTextEncoding	Downloads		Pictures
.Trash			Library			Public
COMPUTERNAME:~ USERNAME$ 🁢
```

El comando 'ls -a' revela una serie de directorios y archivos que están marcados como invisibles para Finder y la GUI de Mac. Cualquier archivo o directorio que comience con un punto también será invisible para Finder. Aprenderemos más sobre estos archivos más tarde.

Para mirar el contenido de otro directorio, puedes agregar una opción de *camino* al comando **`ls`**. Escribe **`ls Public`** para ver el contenido de tu directorio Public (el nombre del directorio **`Public`** distingue entre mayúsculas y minúsculas: **`public`** no funcionará).

```markdown
COMPUTERNAME:~ USERNAME$ ls Public
Drop Box
COMPUTERNAME:~ USERNAME$ 🁢
```

El comando **`ls -l`** (es decir, **`listar largo`**) lista información adicional sobre cada ítem en el directorio actual:

```markdown
COMPUTERNAME:~ USERNAME$ ls -l
total 0
drwx------+  3 USERNAME  staff   102 Oct 21 18:44 Desktop
drwx------+  3 USERNAME  staff   102 Oct 21 18:44 Documents
drwx------+  3 USERNAME  staff   102 Oct 21 18:44 Downloads
drwx------@ 43 USERNAME  staff  1462 Apr 12 00:15 Library
drwx------+  3 USERNAME  staff   102 Oct 21 18:44 Movies
drwx------+  3 USERNAME  staff   102 Oct 21 18:44 Music
drwx------+  3 USERNAME  staff   102 Oct 21 18:44 Pictures
drwxr-xr-x+  5 USERNAME  staff   170 Oct 21 18:44 Public
COMPUTERNAME:~ USERNAME$ 🁢
```

Con la opción **`-l`** la **`d`** a la izquierda te dice que el ítem en el directorio contiene otro directorio. Un guion **`-`** te dice que el ítem es un archivo.

Puedes combinar opciones, así que **`ls -la`** listará toda la información sobre todo el contenido del directorio actual, incluyendo archivos ocultos con punto **`.`** y directorios invisibles como **`Library`**.

```markdown
COMPUTERNAME:~ USERNAME$ ls -l
total 8
drwxr-xr-x+ 14 USERNAME  staff   476 Apr 12 12:39 .
drwxr-xr-x   6 root          admin   204 Oct 21 18:44 ..
-r--------   1 USERNAME  staff     7 Oct 21 18:46 .CFUserTextEncoding
drwx------   2 USERNAME  staff    68 Apr 11 23:27 .Trash
drwx------+  3 USERNAME  staff   102 Oct 21 18:44 Desktop
drwx------+  3 USERNAME  staff   102 Oct 21 18:44 Documents
drwx------+  3 USERNAME  staff   102 Oct 21 18:44 Downloads
drwx------@ 43 USERNAME  staff  1462 Apr 12 00:15 Library
drwx------+  3 USERNAME  staff   102 Oct 21 18:44 Movies
drwx------+  3 USERNAME  staff   102 Oct 21 18:44 Music
drwx------+  3 USERNAME  staff   102 Oct 21 18:44 Pictures
drwxr-xr-x+  5 USERNAME  staff   170 Oct 21 18:44 Public
COMPUTERNAME:~ USERNAME$ 🁢
```

También puedes agregar el nombre de un directorio como un argumento para ver el contenido de ese directorio, por ejemplo **`ls -la Public`**

```markdown
COMPUTERNAME:~ USERNAME$ ls -la Public
total 0
drwxr-xr-x+  5 ChristopherA  staff  170 Oct 21 18:44 .
drwxr-xr-x+ 13 ChristopherA  staff  442 Apr 12 12:41 ..
-rw-r--r--   1 ChristopherA  staff    0 Oct 21 18:44 .com.apple.timemachine.supported
-rw-r--r--   1 ChristopherA  staff    0 Oct 21 18:44 .localized
drwx-wx-wx+  3 ChristopherA  staff  102 Oct 21 18:44 Drop Box
COMPUTERNAME:~ USERNAME$ 🁢
```

## **Completación con Tabulador**

Una característica útil que ofrece la línea de comandos se llama "completación de línea de comandos" o "completación con tabulador". Esto significa que si ingresas información insuficiente sobre un argumento, puedes presionar la tecla **`tab`** para ver cuáles son las opciones, o si solo hay una opción, seleccionar esa.

Pruébalo escribiendo **`ls M`** luego presiona la tecla **`tab`** en lugar de return.

```markdown
COMPUTERNAME:~ USERNAME$ ls M→
Movies/ Music/
COMPUTERNAME:~ USERNAME$ ls M🁢
```

En este caso hay dos ítems que comienzan con M, por lo que la línea de comandos los lista ambos y retiene el texto que comenzaste. Ahora agrega una letra más, **`o`** y presiona la tecla **`tab`**:

```markdown
COMPUTERNAME:~ USERNAME$ ls Movies/🁢
```

Solo había un ítem que comenzaba con **`Mo`**, el directorio Movies. Si presionas **`return`** verás el contenido de esa carpeta.

La completación con tabulador es muy útil para nombres de archivos que tienen espacios en ellos. Por ejemplo:

```markdown
COMPUTERNAME:~ USERNAME$ls -la Public/Drop Box
ls: Box: No such file or directory
ls: Public/Drop: No such file or directory
COMPUTERNAME:~ USERNAME$ 🁢
```

Básicamente, el programa **`ls`** está confundido por el espacio en el nombre del directorio **`Drop Box`**, y piensa que quieres listar los contenidos de **`Drop`** y **`Box`** como argumentos separados.

Puedes arreglar esto poniendo comillas alrededor del camino y nombre del archivo:

```markdown
COMPUTERNAME:~ USERNAME$ls -la "Public/Drop Box"
total 0
drwx-wx-wx+ 3 ChristopherA  staff  102 Oct 21 18:44 .
drwxr-xr-x+ 5 ChristopherA  staff  170 Oct 21 18:44 ..
-rw-r--r--  1 ChristopherA  staff    0 Oct 21 18:44 .localized
COMPUTERNAME:~ USERNAME$ 🁢
```

Alternativamente, puedes arreglar esto "escapando" el espacio poniendo una barra invertida delante, por ejemplo:

```markdown
COMPUTERNAME:~ USERNAME$ls -la Public/Drop\ Box
total 0
drwx-wx-wx+ 3 ChristopherA  staff  102 Oct 21 18:44 .
drwxr-xr-x+ 5 ChristopherA  staff  170 Oct 21 18:44 ..
-rw-r--r--  1 ChristopherA  staff    0 Oct 21 18:44 .localized
COMPUTERNAME:~ USERNAME$ 🁢
```

Finalmente, solo escribe **`ls -la Pu`** luego presiona tab, luego escribe **`D`** y presiona tab de nuevo. El camino será autocompletado con todos los espacios correctamente escapados.

## **Truco del Camino del Finder**

Un truco para caminos muy largos con espacios y otros caracteres especiales en ellos es que puedes arrastrar el archivo o carpeta desde una ventana del Finder (o el ícono de la carpeta en la barra de título de una ventana del Finder) al prompt, y el camino completo y nombre del archivo serán añadidos a tu línea de comandos.

Prueba **`ls`** seguido de arrastrar una carpeta abierta en la GUI del Finder, luego presiona **`return`**.

## **Caminos Absolutos y Directorio Hogar**

Hasta ahora, hemos listado el contenido de directorios que existen dentro de nuestro directorio actual. Cada directorio en tu computador tiene un nombre y un camino que te lleva a él.

¿Qué pasa si queremos ver otros directorios? Una forma es por lo que se conoce como el "camino absoluto". Estos caminos comienzan con el carácter **`/`**.

Pruébalo:

```markdown
COMPUTERNAME:~ USERNAME$ls /
Applications			home
Library				installer.failurerequests
System				net
Users				private
Volumes				sbin
bin				tmp
dev				usr
etc				var
COMPUTERNAME:~ USERNAME$ 🁢
```

Esto revela ítems en la carpeta "raíz" de tu computadora. Algunos los reconocerás desde la GUI del Finder, otros son invisibles para el Finder. Desde la línea de comandos, el directorio raíz **`/`** es el punto de partida para todo el contenido de tu computadora. Contiene todos los directorios en tu unidad de arranque, directorios para otras unidades, así como una serie de directorios de sistema especiales.

Ahora miremos el camino absoluto para el Directorio de Usuarios:

```markdown
COMPUTERNAME:~ USERNAME$ls /Users
USERNAME Shared
COMPUTERNAME:~ USERNAME$ 🁢
```

Ahora agreguemos tu nombre de usuario (si tiene un espacio en él, ¡prueba la completación con tabulador!):

```markdown
COMPUTERNAME:~ USERNAME$ls /Users/USERNAME
Desktop		Downloads	Movies		Pictures
Documents	Library		Music		  Public
COMPUTERNAME:~ USERNAME$ 🁢
```

Este es tu directorio de trabajo actual, que también es el directorio "hogar" predeterminado al que la aplicación shell por defecto, por lo que da el mismo resultado exacto que **`ls`** por sí solo.

Tu directorio hogar **`/Users/USERNAME/`** o **`~`** abreviado, contiene tus archivos y directorios personales. Por ejemplo Pictures, Music, Documents, etc. Cada uno de estos directorios se referencia como /home/USERNAME/{nombre del directorio}. Por ejemplo Documents se encuentra en /home/USERNAME/Documents.

Este camino hogar será diferente para cada usuario de la máquina, por lo que hay un atajo para él que es diferente para cada usuario, llevándolos a su directorio hogar. Este es el carácter tilde **`~`**. Así que **`ls`**, **`ls /Users/USERNAME/`** y 'ls ~` todos dan el mismo resultado.

Al igual que con los directorios, los archivos se referencian de la misma manera, por ejemplo, un archivo llamado temp.txt ubicado en el directorio hogar del usuario christophera puede ser referenciado usando el camino completo **`/Users/christophera/temp.txt`** o **`~/temp.txt`** por ese usuario.

Tanto archivos como directorios pueden ser referenciados usando sus caminos absolutos desde cualquier lugar en el sistema. Adicionalmente, se puede acceder a ellos usando solo su nombre si están en el mismo directorio. Por ejemplo, si tu directorio de trabajo actual es **`~`** cuando usas el terminal, puedes acceder al archivo **`/Users/USERNAME/temp.txt`** ingresando solo **`temp.txt`**.

## **Cambiando el Directorio de Trabajo**

En todos los ejemplos anteriores, nuestro camino del directorio de trabajo actual era el directorio hogar. Para cambiar el directorio de trabajo actual, escribe **`cd`** seguido por el {camino del directorio}, por ejemplo:

```markdown
COMPUTERNAME:~ USERNAME$cd Desktop
COMPUTERNAME:Desktop USERNAME$ 🁢
```

Nota que tu prompt ahora muestra tu directorio de trabajo. Para ver el "camino absoluto" de ese directorio, escribe **`pwd`** nuevamente.

```markdown
COMPUTERNAME:Desktop USERNAME$ pwd
/Users/USERNAME/Desktop
COMPUTERNAME:Desktop USERNAME$ 🁢
```

Para volver a tu directorio hogar, puedes escribir **`cd`** sin opciones ni argumentos, pero prefiero escribir **`cd ~`** para recordarme que estoy regresando a casa.

## **Creando un Directorio Temporal**

En la mayoría de los ejemplos restantes ya no voy a demostrar el prompt completo. En cambio, cuando veas el primer **`$`** muestra dónde debes escribir a la derecha de ese prompt. Un **`$`** final sin texto muestra que la salida de tu comando ha completado.

A medida que no queremos llenar nuestro directorio hogar con muchos archivos, vamos a crear un directorio **`temp`** para mantener nuestro trabajo futuro. Usaremos el comando **`mkdir`** (*hacer directorio*), luego entrar al folder con el comando **`cd`**, y confirmar que estamos ahí con el comando **`pwd`**.

```markdown
$ cd ~
$ mkdir temp
$ cd temp
$ pwd
/Users/USERNAME/temp
$
```

## **Manipulando Archivos**

Para crear tu primer archivo vacío, usa el comando **`touch`** seguido por el nombre del archivo:

```markdown
$ touch temp.txt
$
```

Puedes ver que este archivo existe con el comando **`ls`**:

```markdown
$ ls
temp.txt
$
```

Puedes editar este archivo de texto con tu editor de texto GUI de Mac (por defecto la app *Text Edit* en tu carpeta *Aplicaciones*) usando el comando **`open`**.

```markdown
$ open temp.txt
$

```

Ingresa algún texto en ese archivo, guárdalo (usa **`command + S`**) y ciérralo (usa **`command + W`**). Luego vuelve al terminal usando **`command + tab`** para alternar entre tus apps, o **`command + space + term`**. Cuando usas la línea de comandos de Mac es importante aprender estas teclas de comando: tus manos raramente necesitan dejar el teclado.

Ahora podemos mostrar ese texto usando el comando **`cat`** (cuyo nombre es corto para *concatenate*).

```markdown
$ cat temp.txt
The quick brown fox jumped over the lazy dog.
$
```

Si hubiera muchas páginas de texto, también puedes usar el comando **`more`**, que si hay más de una ventana de texto mostrará una ventana llena a la vez. Solo escribe **`space`** para ver la siguiente ventana, o **`q`** para salir, o **`h`** para ver una lista de otras opciones.

Ahora podemos copiar ese archivo usando el comando **`cp`** (*copiar*).

```markdown
$ cp temp.txt temporary.txt
$ cat temporary.txt
The quick brown fox jumped over the lazy dog.
$ ls
temp.txt	temporary.txt
$
```

Podemos copiar ese archivo a otro directorio también, agregando el camino. En este caso copiaremos un archivo temporal al directorio hogar.

```markdown
$ cp temp.txt ~/temp.txt
$ ls ~/*.txt
temp.txt
$
```

Podemos renombrar un archivo usando el comando **`mv`** (*mover*).

```markdown
$ mv temp.txt temp.bak
$ ls
temp.bak	temporary.txt
$
```

También podemos mover un archivo con el mismo comando.

```markdown
$ ls
temp.bak	temporary.txt
$ ls ~/*.txt
temp.txt
$ mv ~/temp.txt ./temp.txt
$ ls
temp.bak	temp.txt  temporary.txt
$ ls ~/*.txt
$
```

Podemos eliminar todos estos archivos usando el comando **`rm`** (corto para *eliminar*). Dado que **`rm`** puede ser peligroso, siempre recomiendo usarlo con la opción **`-i`** que lo hace interactivo.

```markdown
$ rm -i temp.txt
remove temp.txt? y
$ rm -i temporary.txt
remove temporary.txt? y
$ rm -i temp.bak
remove temp.bak? y
$
```

## **Los dos puntos (..) y el punto (.) Caminos Relativos**

Hay dos caminos especiales, el **`.`** y '..` - estos se usan para lo que son caminos *relativos*.

El directorio **`..`** es el directorio *arriba* del directorio de trabajo actual. Así que mientras aún estés en el directorio **`~/temp`** escribes 'ls ..` y verás el contenido del directorio hogar:

```markdown
$ ls ..
Desktop		Downloads	Movies		Pictures
Documents	Library		Music		Public
$
```

Mientras estés en ~/temp también puedes ingresar **`ls ..\{nombre del directorio}`** para ver directorios hermanos bajo el directorio hogar.

Si estuvieras profundamente dentro de un conjunto complejo de directorios, puedes salir de ellos ingresando **`cd ..`** - nota cómo cambia el prompt después de cada comando:

```markdown
COMPUTERNAME:~ temp USERNAME$ pwd
/Users/ChristopherA/temp
COMPUTERNAME:~ temp USERNAME$ cd ..
COMPUTERNAME:~ USERNAME$ cd ..
COMPUTERNAME:Users USERNAME$ cd ..
COMPUTERNAME:/ USERNAME$ cd ~/temp
COMPUTERNAME:temp USERNAME$ pwd
/Users/USERNAME/temp
COMPUTERNAME:~ USERNAME$
```

Un camino que comienza con **`.`** significa relativo al directorio de trabajo actual. En efecto **`ls .`** es lo mismo que **`ls`**. Hay momentos en que absolutamente quieres que un camino sea relativo a donde estás actualmente, usa la forma **`.`**.

## **Los * y ? Comodines**

A veces quieres copiar, renombrar o eliminar múltiples archivos a la vez. Podemos hacer esto usando el caracter comodín **`*`** (a veces llamado *estrella*) para reemplazar cero o más caracteres en un nombre de archivo o directorio.

El comando **`rm *`** eliminará todo en el directorio de trabajo actual excepto por aquellos archivos que son especiales y comienzan con un **`.`**, por lo tanto, hasta que seas muy experimentado, recomiendo que siempre uses la opción **`-i`** (para *interactivo*) cuando uses **`rm`**.

Prueba este experimento:

```markdown
$ cd ~/temp
$ ls
$ ls -a
.	..
$ mkdir there
$ touch .where here that then
$ ls
here	that	then	there
$ ls -a
.	..	.where	here	that	then	there
$ rm -i t*
remove that? y
remove then? y
rm: there: is a directory
$ ls
here there
$ ls -a
.	..	.where	here there
$ rm -i *
remove here? y
rm: there: is a directory
$ ls
there
$ ls -a
.	..	.where	there
$ rm -i .w*
remove .where? y
$ rm -i .*
rm: "." and ".." may not be removed
$
```

Como puedes ver, intentar eliminar directorios, incluyendo el **`.`** (el directorio actual) y **`..`** (el directorio padre) no está permitido con el comando **`rm -i`**. Entonces, ¿cómo eliminas directorios? Con el comando **`rmdir`**.

```markdown
$ ls
there
$ rmdir there
$ ls
$
```

Este comando puede parecer peligroso, pero el comando **`rmdir`** tiene una protección que no te permite eliminar carpetas que tienen contenidos. Primero debes eliminar cualquier contenido.

```markdown
$ mkdir there
$ touch there/that
$ ls there
that
A$ rmdir there
rmdir: there: Directory not empty
$ rm -i there/*
remove there/that? y
$ rmdir there
$ ls
$
```

Un uso particularmente común del comodín **`*`** es para ver o eliminar solo archivos con ciertas extensiones. Por ejemplo:

```markdown
$ touch a.txt b.txt a.jpg b.jpg
$ ls a*
a.jpg	a.txt
$ ls a.*
a.jpg	a.txt
$ ls *.txt
a.txt	b.txt
$ rm -i a.*
remove a.jpg? y
remove a.txt? y
$ ls
b.jpg	b.txt
$ rm -i *.txt
remove b.txt? y
$ ls
b.jpg
$ rm -i *.*
remove b.jpg? y
$ ls
$
```

Supongamos que tienes algunos archivos que terminan en **`.jpg`** y algunos que terminan en **`.jpeg`** -- el comodín asterisco facilita la limpieza:

```markdown
$ touch a.jpg b.jpeg c.java d.js
$ rm -i *.jp*g
remove a.jpg? y
remove b.jpeg? y
$ rm -i *.j*
remove c.java? y
remove d.js? y
$ ls
$
```

El comodín **`*`** coincide con cero o más caracteres, pero a veces puedes querer coincidir solo con un caracter. En este caso usamos el comodín **`?`**:

```markdown
$ touch task  taskA  taskB  taskXY
$ ls task*
task  taskA  taskB  taskXY
$ ls task?
taskA  taskB
$ ls task??
taskXY
$ rm -i ?ask*
remove task? y
remove taskA? y
remove taskB? y
remove taskXY? y
$ ls
$
```

Así que ahora que hemos terminado con nuestro directorio temp, podemos eliminar el directorio completo y todo su contenido de una vez con el comando **`rm -ir`** y la opción:

```markdown
$ cd ..
$ pwd
/Users/USERNAME
$ ls temp
task  taskA taskB taskXY
$ rm -ir temp
examine files in directory temp? y
remove temp/task? y
remove temp/taskA? y
remove temp/taskB? y
remove temp/taskXY? y
remove temp? y
$
```

## **Obteniendo Ayuda**

Si no recuerdas qué hace un comando, hay un comando **`whatis`** que devuelve una línea básica de información sobre él. También puedes usarlo para buscar palabras completas en la descripción de comandos:

```markdown
$ whatis cat
cat(1)                   - concatenate and print files
$ whatis rm
rm(1), unlink(1)         - remove directory entries
$ whatis delete
at(1), batch(1), atq(1), atrm(1) - queue, examine, or delete jobs for later execution
delete(n)                - delete things in the interpreter
ldapdelete(1)            - LDAP delete entry tool
rename(ntcl)             - Rename or delete a command
unset(ntcl)              - Delete variables
$
```

Relacionado está **`apropos`** que te permite buscar palabras clave. Típicamente devolverá muchos más ítems que **`whatis`**.

```markdown
$ whatis unzip
unzip(1)                 - list, test and extract compressed files in a ZIP archive
$ apropos unzip
bzip2(1), bunzip2(1)     - a block-sorting file compressor, v1.0.6 bzcat - decompresses files to stdout bzip2recover - recovers data from damaged bzip2 files
funzip(1)                - filter for extracting from a ZIP archive in a pipe
unzip(1)                 - list, test and extract compressed files in a ZIP archive
unzipsfx(1)              - self-extracting stub for prepending to ZIP archives
$
```

Cada uno de estos comandos tienen archivos de ayuda asociados con ellos, que pueden ser vistos con el comando **`man`** (corto para *manual*).

Al igual que el comando **`more`**, teclear **`space`** mueve hacia abajo una ventana llena de texto, y teclear **`q`** saldrá. Incluso puedes ver la página man de man con **`man man`**.

Muchos, pero no todos los comandos te darán un breve resumen de lo que hacen si los escribes sin opciones, o con la opción **`-h`** o **`--help`**. Muchas opciones pueden ser crípticas, pero la página man de los comandos debería explicarlas en más detalle.

## **MacOSX Bash Shell Keys**

### **Las siguientes funcionan en todas partes**

```markdown
Command-Shift-3    Capture the screen to a file
Command-Shift-Control-3    Capture the screen to the Clipboard
Command-Shift-4   Capture a selection of the screen to a file, or press the spacebar to capture just a window
Command-Shift-Control-4    Capture a selection of the screen to the Clipboard, , or press the spacebar to capture just a window
```

### **Las siguientes teclas funcionan en la mayoría de las apps de Mac donde se admite la entrada de texto:**

```markdown
Cmd + A     Select all text in text area
Ctrl + A    Move cursor to the beginning of the line or paragraph you are currently typing on
Ctrl + B    Move the cursor one character backward (same as Left-Arrow)
Ctrl + D    Delete one character in front of cursor (same as fn-Delete)
Ctrl + E    Move cursor to the end of the line you are currently typing on
Ctrl + F    Move the text cursor one character forward (same as Right-Arrow)
Ctrl + H    Delete the character behind the curor <same as Delete>
Ctrl + K    Delete "Kills" all characters after cursor to the end of the line.
Ctrl + N    Move the cursor down one line (same as Down-Arrow)
Ctrl + P    Move the cursor up one line (same as Up-Arrow)
Ctrl + T    Swap the last two characters before the cursor
Ctrl + Y    Pastes "Yanks" text that was Killed (Ctrl+K)
```

### **Las siguientes solo funcionan en la Terminal de Mac OSX usando el shell Bash predeterminado:**

```markdown
Ctrl + C    Kill whatever you are running
Ctrl + D    Exit the current shell
Ctrl + G    Aborts the current incremental search, restoring the original command at the prompt
Ctrl + J    Stops incremental search (Ctrl-R or Ctrl-S) and puts the found command at the prompt
Ctrl + L    Clears the the terminal window, leaving the current command at the prompt, similar to the clear command
Ctrl + R    Incrementally searches back through previously used commands (with history or !)
Ctrl + S    Incrementally searches forward through previously used commands (with history or !)
Ctrl + U    Clears the line before the cursor position. If you are at the end of the line, clears the entire line.
Ctrl + W    Delete the word before the cursor
Ctrl + Z    Puts whatever you are running into a suspended background process. fg restores it.
Ctrl + _    Undo the last editing command; you can undo all the way back to an empty line
Esc + B     Move cursor backward one word on the current line
Esc + D     Delete one word in front of cursor
Esc + F     Move cursor forward one word on the current line
Esc + R     Undo all changes made to this line
Esc + T     Swap the last two words before the cursor
Esc + Y     Pastes "Yanks" text that was previous Killed (Ctrl+K) before the last Kill
Tab         Auto-complete files and folder names
Tab Tab     Display all possible auto-complete values
```

### **Ratón en la Terminal**

```markdown
Opt + Click Moves cursor to where the mouse was clicked in many shell editors.
```

## **Comandos Meta**

``! - inicia una sustitución de historial !n - el comando en la lista de historial de bash, para algún entero n (funciona para negativos también) !! - el comando anterior; equivalente a !-1
!string - el comando más reciente que comienza con string

Los designadores de palabra seleccionan ciertas partes de un evento. Usa : para separar el evento del designador de palabra. Las palabras están numeradas desde 0 comenzando al inicio de la línea, y se insertan en la línea actual separadas por espacios simples.

$ - designa el último argumento (por ejemplo, !!:$ es el último arg del último comando; se puede acortar a !$) n - designa la enésima palabra (por ejemplo, !str:2 es el 2do arg del comando más reciente que comienza con str; !!:0 es el comando del último comando)