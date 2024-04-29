<h1 align="center">Ansible</h1>

Nous voila enfin sur la derniere partie de cet atelier, premierement merci a celles et ceux qui sont reste
jusqu'ici. Pour cette derniere etape nous allons decouvir ansible. 

Ansible est une plateforme open-source de gestion de configuration et d'automatisation des déploiements.
Grâce à sa simplicité et à son approche basée sur YAML, Ansible permet de provisionner,
de configurer et de déployer des infrastructures informatiques de manière efficace et
reproductible, facilitant ainsi la gestion des environnements informatiques à grande échelle.
Pendant cet atelier nous allons voir comment utiliser cet outils pour automatiser
d'installation de notre environement de travail.

## Prerequis

Pour commencer cet atlelier, il faut avoir copier le dossier AtelierDP :

```bash
cd /
cd sgroinfre/cassie
cp -R sgoinfre/cassie/AtelierDP ~/sgoinfre/
```

## Ansible

Pour installer ansible la [doc](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#installing-ansible-on-specific-operating-systems)

Sur un dotfile quelque par dans l'internet, avec seulement cette commande quelqu'un
peu installer son environement de travail.

```bash
ansible-playbook --ask-become-pass bootstrap.yml
```

Qu'est ce que bootstrap.yml ?
En voici un exemple :

```yaml
- name: Bootstrap development environment
  hosts: localhost

  tasks:
  - name: Install packages with apt
    become: yes
    ansible.builtin.apt:
      name:
        - git
        - tmux
      state: present
```

### Playbook

En terminologie Ansible le fichier `bootstrap.yml` est appele [playbook](https://docs.ansible.com/ansible/latest/user_guide/playbooks_intro.html).
Les playbooks sont ecrit en [YAML](https://learnxinyminutes.com/docs/yaml/).

Un playbook peux contenir plusieurs play / pieces et dans une piece / play plusieurs tasks / taches.
Dans l'exemple si dessus le playbook possede une play avec une task : "Install packages with apt"

### Host & Inventory

Ansible peut executer des taches / tasks en remote ou en local. 
Pendant cet atelier on va se focus sur la partie local.

```yaml {2}
- name: Bootstrap development environment
  hosts: localhost
```

Par defaut ansible defini host en local, il ne sera pas necessaire pour cet atelier.

### Tasks

On va ce focus sur les differentes parties des tasks.

```yaml
  tasks:
  - name: Install packages with apt
    become: yes
    ansible.builtin.apt:
      name:
        - git
        - tmux
      state: present
```

#### Become

Permet de `become` un autre utilisateur pendant que l'on fait cette task.
L'utilsateur par default etant `root`. Cela revient a utiliser sudo pour cette task.
Et enfin c'est pour cela que dans la commande si dessus on utilise l'option `--ask-become-pass` (ou `-K`).

#### Modules

`ansible.builtin.apt` est un module de Ansible, ansible possede plusieurs modules built-ini ([liste](https://docs.ansible.com/ansible/latest/module_plugin_guide/index.html)).
Il existe des modules pour la majorite des gestionnaire de packets des differentes distro linux.
Aussi il a des modules communautaire par exemple pour [Homebrew](https://docs.ansible.com/ansible/latest/collections/community/general/homebrew_module.html) pour macos.

Un module Ansible a besoin d'arguments pour accomplir sa task.
Par exemple dans le cas si dessous on peut donner une liste de packet dans [`name`](https://docs.ansible.com/ansible/2.9/modules/apt_module.html#parameter-name)
et le [`state`](https://docs.ansible.com/ansible/2.9/modules/apt_module.html#parameter-state) desire.

```yaml {4-8}
  tasks:
  - name: Install packages with apt
    become: yes
    ansible.builtin.apt:
      name:
        - git
        - tmux
      state: present # peut etre aussi 'latest' or 'absent'
```
#### Idempotence

Les playbooks de Ansible sont fait pour etre idempotent, qu'importe le nombre de fois
que vous les lancer, la machine finira dans le meme etat.

### Facts and conditionals

Imaginont maintenant que j'utilise macOS et Ubuntu.
On ne peut pas utiliser pour des deux apt..
On peut donc utiliser des conditions a nos tasks.

```yaml {9, 19}
  tasks:
  - name: Install packages with apt
    become: yes
    ansible.builtin.apt:
      name:
        - git
        - tmux
      state: present
    when: ansible_distribution == "Ubuntu"

  tasks:
  - name: Install packages with brew
    become: yes
    community.general.homebew:
      name:
        - git
        - tmux
      state: present
    when: ansible_distribution == "MacOSX"
```
La task sera effectue que si la condition `when` est `true`.

### Ansible Galaxy

Si dessus le module `community.general.homebrew` n'est pas built-in.
Pour l'installer vous devez utiliser [Ansible Galaxy](https://galaxy.ansible.com/ui/)


```bash
$ ansible-galaxy collection install community.general
```

### Roles

Les role dans Ansible sont une maniere d'organiser vos tasks.
C'est aussi le format utiliser les tasks d'autre personnes.

Exemple : 

```bash
ansible-galaxy role install gantsign.visual-studio-code
```

Il est possible de customizer des roles.

```yaml
    - role: gantsign.visual-studio-code
      users:
        - username: something
          visual_studio_code_extensions:
            - "eamodio.gitlens"
            - "kahole.magit"
            - "PhilHindle.errorlens"
            - "sleistner.vscode-fileutils"
            - "vscodevim.vim"
```

L'objectifs principal des roles est d'organiser des tasks.
Exemple on creer le role nvim , avec cette structure :

```bash
$ tree roles/nvim
roles/nvim
└── tasks
    ├── fedora.yml
    ├── macos.yml
    ├── main.yml
    └── ubuntu.yml

1 directory, 4 files
```

Le fichier main.yml import les tasks d'autre fichiers.

```yaml
- name: Build nvim from source in Ubuntu
  import_tasks: ubuntu.yml
  when: ansible_distribution == "Ubuntu"

- name: Build nvim from source in Fedora
  include_tasks: fedora.yml
  when: ansible_distribution == "Fedora"

- name: Install nvim with Homebrew in macOS
  import_tasks: macos.yml
  when: ansible_distribution == "MacOSX"
```

La doc sur les roles [ici](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_reuse_roles.html)

Et un [exemple](https://github.com/phelipetls/dotfiles) de dotfile qui utilse Ansible.

## Atelier

Durant cet atelier en utilisant la vm que vous avez recuperer hier et votre dotfile, vous devrez 
commencer a automatiser votre dotfile.
Utilisez les infos si dessus, les docs de ansible et regarder des exemples de dotfile.

[Github Awesome dotfile](https://github.com/webpro/awesome-dotfiles).
Pleins d'info et ressouces sur les dotfiles.

## Sources

Pour cette partie je majoritairement traduit ce [tutoriel](https://phelipetls.github.io/posts/introduction-to-ansible/#building-neovim-from-source)
Que je vous conseil de lire si ca vous interesse.
