# Parte2-Preparación_e_instalación.md

Cada Mac soporta un gran número de herramientas de línea de comandos, sin embargo, no todos los programas que necesitas para el desarrollo web están incluidos por defecto. Este tutorial te instruye sobre cómo preparar y configurar tu Mac para convertirlo en un potente sistema de desarrollo web.

No necesitas entender profundamente todos los comandos que se usan aquí — se explican brevemente, pero aún no necesitas aprenderlos. Solo los explico porque es TU computadora y deberías saber qué herramientas se han añadido y por qué.

## **Actualizaciones del Sistema**

Lo primero que necesitas hacer es asegurarte de que tienes la versión más reciente del sistema operativo, que al momento de escribir esta introducción es Mac OS X Yosemite 10.10.3. Todo en estos archivos de introducción debería funcionar en versiones anteriores del sistema operativo, sin embargo, cuando estás desarrollando web es importante tener las actualizaciones más recientes por razones de seguridad.

Puedes obtener todas tus actualizaciones del sistema yendo al ítem *App Store…* bajo el menú Apple, haciendo clic en la pestaña *Updates* y presionando el botón *Update All*. Sin embargo, también puedes hacerlo desde la línea de comandos.

El comando **`sudo`** se usa para ejecutar programas que necesitan privilegios adicionales para cambiar tu computadora, y por lo tanto, la contraseña administrativa de tu Mac. **`/usr/sbin/softwareupdate -l`** es el programa que verifica con los servidores de actualización de Apple la versión más reciente. Puede que necesites ejecutar este comando varias veces, o incluso reiniciar tu sistema si tu Mac no está actualizado.

```markdown
$ cd ~
$ sudo /usr/sbin/softwareupdate -l

WARNING: Improper use of the sudo command could lead to data loss
or the deletion of important system files. Please double-check your
typing when using sudo. Type "man sudo" for more information.

To proceed, enter your password, or type Ctrl-C to abort.

Password:
Software Update Tool
Copyright 2002-2012 Apple Inc.

Finding available software
No new software available.
$
```

## **Instalar las Herramientas de Línea de Comandos de Apple**

A continuación, vamos a instalar las Herramientas de Línea de Comandos de Apple, que instalarán una serie de herramientas de desarrollo que estarán disponibles desde la línea de comandos. Hay un "truco" que consiste en tocar un archivo que hace que esto suceda desde la línea de comandos sin cargar el entorno de desarrollo XCODE de Apple para crear aplicaciones para Mac y iOS.

Debido a que recientemente ingresaste una contraseña administrativa para el comando **`sudo`**, es posible que el shell no te pida de nuevo tu contraseña administrativa.

```markdown
$ touch /tmp/.com.apple.dt.CommandLineTools.installondemand.in-progress
sudo /usr/sbin/softwareupdate -ia
Software Update Tool
Copyright 2002-2012 Apple Inc.

Finding available software

Downloading Command Line Tools (OS X 10.10)
Downloaded Command Line Tools (OS X 10.10)
Installing Command Line Tools (OS X 10.10)
Done with Command Line Tools (OS X 10.10)
Done.
$/bin/rm /tmp/.com.apple.dt.CommandLineTools.installondemand.in-progress
```

Con esta instalación, acabas de instalar 92 herramientas de desarrollo en tu /Library/Developer/CommandLineTools/bin/

```markdown
BuildStrings CpMac DeRez GetFileInfo MergePef MvMac ResMerger Rez RezDet RezWack SetFile SplitForks UnRezWack ar as asa bison c++ c89 c99 cc clang clang++ cmpdylib codesign_allocate cpp ctags ctf_insert dsymutil dwarfdump dyldinfo flex flex++ g++ gatherheaderdoc gcc gcov git git-cvsserver git-receive-pack git-shell git-upload-archive git-upload-pack gm4 gnumake gperf hdxml2manxml headerdoc2html indent install_name_tool ld lex libtool lipo lldb llvm-cov llvm-profdata lorder m4 make mig mkdep nasm ndisasm nm nmedit otool pagestuff projectInfo ranlib rebase redo_prebinding resolveLinks rpcgen segedit size strings strip svn svnadmin svndumpfilter svnlook svnrdump svnserve svnsync svnversion unifdef unifdefall unwinddump what xml2man yacc
```

A partir de ahora, la actualización regular del Sistema de la Mac App Store mantendrá estas herramientas actualizadas.

