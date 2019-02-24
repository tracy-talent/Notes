python号称人工智能语言，现在可算大热，这篇博客将介绍如何用vim打造一款自己专属的python编程环境。

## step1

由于安装YouCompleteMe需要vim8.0及以上版本，所以得安装使用vim的8.0及以上版本，使用vim --version查看自己的vim版本，如果没达到要求可以参考我的另一篇博客[vim8.0安装教程](https://www.cnblogs.com/brooksj/p/10428705.html)进行安装。接着使用git安装vim的包管理工具Vundle

```shell
git clone https://github.com/gmarik/Vundle.vim.git ~/.vim/bundle/Vundle.vim
```

然后在vim的配置文件~/.vimrc中添加如下内容

```shell
set nocompatible              " required
filetype off                  " required
 
" set the runtime path to include Vundle and initialize
set rtp+=~/.vim/bundle/Vundle.vim
call vundle#begin()
 
" alternatively, pass a path where Vundle should install plugins
"call vundle#begin('~/some/path/here')
 
" let Vundle manage Vundle, required
<strong>Plugin 'gmarik/Vundle.vim'</strong>
 
" Add all your plugins here (note older versions of Vundle used Bundle instead of Plugin)
 
" All of your Plugins must be added before the following line
call vundle#end()            " required
filetype plugin indent on    " required
```

配置好之后执行vim命令打开编辑窗口，输入命令PLuginList若能显示已安装的插件则表明Vundle已安装成功，命令PLuginInstall可用于安装插件，PluginClean可用于卸载插件，不过需要先在~/.vimrc中将不要下载的插件注释掉或者去除。

## step2

在\~/.vimrc中添加让vundle安装的插件并且对插件进行配置，这里直接贴出我\~/vim.rc的全部内容

```shell
set nocompatible              " required
filetype off                  " required
 
"设置Vundle的运行路径
set rtp+=/home/brooksj/.vim/bundle/Vundle.vim
"设置插件的安装路径,vundle插件起始标志
call vundle#begin('/home/brooksj/.vim/bundle')
"让vundle管理插件版本
Plugin 'VundleVim/Vundle.vim'
"添加nerdtree插件
Plugin 'scrooloose/nerdtree'
"使用tab键切换窗口与目录树
Plugin 'jistr/vim-nerdtree-tabs'
"添加jedi-vim代码补全插件
"Plugin 'davidhalter/jedi-vim'
Plugin 'Valloric/YouCompleteMe'
"添加PEP8代码风格检查
Plugin 'nvie/vim-flake8'
"配色方案
Plugin 'jnurmine/Zenburn'
Plugin 'altercation/vim-colors-solarized'
Plugin 'tomasr/molokai'
"代码折叠插件
Plugin 'tmhedberg/SimpylFold'
"自动缩进
Plugin 'vim-scripts/indentpython.vim'
"在vim的normal模式下搜索文件
Plugin 'kien/ctrlp.vim'
"Powerline状态栏
Plugin 'Lokaltog/powerline', {'rtp': 'powerline/bindings/vim/'}
"你的所有插件需要在下面这行之前
call vundle#end() 
"设置显示powerline
set laststatus=2
"设置分割窗口
set splitbelow
set splitright
"设置窗口移动快捷键
nnoremap <C-J> <C-W><C-J>
nnoremap <C-K> <C-W><C-K>
nnoremap <C-L> <C-W><C-L>
nnoremap <C-H> <C-W><C-H>
"设置按F2启动NerdTree
map <F2> :NERDTreeToggle<CR>
"youcompleteme  默认tab  s-tab 和自动补全冲突
""let g:ycm_key_list_select_completion=['<c-n>']
let g:ycm_key_list_select_completion = ['<Down>']
"let g:ycm_key_list_previous_completion=['<c-p>']
let g:ycm_key_list_previous_completion = ['<Up>']
"关闭加载.ycm_extra_conf.py提示
let g:ycm_confirm_extra_conf=0 
" 开启 YCM 基于标签引擎
let g:ycm_collect_identifiers_from_tags_files=1 
" 从第2个键入字符就开始罗列匹配项
let g:ycm_min_num_of_chars_for_completion=2 
" 禁止缓存匹配项,每次都重新生成匹配项
let g:ycm_cache_omnifunc=0  
" 语法关键字补全
let g:ycm_seed_identifiers_with_syntax=1
"force recomile with syntastic
nnoremap <F5> :YcmForceCompileAndDiagnostics<CR>    
"nnoremap <leader>lo :lopen<CR> "open locationlist
"nnoremap <leader>lc :lclose<CR>    "close locationlist
inoremap <leader><leader> <C-x><C-o>
"在注释输入中也能补全
let g:ycm_complete_in_comments = 1
"在字符串输入中也能补全
let g:ycm_complete_in_strings = 1
"注释和字符串中的文字也会被收入补全
let g:ycm_collect_identifiers_from_comments_and_strings = 0
"let g:ycm_autoclose_preview_window_after_completion=1
 
"隐藏目录树种的.pyc文件
let NERDTreeIgnore=['\.pyc$', '\~$'] "ignore files in NERDTree
 
"设置主题颜色，以及设置快捷键F5
set t_Co=256
set background=dark
if has('gui_running')
  colorscheme solarized
else
  colorscheme molokai
  "let g:molokai_original=1
endif
call togglebg#map("<F3>")

if &diff
    colors blue
endif
 
"开启代码折叠
set foldmethod=indent
set foldlevel=99
"设置快捷键为空格
nnoremap <space> za
"显示折叠代码的文档字符串
let g:SimpylFold_docstring_preview=1
 
"python代码缩进PEP8风格
au BufNewFile,BufRead *.py,*.pyw set tabstop=4
au BufNewFile,BufRead *.py,*.pyw set softtabstop=4
au BufNewFile,BufRead *.py,*.pyw set shiftwidth=4 
au BufNewFile,BufRead *.py,*.pyw set expandtab
au BufNewFile,BufRead *.py,*.pyw set textwidth=79
au BufNewFile,BufRead *.py,*.pyw set autoindent
au BufNewFile,BufRead *.py,*.pyw set fileformat=unix
 
"对其他文件类型设置au命令
au BufNewFile,BufRead *.js, *.html, *.css set tabstop=2
au BufNewFile,BufRead *.js, *.html, *.css set softtabstop=2
au BufNewFile,BufRead *.js, *.html, *.css set shiftwidth=2
"高亮显示行伟不必要的空白字符
highlight Whitespace ctermbg=red guibg=red
au BufRead,BufNewFile *.py,*.pyw,*.c,*.h match Whitespace /\s\+$\ \+/
"设置行号显示
set nu
 
"设置utf-8编码
set encoding=utf-8
 
let python_highlight_all=1
syntax on
filetype plugin indent on
set backspace=indent,eol,start
set cursorline
set history=1000
set fileencodings=utf-8,gb18030,utf-16,big5
set hlsearch
set clipboard=unnamed
set expandtab
set softtabstop=4
set tabstop=4
set shiftwidth=4
```

对安装的几个插件作一个简要的介绍：

* nerdtree可用于在vim窗口下查看文件的数形结构
* YouCompleteMe可提供语法高亮以及代码提示等，打造IDE必备
* vim-flake8支持python PEP8代码风格检查
* indentpython.vim用于写python时自动缩进
* SimpylFold用于代码折叠(我配置了快捷键space或者za来折叠代码)
* ctrlp用于查找文件(按下ctrl+p即进入文件查找功能)
* powerline是一款比较炫酷的状态栏工具，显示vim状态及其打开文件的一些信息(我安装powerline时提示我powerline只兼容python2.7以及python3.2版本，所以得注意你所使用的python版本)
* vim-colors-solarized、Zenburn以及molokai是三款好看的配色方案，可以自己在\~/.vimrc中配置时使用哪种颜色方案

## step3

终端执行vim命令打开vim，然后输入命令PLuginInstall对上面配置的插件进行安装，下面是我安装好之后插件截图

<div align="center">
    <img src="https://raw.githubusercontent.com/tracy-talent/Notes/master/imgs/vundle_plugin.png">
</div>

## step4

YouCompleteMe的安装比较特殊，使用Vundle安装好之后还需要进入到~/.vim/bundle/YouCompleteMe目录下安装一次才能正常使用YouCompleteMe的全部功能

```shell
./install.py --clang-completer
```

如果还想支持go和node.js的自动补全可以

```	shell
./install.py --clang-completer --gocode-completer --tern-completer
```

后期需要其他的语言补全可以上网查一下对应的安装选项然后附加在./install.py之后执行即可。

到此vim的python配置就全部完成了，且看vim的效果图

<div align="center">
    <img src="https://raw.githubusercontent.com/tracy-talent/Notes/master/imgs/vim效果图.png">
</div>



参考：

https://www.cnblogs.com/cjy15639731813/p/5886158.html

https://blog.csdn.net/nzyalj/article/details/75331822

