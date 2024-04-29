<h1 align="center">Dotfiles</h1>

## Prerequis

Pour preparer l'atlelier de demain nous aurons besoin d'une machine virtuelle.
Afin de gagner du temps il faut copier le dossier AtelierDP :

```bash
cd /
cd sgroinfre/cassie
cp -R sgoinfre/cassie/AtelierDP ~/sgoinfre/
```

## Creer votre dotfiles

Les dotfiles sont simplement des fichiers de configuration utilisés par divers programmes sur un système Unix-like, tels que Linux ou macOS. Leur nom commence généralement par un point (.) pour les rendre cachés par défaut dans les listings de fichiers.

La gestion des dotfiles peut être simplifiée en utilisant des outils spécifiques, comme Git, pour les versionner et les synchroniser entre différentes machines. Cela permet aux utilisateurs de conserver une configuration cohérente de leur environnement de travail, même lorsqu'ils passent d'un système à un autre.

L'objectif de l'atelier d'aujourd'hui est de créer le votre, pour les étapes suivantes il existe des outils pour la maintenance
de dofiles, mais pour comprendre au mieux leur fonctionnement nous le feront à la main :

1. On crée un dossier dotfiles.

```bash 
## Exemple on crée un dossier dotfiles dans notre $HOME
mkdir ~/dotfiles
cd ~/dotfiles
```

2. Lister les conf que vous souhaitez ajouter dans votre dotfile.
Pour cela je vous invite à check en fonction des outils que vous utilisez, pour récuperer leur conf.
Exemple pour vscode : il vous faut le "settings.json", le "keybindings" et tous les ".json" dans le dossier snippets.


3. Dans votre dossier dotfiles, organiser l'architecture comme vous le souhaitez.

```bash
# Par exemple pour moi :
    ~/dotfiles/
        /vscode/
        /nvim/
        /alacritty/
        /zsh/
        /scripts/
```

4. Copier vos différentes conf dans les dossiers respectifs, puis supprimer l'ancien.

```bash
# Exemple pour VScode : 
    cp ~/.config/Code/User/settings.json ~/dotfiles/vscode/
    cp ~/.config/Code/User/keybindings.json ~/dotfiles/vscode/
    cp ~/.config/Code/User/snippets/c.json ~/dotfiles/vscode/
    rm ~/.config/Code/User/settings.json
    rm ~/.config/Code/User/keybindings.json
    rm ~/.config/Code/User/snippets/c.json
```

5. On créer ensuite un lien symbolique vers le fichier dans notre dossier dotfiles

```bash
##          "ORIGIN"                            "lien symbolique"
ln -s ~/dotfiles/vscode/settings.json ~/.config/Code/User/settings.json
ln -s ~/dotfiles/vscode/keybindings.json ~/.config/Code/User/keybindings.json
ln -s ~/dotfiles/vscode/c.jsoni ~/.config/Code/User/snippets/c.json
```

6. Pour les extensions

```bash
# pour save votre liste d'extension
code --list-extensions > ~/dotfiles/vscode/code_extensions
```

```bash
# pour installer votre liste d'extension
cat ~/dotfiles/vscode/code_extensions | xargs -L 1 code --install-extension
```

7. On peut ensuite init notre repo git et finaliser sa création.

```bash
cd ~/dotfiles/
git init
git add .
git commit -m "first commit / add dotfiles"
git branch -M main
git remote add origin "your repo address"
git push
```

8. (Optionnel) Vous pouvez faire un script pour automatiser les commits/push git quand vous faites des mises à jour.

Vous avez maintenant un dotfiles, avec vos configurations dessus. Si vous faites un changement dans votre conf, il vous suffit de git add / commit / 
push et les changements se feront sur vos differentes machines.

Il est possible d'automatiser cette tâche avec divers outils :

- [rcm](https://github.com/thoughtbot/rcm) qui s'occupe même de la création de lien symbolique.
- Avec un Makefile([exemple](https://github.com/denolfe/dotfiles/blob/master/Makefile))
- Demain nous verrons avec ansible.

Si vous utilisez Clion, il vaut mieux utiliser [Share IDE](https://www.jetbrains.com/help/clion/sharing-your-ide-settings.html#IDE_settings_sync).

Tout ici est un exemple, à vous d'adapter en fonction de vos besoins et de votre environnement.

## Petit plus

Pour vscode une maniere pour automotiser la creation de dotfiles :
[article](https://anhari.dev/blog/saving-vscode-settings-in-your-dotfiles)


Je vous conseil grandement de faire un tour sur [awesome-dotfiles](https://github.com/webpro/awesome-dotfiles).
Dans ce repo vous trouver pleins d'outils et de tutoriels pour faire votre dotfiles, ainsi que pleins d'exemple de dotfiles.

<details>
  <summary>Exemple de script</summary>

```bash
#!/bin/bash
############################
# .make.sh
# This script creates symlinks from the home directory to any desired dotfiles in ~/dotfiles
############################

########## Variables

dir=~/dotfiles                    # dotfiles directory
olddir=~/dotfiles_old             # old dotfiles backup directory
files="bashrc vimrc vim zshrc oh-my-zsh"    # list of files/folders to symlink in homedir

##########

# create dotfiles_old in homedir
echo "Creating $olddir for backup of any existing dotfiles in ~"
mkdir -p $olddir
echo "...done"

# change to the dotfiles directory
echo "Changing to the $dir directory"
cd $dir
echo "...done"

# move any existing dotfiles in homedir to dotfiles_old directory, then create symlinks 
for file in $files; do
    echo "Moving any existing dotfiles from ~ to $olddir"
    mv ~/.$file ~/dotfiles_old/
    echo "Creating symlink to $file in home directory."
    ln -s $dir/$file ~/.$file
done
```
</details>
