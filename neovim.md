<h1 align="center">Atelier Developer Productivity</h1>

## Vim Motions

Encore plus que sur d'autres ide, il est nécessaire d'utiliser les raccourcis sur Neovim.
On parle ici des vim Motions, permettant de gagner une fluidité et une rapidité de développement sans pareille.
Si vous n'êtes pas encore familier avec les vim Motions je vous conseille vim tutor.
>:tutor

Qui est l'intro parfaite au vim motions.

Sinon voici quelques liens pour vous aider :

- [Vim Cheat Sheet](https://vim.rtorr.com/)
- [Good site to learn](https://www.barbarianmeetscoding.com/boost-your-coding-fu-with-vscode-and-vim/moving-blazingly-fast-with-the-core-vim-motions/)
- [Vim be good](https://github.com/ThePrimeagen/vim-be-good) 

Il n'est pas nécessaire de connaître tous les vim Motion, ajoutez-en au fur et
à mesure a votre arsenal pour qu'elles deviennent seconde nature.

Une petite liste de certains que je trouve super :

    y + i + delimilter : ça copy à l'intérieur du delimiter (ex yi" copy le content des guillemets)
    d + i + delimilter : ça delete à l'intérieur du delimiter (ex di{ delete entre les accolades)
    gg : aller en haut du fichier
    G : aller en bas du fichier
    Ctrl + 6 : switch entre l'ancien fichier ouvert et celui où vous êtes
    :Ex : permet d'aller dans Netwr, possible de le bind
    Ctrl + d : Descend dans le fichier par demi page
    Ctrl + u : Monte dans le fichier par demi page

Plus tous les raccourcis ajouter par des plugins et des customs.

## Addon

- Plugin manager : [lazy.nvim](https://github.com/folke/lazy.nvim)
- Un plugin presque obligatoire : [telescope.nvim](https://github.com/nvim-telescope/telescope.nvim)
- Pour aider à apprendre les raccourcis, tiptop : [Which Key.nvim](https://github.com/folke/which-key.nvim)
- Plugin de commentaire : [comment.nvim](https://github.com/numToStr/Comment.nvim)
- Aide à utiliser nvim de la bonne manière : [hardtime.nvim](https://github.com/m4xshen/hardtime.nvim)
- [Vim Suround](https://github.com/tpope/vim-surround)
- Pour installer un LSP : [mason.nvim](https://github.com/williamboman/mason.nvim)
- Un super plugin git : [fugitive.nvim](https://github.com/tpope/vim-fugitive?tab=readme-ov-file)

- Git qui répertorie pleins de plugin : [awesome nvim](https://github.com/rockerBOO/awesome-neovim)

- Pour le [fun](https://github.com/Eandrju/cellular-automaton.nvim)

## luasnip

Plugin qui permet l'utilisation de snippet :

[luasnip](https://github.com/L3MON4D3/LuaSnip)

## Petit plus

Si vous voulez switch sur nvim je vous conseille [kickstart.nvim](https://github.com/nvim-lua/kickstart.nvim)
super pour apprendre à configurer Neovim.
Lizez bien le git et tous le init.lua.

Plus une [video](https://www.youtube.com/watch?v=m8C0Cq9Uv9o)
