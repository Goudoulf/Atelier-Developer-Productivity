<h1 align="center">Dotfiles</h1>

Les dotfiles sont simplement des fichiers de configuration utilisés par divers programmes sur un système Unix-like, tels que Linux ou macOS. Leur nom commence généralement par un point (.) pour les rendre cachés par défaut dans les listings de fichiers.

La gestion des dotfiles peut être simplifiée en utilisant des outils spécifiques, comme Git, pour les versionner et les synchroniser entre différentes machines. Cela permet aux utilisateurs de conserver une configuration cohérente de leur environnement de travail, même lorsqu'ils passent d'un système à un autre.

L'objectif de l'atelier d'aujourd'hui est de créer le votre, pour les étapes suivantes il existe des outils pour la maintenance
de dofiles, mais pour comprendre au mieux leur fonctionnement nous le feront à la main :

1. On crée un dossier dotfiles.

``` 
// Exemple on crée un dossier dotfiles dans notre $HOME
mkdir ~/dotfiles
cd ~/dotfiles
```

2. Lister les conf que vous souhaitez ajouter dans votre dotfile.
Pour cela je vous invite à check en fonction des outils que vous utilisez, pour récuperer leur conf.
Pour vscode : il vous faut le "settings.json", le "keybindings" et tous les ".json" dans le dossier snippets.


3. Dans votre dossier dotfiles, organiser l'architecture comme vous le souhaitez.

```
Par exemple pour moi :
    ~/dotfiles/
        /vscode/
        /nvim/
        /alacritty/
        /zsh/
        /scripts/
```

4. Copier vos différentes conf dans les dossiers respectifs, puis supprimer l'ancien.

```
 Exemple pour VScode : 
    cp ~/.config/Code/User/settings.json ~/dotfiles/vscode/
    cp ~/.config/Code/User/keybindings.json ~/dotfiles/vscode/
    cp ~/.config/Code/User/snippets/c.json ~/dotfiles/vscode/
    rm ~/.config/Code/User/settings.json
    rm ~/.config/Code/User/keybindings.json
    rm ~/.config/Code/User/snippets/c.json
```

5. On créer ensuite un lien symbolique vers le fichier dans notre dossier dotfiles

```
//          "ORIGIN"                            "lien symbolique"
ln -s ~/dotfiles/vscode/settings.json ~/.config/Code/User/settings.json
ln -s ~/dotfiles/vscode/keybindings.json ~/.config/Code/User/keybindings.json
ln -s ~/dotfiles/vscode/c.jsoni ~/.config/Code/User/snippets/c.json
```

6. On peut ensuite init notre repo git et finaliser sa création.

```
cd ~/dotfiles/
git init
git add .
git commit -m "first commit / add dotfiles"
git branch -M main
git remote add origin "your repo address"
git push
```

7. (Optionnel) Vous pouvez faire un script pour automatiser git quand vous faites des mises à jour.

Vous avez maintenant un dotfiles, avec vos configurations dessus. Si vous faites un changement dans votre conf, il vous suffit de git add, git commit, et push et les changements se feront.
C'est possible d'automatiser cette tâche avec divers outils.
Par exemple [rcm](https://github.com/thoughtbot/rcm) qui s'occupe même de la création de lien symbolique.
Nous verrons aussi une autre manière avec ansible au prochain atelier.

Pour vscode je vous conseille cet article qui explique aussi comment récuperer la liste des extensions :
[article](https://anhari.dev/blog/saving-vscode-settings-in-your-dotfiles)

Pour aller plus loin [awesome-dotfiles](https://github.com/webpro/awesome-dotfiles)

Tout ici est un exemple, à vous d'adapter en fonction de vos besoins et de votre environnement.
