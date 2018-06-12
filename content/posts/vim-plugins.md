---
title: vim plugins
date: 2016-04-27 15:19:40
tags: 
    - vim
    - production
---
工欲善其事,必先利其器.对于天天在类Unix写后台的代码的人来说,便捷的插件会使你写代码的速度加快很多.下面介绍一下我经常使用的插件(直接粘贴的英文,英文不好):


|插件名称|简介|
|----|----|
|Vundle|统一管理所有vim插件的工具,让你管理插件very easy|
|google/vim-maktaba|Maktaba is a vimscript plugin library. It is designed for plugin authors|
|google/vim-codefmt|codefmt is a utility for syntax-aware code formatting. It contains several built-in formatters, and allows new formatters to be registered by other plugins.|
|google/vim-glaive|Glaive is a utility for configuring maktaba plugins.|
|tpope/vim-fugitive|I'm not going to lie to you; fugitive.vim may very well be the best Git wrapper of all time.|
|vim-scripts/LargeFile|Editing large files can be a time consuming process as Vim is working on a number of things behind the scenes, such as maintaining an undo database, searching for a syntax highlighting synchronization point, etc.  LargeFile.vim is a very small "plugin"; mostly, its just an autocmd that disables certain features of vim in the interests of speed.|
|scrooloose/nerdcommenter|Vim plugin for intensely orgasmic commenting|
|Lokaltog/vim-easymotion|Vim motions on speed!|
|Raimondi/delimitMate|This plug-in provides automatic closing of quotes, parenthesis, brackets, etc., besides some other related features that should make your time in insert mode a little bit easier, like syntax awareness (will not insert the closing delimiter in comments and other configurable regions), and expansions (off by default), and some more.|
|mbbill/fencview|Auto detect CJK and Unicode file encodings.|
|vim-scripts/Visual-Mark|Visual mark, similar to UltraEdit's bookmark|
|Valloric/YouCompleteMe|A code-completion engine for Vim|
|google/vim-searchindex|This plugin shows how many times does a search pattern occur in the current buffer. After each search, it displays total number of matches, as well as the index of a current match, in the command line|
|fatih/vim-go|Go (golang) support for Vim, which comes with pre-defined sensible settings (like auto gofmt on save), with autocomplete, snippet support, improved syntax highlighting, go toolchain commands, and more. If needed vim-go installs all necessary binaries for providing seamless Vim integration with current commands. It's highly customizable and each individual feature can be disabled/enabled easily.|
|scrooloose/nerdtree|The NERD tree allows you to explore your filesystem and to open files and directories. It presents the filesystem to you in the form of a tree which you manipulate with the keyboard and/or mouse. It also allows you to perform simple filesystem operations.|
|Xuyuanp/nerdtree-git-plugin|A plugin of NERDTree showing git status flags. Works with the LATEST version of NERDTree.|
|google/vim-colorscheme-primary|google Vim colors scheme|
|airblade/vim-gitgutter|A Vim plugin which shows a git diff in the 'gutter' (sign column). It shows whether each line has been added, modified, and where lines have been removed. You can also stage and undo individual hunks.|

## Make cscope support for go
{% codeblock lang:bash %}
find . -name "*.go" -print > cscope.files
if cscope -b -k; then
    echo "Done"
else
    echo "Failed"
    exit 1
fi
{% endcodeblock %}

然后下面粘贴一下我的.vimrc配置文件
{% codeblock .vimrc lang:vim %}
set nocompatible
filetype off
set rtp+=~/.vim/bundle/Vundle.vim
call vundle#begin()
Plugin 'VundleVim/Vundle.vim'
Plugin 'google/vim-maktaba'
Plugin 'google/vim-codefmt'
Plugin 'google/vim-glaive'
Plugin 'tpope/vim-fugitive'
Plugin 'vim-scripts/LargeFile'
Plugin 'scrooloose/nerdcommenter'
"Plugin 'altercation/vim-colors-solarized'
Plugin 'Lokaltog/vim-easymotion'
Plugin 'Raimondi/delimitMate'
Plugin 'mbbill/fencview'
Plugin 'vim-scripts/Visual-Mark'
Plugin 'Valloric/YouCompleteMe'
Plugin 'google/vim-searchindex'
Plugin 'fatih/vim-go'
Plugin 'scrooloose/nerdtree'
Plugin 'Xuyuanp/nerdtree-git-plugin'
Plugin 'google/vim-colorscheme-primary'
Plugin 'airblade/vim-gitgutter'
Plugin 'artur-shaik/vim-javacomplete2'
Plugin 'majutsushi/tagbar'
call vundle#end()
filetype plugin indent on
call glaive#Install()
call maktaba#plugin#Detect()

