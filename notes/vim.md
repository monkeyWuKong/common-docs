
### centos7 升级vim8

```
yum remove vim -y
yum install ncurses-devel python-devel -y
git clone https://github.com/vim/vim.git
cd vim/src

打开Makefile
CONF_OPT_PYTHON = --enable-pythoninterp

make
make install
#设置环境变量，打开`/etc/profile`,最后一行写入
PATH=$PATH:/usr/local/bin/
```

如果之前没有python支持，增加python支持，则需要重新编译

```
cd vim/src
make distclean
./configure --enable-pythoninterp=yes --with-python-config-dir=/usr/lib/python2.7/config
make
make install
```

### 配置vundle

https://github.com/VundleVim/Vundle.vim

`git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim`

```
set nocompatible              " be iMproved, required
filetype off                  " required

syntax enable
syntax on

set number

set expandtab
set tabstop=4


" set the runtime path to include Vundle and initialize
set rtp+=~/.vim/bundle/Vundle.vim


map <F2> :NERDTreeToggle<CR>
autocmd bufenter * if (winnr("$") == 1 && exists("b:NERDTreeType") &&b:NERDTreeType == "primary") | q | endif


call vundle#begin()
" " alternatively, pass a path where Vundle should install plugins
"call vundle#begin('~/some/path/here')
"
" " let Vundle manage Vundle, required

Plugin 'VundleVim/Vundle.vim'
Plugin 'scrooloose/nerdtree'

Plugin 'fatih/vim-go'

"
" " The following are examples of different formats supported.
" " Keep Plugin commands between vundle#begin/end.
" " plugin on GitHub repo
" Plugin 'tpope/vim-fugitive'
" " plugin from http://vim-scripts.org/vim/scripts.html
" Plugin 'L9'
" " Git plugin not hosted on GitHub
" Plugin 'git://git.wincent.com/command-t.git'
" " git repos on your local machine (i.e. when working on your own plugin)
" Plugin 'file:///home/gmarik/path/to/plugin'
" " The sparkup vim script is in a subdirectory of this repo called vim.
" " Pass the path to set the runtimepath properly.
" Plugin 'rstacruz/sparkup', {'rtp': 'vim/'}
" " Install L9 and avoid a Naming conflict if you've already installed a
" " different version somewhere else.
" Plugin 'ascenator/L9', {'name': 'newL9'}
"
" " All of your Plugins must be added before the following line
call vundle#end()            " required

filetype plugin indent on    " required
" " To ignore plugin indent changes, instead use:
" "filetype plugin on
" "
" " Brief help
" " :PluginList       - lists configured plugins
" " :PluginInstall    - installs plugins; append `!` to update or just
" :PluginUpdate
" " :PluginSearch foo - searches for foo; append `!` to refresh local cache
" " :PluginClean      - confirms removal of unused plugins; append `!` to
" auto-approve removal
" "
" " see :h vundle for more details or wiki for FAQ
" " Put your non-Plugin stuff after this line
```

按需配置

启动 vim
执行 `:PluginInstall`即可自动安装插件。

### 安装文件浏览器nerdtree

插件官网： http://www.vim.org/scripts/script.php?script_id=1658

github： https://github.com/scrooloose/nerdtree

```
git clone https://github.com/scrooloose/nerdtree.git ~/.vim/bundle/nerdtree
```

### 一键配置参考
https://github.com/chxuan/vimplus
