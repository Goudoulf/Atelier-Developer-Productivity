<h1 align="center">Atelier Developer Productivity</h1>

## Vim Motions

Encore plus que sur d'autre ide, il est neccessaire d'utiliser les raccourcis sur Neovim.
On parle ici des vim Motions, permetant de gagner une fluidite et une rapidite de devloppement sans pareil.
Si vous n'etes pas encore familier avec les vim Motions je vous conseil vim tutor.
>:tutor

Qui est l'intro parfaite au vim motions.

Sinon voici quelque lien pour vous aidez :

- [Vim Cheat Sheet](https://vim.rtorr.com/)
- [Good site to learn](https://www.barbarianmeetscoding.com/boost-your-coding-fu-with-vscode-and-vim/moving-blazingly-fast-with-the-core-vim-motions/)
- [Vim be good](https://github.com/ThePrimeagen/vim-be-good) 

Il n'est pas necessaire de connaitre tous les vim Motion, ajouter en au fur et
a mesure a votre arsenal pour quelle devient seconde nature.

Une petite liste de certain que je trouve super :

    y + i + delimilter : Ca copy a l'interieur du delimiter (ex yi" copy le content des guillemets)
    d + i + delimilter : Ca delete a l'interieur du delimiter (ex di{ delete entre les accolades)
    gg :aller en haut du fichier
    G : aller en bas du fichier
    Ctrl + 6 : switch entre l'ancien fichier ouvert et celui ou vous etes
    :Ex : permet d'aller dans Netwr, possible de le bind
    Ctrl + d : Dessend dans le fichier par demi page
    Ctrl + u : Monte dans le fichier par demi page

Plus tous les raccourcis ajouter par des plugins et des customs.

## Addon

- Plugin manager : [lazy.nvim](https://github.com/folke/lazy.nvim)
- Un plugin presque obligatoire : [telescope.nvim](https://github.com/nvim-telescope/telescope.nvim)
- Pour aider a apprendre les raccourcis, tiptop : [Which Key.nvim](https://github.com/folke/which-key.nvim)
- Plugin de commentaire : [comment.nvim](https://github.com/numToStr/Comment.nvim)
- Aide a utilise nvim de la bonne maniere : [hardtime.nvim](https://github.com/m4xshen/hardtime.nvim)
- Pour installer un LSP : [mason.nvim](https://github.com/williamboman/mason.nvim)
- Un super plugin git : [fugitive.nvim](https://github.com/tpope/vim-fugitive?tab=readme-ov-file)

- Git qui repertorie pleins de plugin : [awesome nvim](https://github.com/rockerBOO/awesome-neovim)


## luasnip

Plugin qui permet l'utilisation de snippet :

[luasnip](https://github.com/L3MON4D3/LuaSnip)

## Petit plus

Si vous voulez switch sur nvim je vous conseil [kickstart.nvim](https://github.com/nvim-lua/kickstart.nvim)
super pour apprendre a configurer Neovim.
Lizez bien le git et tous le init.lua.