" map leader key
let mapleader = ","

" Large file
let g:LargeFile=10

" File encoding dectection
set fileencodings=ucs-bom,utf-8,cp936,gb18030,big5,euc-jp,euc-kr,latin1
set encoding=utf-8

" Tab Settings
set smarttab
set tabstop=2
set softtabstop=2
set shiftwidth=2
set expandtab

" Fix backspace indentation
set backspace=indent,eol,start

" Convince Vim it can use 256 colors
set t_Co=256

let no_buffers_menu=1

" Code Folding, everything foleded by default
set foldmethod=indent
set foldlevel=99
set foldenable

" Turn off annoying swapfiles
set noswapfile

" Enable hidden buffers
set hidden

" Enable automatic title setting for terminals
set title
set titleold="Terminal"
set titlestring=%F\ -\ Vim

" Activate a permanent ruler
set ruler

" Disable the stupid pydoc preview window for the omni completion
set completeopt-=preview

" Global by default
set gdefault

" Better Search
set hlsearch

" Hide matched on <Leader>space
nnoremap <leader><space> :nohlsearch<CR>

" goto the middle of a line
nnoremap <leader>m :call cursor(0, len(getline('.'))/2)<CR>

" Quit windows on <leader>q
nnoremap <leader>q :q<CR>

" substitute
nnoremap <leader>ss :%s/

" next split and prev split
nnoremap <leader>wl <c-w>l
nnoremap <leader>wh <c-w>h
nnoremap <leader>wj <c-w>j
nnoremap <leader>wk <c-w>k

" vsplit map
nnoremap <leader>vp :vsplit<CR>

" fencview
"let g:fencview_autodetect=1

" Make the commadn line two lines high and change the statusline display to
" something that looks useful.
set cmdheight=2
set laststatus=2
set showcmd
set showmode
set number

" SuperTab
let g:SuperTabDefaultCompletionType = "context"

" Solarized Vim
syntax enable
set background=dark
"let g:solarized_termtrans=1
"let g:solarized_termcolors=256
"let g:solarized_contrast="high"
"let g:solarized_visibility="high"
"colorscheme solarized
colorscheme primary

" set paste
noremap <leader>sp :set paste<CR>
noremap <leader>cp :set nopaste<CR>

" delimitMate
let g:delimitMate_autoclose=1
let g:delimitMate_matchpairs="(:),[:],{:}"
let g:delimitMate_balance_matchpairs=1
let g:delimitMate_expand_cr=1

" ycm
let g:ycm_confirm_extra_conf=0
nnoremap <f4> :YcmDiag<CR>

" not change clipboard
xnoremap p pgvy

" nerdTree for git
let g:NERDTreeIndicatorMapCustom = {
    \ "Modified"  : "✹",
    \ "Staged"    : "✚",
    \ "Untracked" : "✭",
    \ "Renamed"   : "➜",
    \ "Unmerged"  : "═",
    \ "Deleted"   : "✖",
    \ "Dirty"     : "✗",
    \ "Clean"     : "✔︎",
    \ "Unknown"   : "?"
    \ }

" open nerdTree
map <leader>t :NERDTreeToggle<CR>

" gitgutter
nmap ]h <Plug>GitGutterNextHunk
nmap [h <Plug>GitGutterPrevHunk

" java complete2
autocmd FileType java setlocal omnifunc=javacomplete#Complete
let g:JavaComplete_UseFQN=1
nmap <F5> <Plug>(JavaComplete-Imports-Add)
imap <F5> <Plug>(JavaComplete-Imports-Add)

" gotags
let g:tagbar_type_go = {
    \ 'ctagstype' : 'go',
    \ 'kinds'     : [
        \ 'p:package',
        \ 'i:imports:1',
        \ 'c:constants',
        \ 'v:variables',
        \ 't:types',
        \ 'n:interfaces',
        \ 'w:fields',
        \ 'e:embedded',
        \ 'm:methods',
        \ 'r:constructor',
        \ 'f:functions'
    \ ],
    \ 'sro' : '.',
    \ 'kind2scope' : {
        \ 't' : 'ctype',
        \ 'n' : 'ntype'
    \ },
    \ 'scope2kind' : {
        \ 'ctype' : 't',
        \ 'ntype' : 'n'
    \ },
    \ 'ctagsbin'  : 'gotags',
    \ 'ctagsargs' : '-sort -silent'
\ }

" ctag
nmap <leader>c :TagbarToggle<CR>
{% endcodeblock %}
为了每次插件能与远端一直同步,可以用checkout我的vim配置项目
```bash
git clone https://github.com/mYmNeo/vim.git ~/.vim
cd ~/.vim
./install.sh
```