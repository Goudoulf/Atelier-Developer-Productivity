<h1 align="center">Atelier Developer Productivity</h1>

## Linux

### Shell

Article avec pleins de plugins zsh sympa : [article](https://safjan.com/top-popular-zsh-plugins-on-github-2023/)

### Fuzzy Finder

#### Install

DL github + launch install

    git clone --depth 1 https://github.com/junegunn/fzf.git ~/.fzf
    ~/.fzf/install

Ajouter dans shell que vous utiliser :

- bash

        # Set up fzf key bindings and fuzzy completion
        eval "$(fzf --bash)"

- zsh

        # Set up fzf key bindings and fuzzy completion
        eval "$(fzf --zsh)"

- fish

        # Set up fzf key bindings
        fzf --fish | source

#### To Infinity and beyond (with script)

Exemples de Script :

Permet de chercher un de mes projets et de l'ouvrir dans neovim

`vd() {
  local dir

  dir=(${(f)"$(find ~/Documents -type d | fzf)"})

  if [[ -n $dir ]]
  then
     cd $dir
     vim .
     print -l $dir[1]
  fi
}`

[fzf github](https://github.com/junegunn/fzf)

### cheat_sheet

[repo](https://github.com/chubin/cheat.sh?tab=readme-ov-file#installation)

#### How to use it
#### Unlimited Powa (with script)

### Commande utile

[Cheat sheet](https://www.geeksforgeeks.org/linux-commands-cheat-sheet/)
