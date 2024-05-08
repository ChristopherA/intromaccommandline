# Parte3-Personaliza_tu_entorno.md

Esta parte es completamente opcional. Aquí tengo una serie de recomendaciones sobre cómo personalizar tu "entorno" de línea de comandos para que sea un poco más fácil de usar. No hay nada aquí que sea necesario para más adelante.

## **Perfiles de Terminal Solarizados**

La aplicación *Terminal* te permite elegir entre varias opciones para cómo se muestra la ventana del terminal. Abre su menú *Terminal*, submenú *Preferencias* y se pueden definir varias opciones. Haz clic en la pestaña *Perfiles* y verás las opciones. De las opciones predeterminadas, el perfil *Homebrew* es una elección útil — es texto brillante sobre fondo oscuro, lo que personalmente encuentro más fácil para programar.

Personalmente uso un fondo oscuro, pero con un texto de colores más sutiles basado en [Solarized](http://ethanschoonover.com/solarized). Puedes descargar y abrir mis preferencias usando el comando **`wget`**.

```markdown
$ cd ~/temp
$ wget https://github.com/ChristopherA/dotfiles/blob/master/install/osxterminal/christophera-dark.terminal
$ open christophera-dark.terminal
$ rm christophera-dark.terminal
```

En las *Preferencias* de *Terminal*, en el panel *General*, establece "Al iniciar abrir: Nueva ventana con perfil" y luego selecciona 'christophera-dark'.

Puedes configurar el tema de Atom para usar un conjunto similar de colores solarizados oscuros. El tema se llama *Solarized Dark* y viene instalado por defecto con Atom y puede ser activado yendo a la sección de Temas en la vista de Configuración **`comando + -`** y seleccionándolo del menú desplegable de Temas de Sintaxis.

# **Colores CLI**

Puedes habilitar colores de sintaxis para cómo varios comandos muestran texto en la línea de comandos. Para ver esto, prueba esto:

```markdown
$ export CLICOLOR=1
```

Ahora escribe **`ls -la`** y verás que los directorios y archivos se listan con diferentes colores.

Para compatibilidad con el tema solarizado del terminal, también configuro algunos colores específicos que encuentro que combinan bien:

```markdown
$ export LSCOLORS=gxfxbEaEBxxEhEhBaDaCaD
$ export LS_COLORS="di=36;40:ln=35;40:so=31;:pi=0;:ex=1;;40:bd=0;:cd=37;:su=37;:sg=0;:tw=0;:ow=0;:"
```

Ahora, si quieres que estos colores se muestren cada vez que abras *Terminal*, necesitarás agregarlos a un archivo especial para que siempre se carguen. Este archivo se llama **`~/.bash_profile`**.

```markdown
$ atom ~/.bash_profile
```

Agrega las tres líneas (sin el $), guarda, cierra *Terminal* y lánzalo de nuevo, y verás todos tus ajustes de color como prefieres.

Hay una aplicación de **`brew`** llamada **`grc`** (por [Generic Colourizer](http://kassiopeia.juls.savba.sk/~garabik/software/grc.html)) que agrega colorización a muchos más comandos que los mencionados anteriormente.

```markdown
$ brew install grc
==> Downloading http://korpus.juls.savba.sk/~garabik/software/grc/grc_1.9.orig.tar.gz
######################################################################## 100.0%
==> Caveats
New shell sessions will start using GRC after you add this to your profile:
  source "`brew --prefix`/etc/grc.bashrc"
==> Summary
🍺  /usr/local/Cellar/grc/1.9: 32 files, 148K, built in 3 seconds
$
```

Al igual que con los colores CLI, necesitarás agregar una línea a tu **`~/.bash_profile`**. Recomiendo una sintaxis ligeramente diferente a la que sugiere **`brew`**:

```markdown
if [ -f $(brew --prefix)/etc/grc.bashrc ]; then
  . $(brew --prefix)/etc/grc.bashrc
fi
```

## **Completado de Bash**

Hay una serie de aplicaciones que no permiten la completación de texto parcial con tabulación de la manera que otras lo hacen. La aplicación **`brew`** llamada **`bash-completion`** (de [http://bash-completion.alioth.debian.org](http://bash-completion.alioth.debian.org/)) hará que muchos más comandos soporten la completación con tabulación.

```markdown
$ brew install bash-completion
==> Downloading http://bash-completion.alioth.debian.org/files/bash-completion-1.3.tar.bz2
######################################################################## 100.0%
==> Patching
patching file bash_completion
==> ./configure --prefix=/usr/local/Cellar/bash-completion/1.3
==> make install
==> Caveats
Add the following lines to your ~/.bash_profile:
  if [ -f $(brew --prefix)/etc/bash_completion ]; then
    . $(brew --prefix)/etc/bash_completion
  fi

Homebrew's own bash completion script has been installed to
  /usr/local/etc/bash_completion.d

Bash completion has been installed to:
  /usr/local/etc/bash_completion.d
==> Summary
🍺  /usr/local/Cellar/bash-completion/1.3: 188 files, 1.1M, built in 20 seconds
$
```

Para instalar bash-completion una vez, escribe **`. $(brew --prefix)/etc/bash_completion`**. Puedes ver todas las aplicaciones que esta receta de **`brew`** añade escribiendo 'complete -p'

Una vez más, si quieres esto permanentemente, hay algunas líneas más para agregar a tu ~/.bash_profile

```markdown
if [ -f $(brew --prefix)/etc/bash_completion ]; then
  . $(brew --prefix)/etc/bash_completion
fi
```

## **Mejor Prompt**

Puedes personalizar el prompt del shell (la parte antes del $) de varias maneras, pero encuentro que la receta de **`brew`** llamada **`bash-git-prompt`** es bastante poderosa, especialmente una vez que comienzas a usar **`git`**.

```markdown
$ brew install bash-git-prompt
==> Downloading https://github.com/magicmonty/bash-git-prompt/archive/2.3.5.tar.gz
######################################################################## 100.0%
==> Caveats
You should add the following to your .bashrc (or equivalent):
  if [ -f "$(brew --prefix bash-git-prompt)/share/gitprompt.sh" ]; then
    GIT_PROMPT_THEME=Default
    source "$(brew --prefix bash-git-prompt)/share/gitprompt.sh"
  fi
==> Summary
🍺  /usr/local/Cellar/bash-git-prompt/2.3.5: 21 files, 120K, built in 2 seconds
$
```

Para ejecutarlo una vez, escribe:

```markdown
GIT_PROMPT_THEME=Default
source "$(brew --prefix bash-git-prompt)/share/gitprompt.sh"
```

Si te gusta, agrega esto a tu ~/.bash_profile:

```markdown
if [ -f "$(brew --prefix bash-git-prompt)/share/gitprompt.sh" ]; then
  GIT_PROMPT_THEME=Solarized
  source "$(brew --prefix bash-git-prompt)/share/gitprompt.sh"
fi
```

## **Más herramientas de Git y Github**

Usarás **`git`** y el servidor *GitHub* regularmente, por lo que estas herramientas añaden funcionalidades adicionales.

La primera se llama **`hub`**, y proporciona toda la funcionalidad de **`git`**, pero añade algunas características específicas de *GitHub*.

```markdown
$ brew install hub

```

Dado que **`hub`** es compatible con **`git`**, lo **`alias`** en mi **`~/bash_profile`**

```markdown
alias git=hub
```

La receta de **`brew`** [git-extras](https://github.com/visionmedia/git-extras) añade una serie de comandos **`git`** adicionales útiles, y son compatibles con **`hub`**:

```markdown
$ brew install git-extras
==> Downloading https://homebrew.bintray.com/bottles/git-extras-2.2.0.yosemite.bottle.tar.gz
######################################################################## 100.0%
==> Pouring git-extras-2.2.0.yosemite.bottle.tar.gz
==> Caveats
Bash completion has been installed to:
  /usr/local/etc/bash_completion.d
==> Summary
🍺  /usr/local/Cellar/git-extras/2.2.0: 91 files, 388K
$
```

Finalmente, GitHub ofrece una aplicación GUI de Mac útil llamada [GitHub](https://mac.github.com/) para navegar por los repositorios git.

```markdown
$ brew cask install github-desktop 
```

## **Script de preparación de OSX**

Todas las características de instalación y personalización sugeridas por este tutorial también están automatizadas como parte de un script prepare-osx.sh en [https://github.com/ChristopherA/prepare-osx-for-webdev](https://github.com/ChristopherA/prepare-osx-for-webdev), sin embargo, recomiendo que realices el tutorial primero para entender qué hace este script.