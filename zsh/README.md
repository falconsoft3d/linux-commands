# Configuración de **zsh** (ubuntu 18.04)

### Prerequisitos

```
# apt install zsh vim git curl wget
```

### Instalar [oh my zsh](https://ohmyz.sh/)

```
$ sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```

actualizar el shell a zsh:

```
# chsh -s `which zsh`
```

y cerrar/iniciar sesión:

```
$ pkill -KILL -u $USER
```

### Temas

#### Actualizar tema a [agnoster](https://github.com/agnoster/agnoster-zsh-theme)

instalar fuentes ([aquí](https://powerline.readthedocs.io/en/latest/installation/linux.html#fonts-installation)):

```
# apt install fonts-powerline
```

abrir archivo de configuración:

```
$ vi ~/.zshrc    
```

actualizar tema:

```
ZSH_THEME="agnoster"
```

#### Instalar [powerlevel9k](https://github.com/bhilburn/powerlevel9k)

```
$ git clone https://github.com/bhilburn/powerlevel9k.git ~/.oh-my-zsh/custom/themes/powerlevel9k
```

abrir archivo de configuración:

```
$ vi ~/.zshrc    
```

actualizar tema:

```
ZSH_THEME="powerlevel9k/powerlevel9k"
```

agregar configuraciones:

```
POWERLEVEL9K_LEFT_PROMPT_ELEMENTS=(context dir newline vcs)
POWERLEVEL9K_RIGHT_PROMPT_ELEMENTS=(status ram time)
```

en caso de usar [tmux](tmux):

```
POWERLEVEL9K_LEFT_PROMPT_ELEMENTS=(dir newline vcs)
POWERLEVEL9K_RIGHT_PROMPT_ELEMENTS=(status)
```

en caso de usar [tmux](tmux), [nodeenv](https://github.com/ekalinin/nodeenv) y [virtualenv](https://virtualenv.pypa.io/en/latest/):

```
POWERLEVEL9K_LEFT_PROMPT_ELEMENTS=(dir newline nodeenv virtualenv vcs)
POWERLEVEL9K_RIGHT_PROMPT_ELEMENTS=(status)
```

#### Mejora del elemento `virtualenv`
Abrir archivo de configuración:

```
$ vi ~/.oh-my-zsh/custom/themes/powerlevel9k
```

Y reemplazar la función `prompt_virtualenv` por:

```
prompt_virtualenv() {
  [[ -z "$VIRTUAL_ENV" ]] && return

  local info="\ue63c v$(python --version | cut -d' ' -f2)[${VIRTUAL_ENV:t}]"
  "$1_prompt_segment" "$0" "$2" "black" "green" "$info"
}
```

Instalar en el sistema la fuente: [devicons](https://github.com/gabrielelana/awesome-terminal-fonts/blob/master/fonts/devicons-regular.ttf)

### Alias

Abrir archivo de configuración y agregar alias:

```
$ vi ~/.zshrc    
```


#### Docker

Remover contenedores:

```
alias docker-destroy-all-ps='docker rm -f $(docker ps -aq)'
```

Remover contenedores y volúmenes:

```
alias docker-destroy-all-ps-v='docker rm -f $(docker ps -aq) ; docker volume rm $(docker volume ls -q)'
```

Remover imágenes:

```
alias docker-destroy-all-i='docker rmi -f $(docker images -aq)'
```

Remover todo:

```
alias docker-destroy-all='docker rm -f $(docker ps -aq) ; docker volume rm $(docker volume ls -q) ; docker rmi -f $(docker images -aq)'
```

#### Sistema

Actualizar:

```
alias upgrade='sudo apt update -y && sudo apt upgrade -y && sudo apt autoremove'
```

#### Git

Pull rebase de muchos repositorios:

```
alias gup-all='find . -mindepth 1 -maxdepth 1 -type d -printf "\n\n>>>>%f\n" -exec git --git-dir={}/.git --work-tree=$PWD/{} pull -r origin master \;'
```

Git status de muchos repositorios:

```
alias gst-all='find . -mindepth 1 -maxdepth 1 -type d -printf "\n\n>>>>%f\n" -exec git --git-dir={}/.git --work-tree=$PWD/{} status \;'
```

### Otros

- [Cheat sheet](https://github.com/robbyrussell/oh-my-zsh/wiki/Cheatsheet)