## **Crear Algunas Carpetas Adicionales en el Hogar**

Encuentro útil preparar con antelación algunas carpetas adicionales en mi directorio de inicio "~". La convención que uso es que si la carpeta comienza con una mayúscula, la carpeta contiene elementos para la GUI del Finder. Si la carpeta comienza con una letra minúscula (lo que hace que sea más rápido de escribir) entonces se usa por la CLI.

Todas estas carpetas son opcionales — muchas no las usarás hasta mucho más tarde en este tutorial:

- ~/.dotfiles # Aquí es donde respaldo mis dotfiles (explicado más adelante) y almaceno algunas otras herramientas útiles.
- ~/.dotfiles/bin # Aquí es donde guardo pequeños scripts de línea de comandos que uso regularmente.
- ~/Applications # Aquí es donde guardo cualquier aplicación GUI que está instalada para fines de desarrollo separado de esa carpeta de /Applications raíz.
- ~/code # Aquí es donde almaceno el código fuente de repositorios de código abierto de github.
- ~/Pool # Aquí es donde almaceno archivos grandes que excluyo de la copia de seguridad en Time Machine. Genial para películas, archivos grandes de instalación, etc., que tengo respaldados en otro lugar o que se pueden descargar nuevamente de la red.
- ~/projects # Aquí es donde guardo repositorios de mi propio código fuente o trabajos en progreso de otros.
- ~/temp # Aquí es donde guardo código y proyectos que son solo temporales y pueden ser eliminados en cualquier momento. Practico aquí.

```markdown
$ mkdir ~/.dotfiles ~/.dotfiles/bin ~/Applications ~/code ~/Pool ~/projects ~/temp
$ ls -a
.			Desktop			Pictures
..			Documents		Pool
.CFUserTextEncoding	Downloads		Public
.Trash			Library			code
.dotfiles		Movies			projects
Applications		Music			temp

$
```

## **Instalación de Brew**

