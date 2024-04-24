<h1 align="center">Dotfiles</h1>

Les dotfiles sont simplement des fichiers de configuration utilisés par divers programmes sur un système Unix-like, tels que Linux ou macOS. Leur nom commence généralement par un point (.) pour les rendre cachés par défaut dans les listings de fichiers.

La gestion des dotfiles peut être simplifiée en utilisant des outils spécifiques, comme Git, pour les versionner et les synchroniser entre différentes machines. Cela permet aux utilisateurs de conserver une configuration cohérente de leur environnement de travail, même lorsqu'ils passent d'un système à un autre.

L'objectif de l'atelier d'aujourd'hui est de creer le votre, pour les etapes suivante ils existent des outils pour la maintenance
de dofiles, mais pour comprendre au mieux leur fonctionnement nous le feront a la main :

- 1. On cree un dossier dotfiles.

``
//example on cree un dossier dotfiles dans notre $HOME
mkdir ~/dotfiles
cd ~/dotfiles
``

- 2. Lister les conf que vous souhaitez ajouter dans votre dotfile.
Pour cela je vous invite a check en fonctions des outils que vous utilise, pour recuperer leur conf. ex [vscode](https://anhari.dev/blog/saving-vscode-settings-in-your-dotfiles)

- 3. Dans votre dossier dotfiles, organiser l'architecture comme vous le souhaitez.

    Par exemple pour moi :
    ~/dotfiles/
            /vscode/
            /nvim/
            /alacritty/
            /zsh/
            /scripts/

- 4. Copier vos differentes conf dans les dossier respectifs, puis supprimer l'ancien.

    Ex : 
    cp ~/.config/Code/User/settings.json ~/dotfiles/vscode/
    cp ~/.config/Code/User/keybindings.json ~/dotfiles/vscode/
    cp ~/.config/Code/User/snippets/c.json ~/dotfiles/vscode/
    rm ~/.config/Code/User/settings.json
    rm ~/.config/Code/User/keybindings.json
    rm ~/.config/Code/User/snippets/c.json

- 5. On creer ensuite un lien symbolique vers le fichier dans notre dossier dotfiles

    ln -s ~/dotfiles/vscode/settings.json ~/.config/Code/User/settings.json
    ln -s ~/dotfiles/vscode/keybindings.json ~/.config/Code/User/keybindings.json
    ln -s ~/dotfiles/vscode/c.jsoni ~/.config/Code/User/snippets/c.json

- 6. On peut ensuite init notre repo git et finaliser sa creation.

    cd ~/dotfiles/
    git init
    git commit -m "first commit / add dotfiles"
    git branch -M main
    git remote add origin "your repo address"
    git push

Vous avez mainteant un dotfiles, avec vos configurations dessus. Si vous faite un changement dans votre conf, il vous suffit
de git add , git commit , et push et les changement se feront. C'est possible d'automatiser cette tache avec diverse outils.
Par exemple [rcm](https://github.com/thoughtbot/rcm) qui s'occupe meme de la creation de lien symbolique.
Nous verront aussi une autre mainiere avec ansible au prochain atelier.
