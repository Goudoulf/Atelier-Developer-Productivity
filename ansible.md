<h1 align="center">Ansible</h1>

Nous voilà enfin sur la dernière partie de cet atelier, premièrement merci à celles et ceux qui sont restés
jusqu'ici. Pour cette dernière étape nous allons découvrir ansible. 

Ansible est une plateforme open-source de gestion de configuration et d'automatisation des déploiements.
Grâce à sa simplicité et à son approche basée sur YAML, Ansible permet de provisionner,
de configurer et de déployer des infrastructures informatiques de manière efficace et
reproductible, facilitant ainsi la gestion des environnements informatique à grande échelle.
Pendant cet atelier nous allons voir comment utiliser cet outil pour automatiser
l'installation de notre environnement de travail.

## Pré-requis

Pour commencer cet atelier, il faut avoir copier le dossier AtelierDP :

```bash
cd /
cd sgroinfre/cassie
cp -R sgoinfre/cassie/AtelierDP ~/sgoinfre/
```

## Ansible

Pour installer ansible la [doc](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#installing-ansible-on-specific-operating-systems)

Sur un dotfile quelque part dans l'internet, avec seulement cette commande quelqu'un
peut installer son environnement de travail.

```bash
ansible-playbook --ask-become-pass bootstrap.yml
```

Qu'est-ce que bootstrap.yml ?
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

En terminologie Ansible le fichier `bootstrap.yml` est appelé [playbook](https://docs.ansible.com/ansible/latest/user_guide/playbooks_intro.html).
Les playbooks sont écrits en [YAML](https://learnxinyminutes.com/docs/yaml/).

Un playbook peut contenir plusieurs play / pièces et dans une pièce / play plusieurs tasks / tâches.
Dans l'exemple ci-dessus le playbook possède une play avec une task : "Install packages with apt"

### Host & Inventory

Ansible peut exécuter des tâches / tasks en remote ou en local. 
Pendant cet atelier on va se focus sur la partie local.

```yaml {2}
- name: Bootstrap development environment
  hosts: localhost
```

Par défaut ansible définit host en local, il ne sera pas nécessaire pour cet atelier.

### Tasks

On va se focus sur les différentes parties des tasks.

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
L'utilsateur par défaut étant `root`. Cela revient à utiliser sudo pour cette task.
Et enfin c'est pour cela que dans la commande ci-dessus on utilise l'option `--ask-become-pass` (ou `-K`).

#### Modules

`ansible.builtin.apt` est un module de Ansible, ansible possède plusieurs modules built-ini ([liste](https://docs.ansible.com/ansible/latest/module_plugin_guide/index.html)).
Il existe des modules pour la majorité des gestionnaires de packets des différentes distro linux.
Aussi il y a des modules communautaires par exemple pour [Homebrew](https://docs.ansible.com/ansible/latest/collections/community/general/homebrew_module.html) pour macos.

Un module Ansible a besoin d'arguments pour accomplir sa task.
Par exemple dans le cas ci-dessous on peut donner une liste de packets dans [`name`](https://docs.ansible.com/ansible/2.9/modules/apt_module.html#parameter-name)
et le [`state`](https://docs.ansible.com/ansible/2.9/modules/apt_module.html#parameter-state) desire.

```yaml {4-8}
  tasks:
  - name: Install packages with apt
    become: yes
    ansible.builtin.apt:
      name:
        - git
        - tmux
      state: present # peut être aussi 'latest' or 'absent'
```
#### Idempotence

Les playbooks de Ansible sont faits pour être idempotent, qu'importe le nombre de fois
où vous les lancez, la machine finira dans le même état.

### Facts and conditionals

Imaginons maintenant que j'utilise macOS et Ubuntu.
On ne peut pas utiliser pour des deux apt..
On peut donc utiliser des conditions à nos tasks.

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
La task ne sera effectuée que si la condition `when` est `true`.

### Ansible Galaxy

Ci-dessus le module `community.general.homebrew` n'est pas built-in.
Pour l'installer vous devez utiliser [Ansible Galaxy](https://galaxy.ansible.com/ui/)


```bash
$ ansible-galaxy collection install community.general
```

### Rôles

Les rôles dans Ansible sont une manière d'organiser vos tasks.
C'est aussi le format utilisé par les tasks d'autres personnes.

Exemple : 

```bash
ansible-galaxy role install gantsign.visual-studio-code
```

Il est possible de customizer des rôles.

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

L'objectif principal des rôles est d'organiser des tasks.
Par exemple, on créé le rôle nvim, avec cette structure :

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

Le fichier main.yml import les tasks d'autres fichiers.

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

La doc sur les rôles [ici](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_reuse_roles.html)

Et un [exemple](https://github.com/phelipetls/dotfiles) de dotfile qui utilise Ansible.

## Atelier

Durant cet atelier en utilisant la vm que vous avez recupéré hier et votre dotfile, vous devrez 
commencé à automatiser votre dotfile.
Utilisez les infos ci-dessus, les docs de ansible et regarder des exemples de dotfile.

[Github Awesome dotfile](https://github.com/webpro/awesome-dotfiles).
Plein d'infos et ressources sur les dotfiles.

## Sources

Pour cette partie j'ai majoritairement traduit ce [tutoriel](https://phelipetls.github.io/posts/introduction-to-ansible/#building-neovim-from-source)
Que je vous conseille de lire si ça vous intéresse.