A continuación, vamos a instalar [Homebrew](http://brew.sh/) (conocido como **`brew`**), un gestor de paquetes de software.

Puedes considerar **`brew`** como una tienda de aplicaciones para aplicaciones web de código abierto y herramientas de desarrolladores. Hay miles de diferentes bases de código abierto, todas con varias dependencias entre ellas, y cada una requiriendo diferentes configuraciones según el sistema operativo de computadora en el que se ejecuta (Linux, Unix, Mac, Windows, etc.). Brew gestiona esas complejidades. Si solicitas instalar una herramienta particular que necesita otros paquetes, herramientas o bibliotecas para funcionar, Brew primero los instalará en el orden correcto. Brew también almacena sus archivos de algunas maneras específicas que son las mejores prácticas para que diferentes herramientas no interfieran entre sí.

Brew no está instalado en tu Mac por defecto, por lo que necesitarás ejecutar un script para instalarlo. Proporcionan un script para instalarlo en su sitio de github, que se ejecuta por **`ruby`** que está instalado en tu Mac por defecto. ADVERTENCIA: Ten cuidado siempre que alguien te pida que ejecutes un script que tenga un comando **`curl`** en él, porque si el autor tiene malas intenciones, pueden corromper tu sistema o hacerlo vulnerable. En este caso, el script se ejecuta desde un sitio web confiable (github) y es de una cuenta confiable allí (Homebrew). Te sugiero que vayas al sitio web de [Homebrew](http://brew.sh/) y confirmes que este es el script correcto para usar.

Este script puede pedirte tu contraseña de administrador.

```markdown
$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
==> This script will install:
/usr/local/bin/brew
/usr/local/share/doc/homebrew
/usr/local/share/man/man1/brew.1
/usr/local/share/zsh/site-functions/_brew
/usr/local/etc/bash_completion.d/brew
/usr/local/Homebrew
==> The following new directories will be created:
/usr/local/Cellar
/usr/local/Homebrew
/usr/local/Frameworks
/usr/local/bin
/usr/local/etc
/usr/local/include
/usr/local/lib
/usr/local/opt
/usr/local/sbin
/usr/local/share
/usr/local/share/zsh
/usr/local/share/zsh/site-functions
/usr/local/var

Press RETURN to continue or any other key to abort
==> /usr/bin/sudo /bin/mkdir -p /usr/local/Cellar /usr/local/Homebrew /usr/local/Frameworks /usr/local/bin /usr/local/etc /usr/local/include /usr/local/lib /usr/local/opt /usr/local/sbin /usr/local/share /usr/local/share/zsh /usr/local/share/zsh/site-functions /usr/local/var
==> /usr/bin/sudo /bin/chmod g+rwx /usr/local/Cellar /usr/local/Homebrew /usr/local/Frameworks /usr/local/bin /usr/local/etc /usr/local/include /usr/local/lib /usr/local/opt /usr/local/sbin /usr/local/share /usr/local/share/zsh /usr/local/share/zsh/site-functions /usr/local/var
==> /usr/bin/sudo /bin/chmod u+rwx share/zsh share/zsh/site-functions
==> /usr/bin/sudo /usr/sbin/chown admin /usr/local/Cellar /usr/local/Homebrew /usr/local/Frameworks /usr/local/bin /usr/local/etc /usr/local/include /usr/local/lib /usr/local/opt /usr/local/sbin /usr/local/share /usr/local/share/zsh /usr/local/share/zsh/site-functions /usr/local/var
==> /usr/bin/sudo /usr/bin/chgrp admin /usr/local/Cellar /usr/local/Homebrew /usr/local/Frameworks /usr/local/bin /usr/local/etc /usr/local/include /usr/local/lib /usr/local/opt /usr/local/sbin /usr/local/share /usr/local/share/zsh /usr/local/share/zsh/site-functions /usr/local/var
==> /usr/bin/sudo /bin/mkdir -p /Users/admin/Library/Caches/Homebrew
==> /usr/bin/sudo /bin/chmod g+rwx /Users/admin/Library/Caches/Homebrew
==> /usr/bin/sudo /usr/sbin/chown admin /Users/admin/Library/Caches/Homebrew
==> Downloading and installing Homebrew...
remote: Counting objects: 1033, done.
remote: Compressing objects: 100% (929/929), done.
remote: Total 1033 (delta 95), reused 592 (delta 68), pack-reused 0
Receiving objects: 100% (1033/1033), 1.05 MiB | 508.00 KiB/s, done.
Resolving deltas: 100% (95/95), done.
From https://github.com/Homebrew/brew
 * [new branch]      master     -> origin/master
HEAD is now at 23efbc5 Merge pull request #1051 from woodruffw/cctools-macho-remove
==> Homebrew has enabled anonymous aggregate user behaviour analytics
Read the analytics documentation (and how to opt-out) here:
  https://git.io/brew-analytics
==> Tapping homebrew/core
Cloning into '/usr/local/Homebrew/Library/Taps/homebrew/homebrew-core'...
remote: Counting objects: 3725, done.
remote: Compressing objects: 100% (3617/3617), done.
remote: Total 3725 (delta 15), reused 1247 (delta 0), pack-reused 0
Receiving objects: 100% (3725/3725), 2.91 MiB | 1.13 MiB/s, done.
Resolving deltas: 100% (15/15), done.
Checking connectivity... done.
Tapped 3604 formulae (3,752 files, 9M)
Checking out v1.0.1 in /usr/local/Homebrew...
To checkout master in /usr/local/Homebrew run:
  'cd /usr/local/Homebrew && git checkout master
Already up-to-date.
==> Installation successful!
==> Next steps
Run `brew help` to get started
Further documentation: https://git.io/brew-docs
==> Homebrew has enabled anonymous aggregate user behaviour analytics
Read the analytics documentation (and how to opt-out) here:
  https://git.io/brew-analytics
$
```

Después de instalar Homebrew, lo primero que queremos hacer es confirmar que se ha instalado correctamente, o si había algo más instalado en tu Mac anteriormente que podría causar problemas.

```markdown
$ brew doctor
Your system is ready to brew.
$
```

Si hubiera algún error, **`brew doctor`** te dirá cómo solucionarlo. Si lo que sugiere para solucionar el problema no funciona, encuentro que casi todos los problemas que han surgido son una pregunta en el sitio web [StackOverflow](http://stackoverflow.com/) así que busca tu solución allí.

## **Instalar Git**

La primera aplicación de línea de comandos que instalaremos es [Git](http://git-scm.com/), que es el sistema de control de versiones de código fuente más popular. Un sistema de control de código fuente te ayuda a manejar la producción de tu código, hacer copias de seguridad y restaurar diferentes versiones de tu código, y trabajar cooperativamente con otros. **`git`** es popular porque es de código abierto, es distribuido (es decir, no hay un repositorio maestro de donde los archivos deben venir), funciona con proyectos tan grandes como el sistema operativo Linux con miles de colaboradores, proyectos de equipos pequeños, y sin embargo es útil incluso para un solo programador.

Usaremos **`brew`** para instalar git, así que siempre antes de que hagamos algo con **`brew`** queremos asegurarnos de que **`brew`** está actualizado. Acabamos de instalarlo así que realmente no necesitamos hacer esto ahora, pero demostraré las mejores prácticas (todo después de un # es un comentario):

```markdown
$ brew doctor # run self test to see if brew is running properly
Your system is ready to brew.
$ brew update # update brew itself to the latest version, and get latest list of apps
Already up-to-date.
$ brew upgrade # upgrade any apps managed by brew to the most recent version
$

```

A continuación, confirmaremos información sobre git, luego lo instalaremos.

```markdown
$ brew info git
git: stable 2.3.5 (bottled), HEAD
http://git-scm.com
/usr/local/Cellar/git/2.3.5 (1363 files, 31M) *
Not installed
From: https://github.com/Homebrew/homebrew/blob/master/Library/Formula/git.rb
$ brew install git
==> Downloading https://homebrew.bintray.com/bottles/git-2.3.5.yosemite.bottle.t
######################################################################## 100.0%
==> Pouring git-2.3.5.yosemite.bottle.tar.gz
==> Caveats
The OS X keychain credential helper has been installed to:
  /usr/local/bin/git-credential-osxkeychain

The "contrib" directory has been installed to:
  /usr/local/share/git-core/contrib

Bash completion has been installed to:
  /usr/local/etc/bash_completion.d

zsh completion has been installed to:
  /usr/local/share/zsh/site-functions
==> Summary
🍺  /usr/local/Cellar/git/2.3.5: 1363 files, 31M
$ git --version
git version 2.3.5
$
```

## **Instalar Cask**

[Cask](http://caskroom.io/) es una aplicación especial de brew que instala una serie de aplicaciones GUI para Mac. La encuentro particularmente útil para instalar esas aplicaciones de desarrolladores que requieren un instalador o un archivo .dmg. Otra cosa útil que hace es que pone la aplicación en tu carpeta ~/Applications, manteniéndolas separadas de tus otras aplicaciones.

```markdown
$ brew tap caskroom/cask
Checking out v1.0.1 in /usr/local/Homebrew...
To checkout v1.0.1 in /usr/local/Homebrew run:
  'cd /usr/local/Homebrew && git checkout v1.0.1
==> Tapping caskroom/cask
Cloning into '/usr/local/Homebrew/Library/Taps/caskroom/homebrew-cask'...
remote: Counting objects: 3431, done.
remote: Compressing objects: 100% (3412/3412), done.
remote: Total 3431 (delta 37), reused 452 (delta 13), pack-reused 0
Receiving objects: 100% (3431/3431), 1.16 MiB | 0 bytes/s, done.
Resolving deltas: 100% (37/37), done.
Checking connectivity... done.
Tapped 0 formulae (3,438 files, 3.6M)
$
```

## **Instalando el Editor de Texto Atom**

A continuación, vamos a usar **`brew cask`** para instalar el editor de texto Atom. Hay muchos editores de texto de línea de comandos poderosos por ahí (y una batalla constante entre los fans de emacs vs los de vim), pero aprenderlos está fuera del alcance de este tutorial. Mientras tanto, hay un editor de texto GUI muy poderoso, gratuito y de código abierto optimizado para desarrolladores de línea de comandos y web llamado Atom. Una de sus mejores características es su integración con Git.

Lo instalaremos con **`brew cask`**

```markdown
$ brew cask install atom
==> We need to make Caskroom for the first time at /opt/homebrew-cask/Caskroom
==> We'll set permissions properly so we won't need sudo in the future
Password:
chmod: /opt: No such file or directory
==> Downloading https://atom.io/download/mac
######################################################################## 100.0%
==> Symlinking App 'Atom.app' to '/Users/ChristopherA/Applications/Atom.app'
==> Symlinking Binary 'apm' to '/usr/local/bin/apm'
==> Symlinking Binary 'atom.sh' to '/usr/local/bin/atom'
🍺  atom staged at '/opt/homebrew-cask/Caskroom/atom/latest' (11288 files, 239M)
$
```

De ahora en adelante, en lugar de usar el comando **`open`** para editar un archivo de texto, usaremos **`atom`**, por ejemplo:

```markdown
$ touch ~/temp/temp.txt
$ atom ~/temp/temp.txt
```

Ahora puedes editar este archivo usando la experiencia GUI familiar de Mac.

## **Instalar Node**

[Node](https://nodejs.org/) es una herramienta popular de servidor web que ejecuta Javascript. Instalado en Mac, también proporciona un entorno interactivo para aprender cómo codificar Javascript y usar varios frameworks. Lo estamos instalando porque varios tutoriales más adelante lo usan.

```markdown
$ brew install node
==> Downloading https://homebrew.bintray.com/bottles/node-0.12.2_1.yosemite.bott
######################################################################## 100.0%
==> Pouring node-0.12.2_1.yosemite.bottle.tar.gz
==> Caveats
If you update npm itself, do NOT use the npm update command.
The upstream-recommended way to update npm is:
  npm install -g npm@latest

Bash completion has been installed to:
  /usr/local/etc/bash_completion.d
==> Summary
🍺  /usr/local/Cellar/node/0.12.2_1: 2603 files, 28M
$
```

## **Web Get**

Encuentro la herramienta **`wget`** muy útil. Apúntala a una URL y descarga los contenidos en un archivo. También puedes hacer esto con la herramienta integrada **`curl`**, pero encuentro **`wget`** muy útil en algunos momentos.

```markdown
$ brew install wget
==> Installing wget dependency: openssl
==> Downloading https://homebrew.bintray.com/bottles/openssl-1.0.2a-1.yosemite.bottle.tar.gz
######################################################################## 100.0%
==> Pouring openssl-1.0.2a-1.yosemite.bottle.tar.gz
==> Caveats
A CA file has been bootstrapped using certificates from the system
keychain. To add additional certificates, place .pem files in
  /usr/local/etc/openssl/certs

and run
  /usr/local/opt/openssl/bin/c_rehash

This formula is keg-only, which means it was not symlinked into /usr/local.

Mac OS X already provides this software and installing another version in
parallel can cause all kinds of trouble.

Apple has deprecated use of OpenSSL in favor of its own TLS and crypto libraries

Generally there are no consequences of this for you. If you build your
own software and it requires this formula, you'll need to add to your
build variables:

    LDFLAGS:  -L/usr/local/opt/openssl/lib
    CPPFLAGS: -I/usr/local/opt/openssl/include

==> Downloading https://www.geotrust.com/resources/root_certificates/certificates/Equifax_Secure_
######################################################################## 100.0%
==> /usr/local/Cellar/openssl/1.0.2a-1/bin/c_rehash
==> Summary
🍺  /usr/local/Cellar/openssl/1.0.2a-1: 463 files, 18M
==> Installing wget
==> Downloading https://homebrew.bintray.com/bottles/wget-1.16.3.yosemite.bottle.tar.gz
######################################################################## 100.0%
==> Pouring wget-1.16.3.yosemite.bottle.tar.gz
🍺  /usr/local/Cellar/wget/1.16.3: 9 files, 1.5M
Aeguss-MacBook-Pro:intro-mac-command-line ChristopherA$
```

## **Limpieza de Brew & Cask**

Después de que **`brew`** o **`brew cask`** algo, es una buena práctica decirle a brew que limpie. No tienes que hacer esto después de cada ítem brew, puedes brew varios ítems a la vez y solo limpiar después.

```markdown
$ brew linkapps --local
Finished linking. Find the links under /Users/ChristopherA/Applications.
$ brew cleanup
$ brew prune
Pruned 0 dead formulae
$ brew cask cleanup
brew cask cleanup
==> Removing dead symlinks
Nothing to do
==> Removing cached downloads
/Library/Caches/Homebrew/atom-latest
/Library/Caches/Homebrew/Casks/atom-latest
$
```

## **Limpieza Final**

Las bases de datos locate y whathis, usadas por las utilidades de línea de comandos **`locate`**, **`whatis`** y **`apropos`**, solo se generan semanalmente, así que ejecuta esto después de agregar cualquier comando para actualizar la base de datos. Esto sucederá en segundo plano y puede tomar algún tiempo generarse la primera vez.

```markdown
$ sudo periodic daily weekly monthly
```