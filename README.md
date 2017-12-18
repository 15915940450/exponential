# exponential


### gvim

_vimrc:

```vim
" ------------------------------
" Name: _vimrc
" Author:Thilina
" Email: 15915940450@139.com
" ------------------------------

" Startup {{{
filetype indent plugin on

" 啓動時窗口最大化
autocmd GUIEnter * simalt ~x

augroup vimrcEx
  au!

  autocmd FileType text setlocal textwidth=78

augroup END

" vim 文件折叠方式为 marker
augroup ft_vim
  au!

  autocmd FileType vim setlocal foldmethod=marker

  " 打开文件总是定位到上次编辑的位置
  autocmd BufReadPost *
  \ if line("'\"") > 1 && line("'\"") <= line("$") |
  \   exe "normal! g`\"" |
  \ endif

augroup END
" }}}

" General {{{
set nocompatible
set nobackup
set noswapfile
set history=1024
set autochdir
set whichwrap=b,s,<,>,[,]
set nobomb
set backspace=indent,eol,start whichwrap+=<,>,[,]

" Vim 的默认寄存器和系统剪贴板共享
set clipboard+=unnamed

" 设置 alt 键不映射到菜单栏
set winaltkeys=no
" }}}

" Lang & Encoding {{{
set fileencodings=utf-8,gbk2312,gbk,gb18030,cp936
set encoding=utf-8
set langmenu=zh_CN
let $LANG = 'en_US.UTF-8'
"language messages zh_CN.UTF-8
" }}}

" GUI {{{
colorscheme desert

source $VIMRUNTIME/delmenu.vim
source $VIMRUNTIME/menu.vim
set cursorline
set hlsearch
set number

" 窗口大小
set lines=35 columns=135

" 分割出来的窗口位于当前窗口下边/右边
set splitbelow
set splitright

"不显示工具/菜单栏
set guioptions-=T
set guioptions-=m
set guioptions-=L
set guioptions-=r
set guioptions-=b

" 使用内置 tab 样式而不是 gui
set guioptions-=e

" set nolist
set listchars=trail:·,extends:>,precedes:<

" Inconsolata字體
set guifont=Inconsolata:h12:cANSI

set statusline=%f
set statusline+=%m
set statusline+=\ %{fugitive#head()}
set statusline+=%=
set statusline+=%{''.(&fenc!=''?&fenc:&enc).''}
set statusline+=/
set statusline +=%{&ff}
set statusline+=\ -\
set statusline+=%l/%L
set statusline+=[%p%%]
set statusline+=\ -\
set statusline +=%1*\ %y\ %*
" }}}

" Format {{{
set autoindent
set smartindent
set tabstop=2
set shiftwidth=2
set softtabstop=2
set expandtab
set foldmethod=indent
syntax on
" }}}

" Keymap {{{
let mapleader=","

nmap <leader>s :source $MYVIMRC<cr>
nmap <leader>e :e $MYVIMRC<cr>
nmap <leader>tn :tabnew<cr>
nmap <leader>tc :tabclose<cr>
" nmap <C-j> <C-W>j
" nmap <C-k> <C-W>k
nmap <M-n> <C-W>h
nmap <M-m> <C-W>l
nnoremap <M-j> :resize +5<cr>
nnoremap <M-k> :resize -5<cr>
nnoremap <M-h> :vertical resize -5<cr>
nnoremap <M-l> :vertical resize +5<cr>
inoremap <M-j> <Down>
inoremap <M-k> <Up>
inoremap <M-n> <left>
inoremap <M-m> <Right>
nnoremap vv ^vg_
inoremap <C-u> <esc>mzgUiw`za
nnoremap <F2> :setlocal number!<cr>
nnoremap <leader>w :set wrap!<cr>
imap <C-v> "+gP
vmap <C-c> "+y
vnoremap <C-C> "+y
vnoremap <C-Insert> "+y
imap <C-V> "+gP
map <S-Insert> "+gP
cmap <C-V> <C-R>+
cmap <S-Insert> <C-R>+
exe 'inoremap <script> <C-V>' paste#paste_cmd['i']
exe 'vnoremap <script> <C-V>' paste#paste_cmd['v']
nmap <silent> <leader>x :!start explorer %:p:h<CR>
nmap <silent> <leader>cmd :!start cmd /k cd %:p:h<cr>
nmap <F3> a<C-R>=strftime("%Y-%m-%d %a %I:%M %p")<CR><Esc>
nmap ,fp :let @*=substitute(expand("%:p"), "/", "\\", "g")<CR>
" }}}

" Plugin {{{
filetype off

set rtp+=$VIM/vimfiles/bundle/Vundle.vim
call vundle#begin('$VIM/vimfiles/bundle')

" ----- Vundle ----- {{{
Plugin 'VundleVim/Vundle.vim'
" }}}
" ----- nerdtree ----- {{{
Plugin 'scrooloose/nerdtree'

 let NERDTreeIgnore=['.idea', '.vscode', 'node_modules', '*.pyc']
 let NERDTreeBookmarksFile = $VIM . '/NERDTreeBookmarks'
 let NERDTreeMinimalUI = 1
 let NERDTreeBookmarksSort = 1
 let NERDTreeShowLineNumbers = 0
 let NERDTreeShowBookmarks = 1
 let g:NERDTreeWinPos = 'right'
 let g:NERDTreeDirArrowExpandable = '+'
 let g:NERDTreeDirArrowCollapsible = '-'
 nmap <leader>n :NERDTreeToggle <cr>
 "
 "if exists('g:NERDTreeWinPos')
     "autocmd vimenter * NERDTree C:\wamp64\www\CMS-FrontEnd
     "autocmd vimenter * NERDTree $HOME\gvimnerdtree
 "endif
" }}}
" ----- ctrlp ----- {{{
Plugin 'kien/ctrlp.vim'
 let g:ctrlp_match_window = 'bottom,order:btt,min:1,max:10,results:10'
 set wildignore+=*\\.git\\*,*\\tmp\\*,*.swp,*.zip,*.exe,*.pyc
" }}}
" ----- nerdcommenter ----- {{{
Plugin 'scrooloose/nerdcommenter'
" }}}
" ----- emmet-vim ----- {{{
Plugin 'mattn/emmet-vim'
" }}}
" ----- vim-fugitive(expo) ----- {{{
Plugin 'tpope/vim-fugitive'
" }}}
" ----- syntastic(expo) ----- {{{
Plugin 'vim-syntastic/syntastic'
  set statusline+=%#warningmsg#
  set statusline+=%{SyntasticStatuslineFlag()}
  set statusline+=%*

  let g:syntastic_always_populate_loc_list = 1
  let g:syntastic_auto_loc_list = 1
  let g:syntastic_check_on_open = 1
  let g:syntastic_check_on_wq = 0

  "let g:syntastic_<filetype>_checkers = ['<checker-name>']

  "HTMLHint.................|syntastic-html-htmlhint|
  let g:syntastic_html_checkers = ['htmlhint']
  "ESLint...................|syntastic-javascript-eslint|
  let g:syntastic_javascript_checkers = ['eslint']
" }}}
" ----- vim-surround(expo) ----- {{{
Plugin 'tpope/vim-surround'
" }}}
" ----- vim-vue ----- {{{
Plugin 'posva/vim-vue'
" }}}
" ----- vim-maximizer ----- {{{
Plugin 'szw/vim-maximizer'

  nnoremap <silent><F6> :MaximizerToggle<CR>
  vnoremap <silent><F6> :MaximizerToggle<CR>gv
  inoremap <silent><F6> <C-o>:MaximizerToggle<CR>
" }}}

filetype on
call vundle#end()
" }}}

" Function {{{
" Remove trailing whitespace when writing a buffer, but not for diff files.
function! RemoveTrailingWhitespace()
    if &ft != "diff"
        let b:curcol = col(".")
        let b:curline = line(".")
        silent! %s/\s\+$//
        silent! %s/\(\s*\n\)\+\%$//
        call cursor(b:curline, b:curcol)
    endif
endfunction
autocmd BufWritePre * call RemoveTrailingWhitespace()
" }}}
```

### 瀏覽器擴展

> gooreplacer, Vimium, Vue.js-devtools, Markdown-Here, m1396ck

75cdn.gson:

```
{
  "rules": {
    "ajax.googleapis.com/ajax/libs": {
      "dstURL": "lib.baomitu.com",
      "kind": "wildcard",
      "enable": true
    }
  }
}
```

### nodejs

> npm, webpack, gulp... (npm install -g package-name)

.npmrc:

```
registry = http://registry.npm.taobao.org/
```

package.json:

```
{
  "name": "exponential",
  "version": "1.5.9",
  "homepage": "",
  "description": "I love front-end, get started.",
  "author": {
    "name": "Thilina Fong",
    "email": "15915940450@139.com",
    "url": "http://fangxuecong.com/"
  },
  "main": "",
  "repository": {
    "type": "git",
    "url": "https://github.com/15915940450/exponential"
  },
  "keywords": [
    "exponential",
    "front-end"
  ],
  "license": "MIT",
  "dependencies": {},
  "devDependencies": {}
}
```

webpack.config.js:

```
const path = require('path');

module.exports = {
  entry: './entry.js',
  devtool: 'inline-source-map',
  devServer: {
    contentBase:'./dist'
  },
  output: {
    filename: 'bundle.js',
    path: path.resolve(__dirname, 'dist')
  }
};
```

gulpfile.js:

```
var gulp=require('gulp');

var traditionalized=require('./fplugin/traditionalized.js');

gulp.task('traditionalized',function(){
  gulp.src('./index.html')
      .pipe(traditionalized())
      .pipe(gulp.dest('dist/zh-HK/'));
});

gulp.task('default',['traditionalized'],function(){
  console.log('okay.');
});
```

README.md, LICENSE

### html

.htmlhintrc:

```
{
  "tagname-lowercase": true,
  "attr-lowercase": true,
  "attr-value-double-quotes": true,
  "doctype-first": true,
  "tag-pair": true,
  "spec-char-escape": true,
  "id-unique": true,
  "src-not-empty": true,
  "title-require": true,
  "tag-self-close": true,
  "attr-no-duplication": true,
  "head-script-disabled": true,
  "alt-require": true,
  "doctype-html5": true,
  "style-disabled": true,
  "inline-style-disabled": true,
  "inline-script-disabled": true,
  "space-tab-mixed-disabled": "space",
  "id-class-ad-disabled": true,
  "attr-unsafe-chars": true
}
```

mini.html:

```
<!DOCTYPE html>
<html>
<head>
<title>fangxuecong</title>
<meta charset="utf-8" />
<meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1" />
<meta name="viewport" content="width=device-width,initial-scale=1,maximum-scale=1,user-scalable=no" />
<meta name="author" content="Thilina Fong" />
<meta name="description" content="" />
</head>
<body>
<div id="container">
15816277995
</div>
</body>
</html>
```

loading.html:

```
<!DOCTYPE html>
<html>
  <head>
    <title>spinner</title>
    <meta charset="utf-8" />
    <style media="screen">
      /*1*/
    .spinner1 {
      margin: 100px auto;
      width: 50px;
      height: 60px;
      text-align: center;
      font-size: 10px;
    }

    .spinner1 > div {
      background-color: #67CF22;
      height: 100%;
      width: 6px;
      display: inline-block;

      -webkit-animation: stretchdelay 1.2s infinite ease-in-out;
      animation: stretchdelay 1.2s infinite ease-in-out;
    }

    .spinner1 .rect2 {
      -webkit-animation-delay: -1.1s;
      animation-delay: -1.1s;
    }

    .spinner1 .rect3 {
      -webkit-animation-delay: -1.0s;
      animation-delay: -1.0s;
    }

    .spinner1 .rect4 {
      -webkit-animation-delay: -0.9s;
      animation-delay: -0.9s;
    }

    .spinner1 .rect5 {
      -webkit-animation-delay: -0.8s;
      animation-delay: -0.8s;
    }

    @-webkit-keyframes stretchdelay {
      0%, 40%, 100% { -webkit-transform: scaleY(0.4) }
      20% { -webkit-transform: scaleY(1.0) }
    }

    @keyframes stretchdelay {
      0%, 40%, 100% {
        transform: scaleY(0.4);
        -webkit-transform: scaleY(0.4);
      }  20% {
        transform: scaleY(1.0);
        -webkit-transform: scaleY(1.0);
      }
    }


    /*2*/
    .spinner2 {
      width: 60px;
      height: 60px;
      background-color: #67CF22;

      margin: 100px auto;
      -webkit-animation: rotateplane 1.2s infinite ease-in-out;
      animation: rotateplane 1.2s infinite ease-in-out;
    }

    @-webkit-keyframes rotateplane {
      0% { -webkit-transform: perspective(120px) }
      50% { -webkit-transform: perspective(120px) rotateY(180deg) }
      100% { -webkit-transform: perspective(120px) rotateY(180deg)  rotateX(180deg) }
    }

    @keyframes rotateplane {
      0% {
        transform: perspective(120px) rotateX(0deg) rotateY(0deg);
        -webkit-transform: perspective(120px) rotateX(0deg) rotateY(0deg)
      } 50% {
        transform: perspective(120px) rotateX(-180.1deg) rotateY(0deg);
        -webkit-transform: perspective(120px) rotateX(-180.1deg) rotateY(0deg)
      } 100% {
        transform: perspective(120px) rotateX(-180deg) rotateY(-179.9deg);
        -webkit-transform: perspective(120px) rotateX(-180deg) rotateY(-179.9deg);
      }
    }


    /*3*/
    .spinner3 {
      width: 60px;
      height: 60px;

      position: relative;
      margin: 100px auto;
    }

    .double-bounce1, .double-bounce2 {
      width: 100%;
      height: 100%;
      border-radius: 50%;
      background-color: #67CF22;
      opacity: 0.6;
      position: absolute;
      top: 0;
      left: 0;

      -webkit-animation: bounce 2.0s infinite ease-in-out;
      animation: bounce 2.0s infinite ease-in-out;
    }

    .double-bounce2 {
      -webkit-animation-delay: -1.0s;
      animation-delay: -1.0s;
    }

    @-webkit-keyframes bounce {
      0%, 100% { -webkit-transform: scale(0.0) }
      50% { -webkit-transform: scale(1.0) }
    }

    @keyframes bounce {
      0%, 100% {
        transform: scale(0.0);
        -webkit-transform: scale(0.0);
      } 50% {
        transform: scale(1.0);
        -webkit-transform: scale(1.0);
      }
    }

    /*4*/
    .spinner4 {
      margin: 100px auto;
      width: 32px;
      height: 32px;
      position: relative;
    }

    .cube1, .cube2 {
      background-color: #67CF22;
      width: 30px;
      height: 30px;
      position: absolute;
      top: 0;
      left: 0;

      -webkit-animation: cubemove 1.8s infinite ease-in-out;
      animation: cubemove 1.8s infinite ease-in-out;
    }

    .cube2 {
      -webkit-animation-delay: -0.9s;
      animation-delay: -0.9s;
    }

    @-webkit-keyframes cubemove {
      25% { -webkit-transform: translateX(42px) rotate(-90deg) scale(0.5) }
      50% { -webkit-transform: translateX(42px) translateY(42px) rotate(-180deg) }
      75% { -webkit-transform: translateX(0px) translateY(42px) rotate(-270deg) scale(0.5) }
      100% { -webkit-transform: rotate(-360deg) }
    }

    @keyframes cubemove {
      25% {
        transform: translateX(42px) rotate(-90deg) scale(0.5);
        -webkit-transform: translateX(42px) rotate(-90deg) scale(0.5);
      } 50% {
        transform: translateX(42px) translateY(42px) rotate(-179deg);
        -webkit-transform: translateX(42px) translateY(42px) rotate(-179deg);
      } 50.1% {
        transform: translateX(42px) translateY(42px) rotate(-180deg);
        -webkit-transform: translateX(42px) translateY(42px) rotate(-180deg);
      } 75% {
        transform: translateX(0px) translateY(42px) rotate(-270deg) scale(0.5);
        -webkit-transform: translateX(0px) translateY(42px) rotate(-270deg) scale(0.5);
      } 100% {
        transform: rotate(-360deg);
        -webkit-transform: rotate(-360deg);
      }
    }
    /*5*/
    .spinner5 {
      margin: 100px auto;
      width: 90px;
      height: 90px;
      position: relative;
      text-align: center;

      -webkit-animation: rotate 2.0s infinite linear;
      animation: rotate 2.0s infinite linear;
    }

    .dot1, .dot2 {
      width: 60%;
      height: 60%;
      display: inline-block;
      position: absolute;
      top: 0;
      background-color: #67CF22;
      border-radius: 100%;

      -webkit-animation: bounce 2.0s infinite ease-in-out;
      animation: bounce 2.0s infinite ease-in-out;
    }

    .dot2 {
      top: auto;
      bottom: 0px;
      -webkit-animation-delay: -1.0s;
      animation-delay: -1.0s;
    }

    @-webkit-keyframes rotate { 100% { -webkit-transform: rotate(360deg) }}
    @keyframes rotate { 100% { transform: rotate(360deg); -webkit-transform: rotate(360deg) }}

    @-webkit-keyframes bounce {
      0%, 100% { -webkit-transform: scale(0.0) }
      50% { -webkit-transform: scale(1.0) }
    }

    @keyframes bounce {
      0%, 100% {
        transform: scale(0.0);
        -webkit-transform: scale(0.0);
      } 50% {
        transform: scale(1.0);
        -webkit-transform: scale(1.0);
      }
    }

    /*6*/
    .spinner6 {
      margin: 100px auto 0;
      width: 150px;
      text-align: center;
    }

    .spinner6 > div {
      width: 30px;
      height: 30px;
      background-color: #67CF22;

      border-radius: 100%;
      display: inline-block;
      -webkit-animation: bouncedelay 1.4s infinite ease-in-out;
      animation: bouncedelay 1.4s infinite ease-in-out;
      /* Prevent first frame from flickering when animation starts */
      -webkit-animation-fill-mode: both;
      animation-fill-mode: both;
    }

    .spinner6 .bounce1 {
      -webkit-animation-delay: -0.32s;
      animation-delay: -0.32s;
    }

    .spinner6 .bounce2 {
      -webkit-animation-delay: -0.16s;
      animation-delay: -0.16s;
    }

    @-webkit-keyframes bouncedelay {
      0%, 80%, 100% { -webkit-transform: scale(0.0) }
      40% { -webkit-transform: scale(1.0) }
    }

    @keyframes bouncedelay {
      0%, 80%, 100% {
        transform: scale(0.0);
        -webkit-transform: scale(0.0);
      } 40% {
        transform: scale(1.0);
        -webkit-transform: scale(1.0);
      }
    }
    /*7*/
    .spinner7 {
      width: 40px;
      height: 40px;
      margin: 100px auto;
      background-color: #333;

      border-radius: 100%;
      -webkit-animation: scaleout 1.0s infinite ease-in-out;
      animation: scaleout 1.0s infinite ease-in-out;
    }

    @-webkit-keyframes scaleout {
      0% { -webkit-transform: scale(0.0) }
      100% {
        -webkit-transform: scale(1.0);
        opacity: 0;
      }
    }

    @keyframes scaleout {
      0% {
        transform: scale(0.0);
        -webkit-transform: scale(0.0);
      } 100% {
        transform: scale(1.0);
        -webkit-transform: scale(1.0);
        opacity: 0;
      }
    }

    /*8*/
    .spinner8{
      margin: 100px auto;
      width: 40px;
      height: 40px;
      position: relative;
      /*background: red;*/
    }
    .container1 > div,.container2 > div,.container3 > div{
      width: 12px;
      height: 12px;
      background: #333;

      border-radius: 100%;
      position: absolute;
      -webkit-animation:bouncedelay 1.2s infinite ease-in-out;
      animation:bouncedelay 1.2s infinite ease-in-out;
      -webkit-animation-fill-mode:both;
      animation-fill-mode:both;
    }
    .spinner8 .spinner-container{
      position: absolute;
      width: 100%;
      height: 100%;
    }
    .container2{
      -webkit-transform:rotateZ(45deg);
      transform:rotateZ(45deg);
    }
    .container3{
      -webkit-transform:rotateZ(90deg);
      transform:rotateZ(90deg);
    }
    .circle1{
      top:0;
      left: 0;
    }
    .circle2{
      top:0;
      right: 0;
    }
    .circle3{
      bottom:0;
      right: 0;
    }
    .circle4{
      bottom:0;
      left: 0;
    }
  .container2 .circle1 {
    -webkit-animation-delay: -1.1s;
    animation-delay: -1.1s;
  }

  .container3 .circle1 {
    -webkit-animation-delay: -1.0s;
    animation-delay: -1.0s;
  }

  .container1 .circle2 {
    -webkit-animation-delay: -0.9s;
    animation-delay: -0.9s;
  }

  .container2 .circle2 {
    -webkit-animation-delay: -0.8s;
    animation-delay: -0.8s;
  }

  .container3 .circle2 {
    -webkit-animation-delay: -0.7s;
    animation-delay: -0.7s;
  }

  .container1 .circle3 {
    -webkit-animation-delay: -0.6s;
    animation-delay: -0.6s;
  }

  .container2 .circle3 {
    -webkit-animation-delay: -0.5s;
    animation-delay: -0.5s;
  }

  .container3 .circle3 {
    -webkit-animation-delay: -0.4s;
    animation-delay: -0.4s;
  }

  .container1 .circle4 {
    -webkit-animation-delay: -0.3s;
    animation-delay: -0.3s;
  }

  .container2 .circle4 {
    -webkit-animation-delay: -0.2s;
    animation-delay: -0.2s;
  }

  .container3 .circle4 {
    -webkit-animation-delay: -0.1s;
    animation-delay: -0.1s;
  }

  @-webkit-keyframes bouncedelay{
    0%,80%,100%{
      -webkit-transform:scale(0,0);
    }
    40%{
      -webkit-transform:scale(1,1);
    }
  }
  @keyframes bouncedelay {
    0%, 80%, 100% {
      transform: scale(0,0);
    } 40% {
      transform: scale(1,1);
    }
  }
    </style>
  </head>
  <body>
    <!-- 1 -->
    <div class="spinner1">
      <div class="rect1"></div>
      <div class="rect2"></div>
      <div class="rect3"></div>
      <div class="rect4"></div>
      <div class="rect5"></div>
    </div>




    <!-- 2 -->
    <div class="spinner2"></div>


    <!-- 3 -->
    <div class="spinner3">
      <div class="double-bounce1"></div>
      <div class="double-bounce2"></div>
    </div>


    <!-- 4 -->
    <div class="spinner4">
      <div class="cube1"></div>
      <div class="cube2"></div>
    </div>


    <!-- 5 -->
    <div class="spinner5">
      <div class="dot1"></div>
      <div class="dot2"></div>
    </div>


    <!-- 6 -->
    <div class="spinner6">
      <div class="bounce1"></div>
      <div class="bounce2"></div>
      <div class="bounce3"></div>
    </div>


    <!-- 7 -->
    <div class="spinner7"></div>


    <!-- 8 -->
    <div class="spinner8">
      <div class="spinner-container container1">
        <div class="circle1"></div>
        <div class="circle2"></div>
        <div class="circle3"></div>
        <div class="circle4"></div>
      </div>
      <div class="spinner-container container2">
        <div class="circle1"></div>
        <div class="circle2"></div>
        <div class="circle3"></div>
        <div class="circle4"></div>
      </div>
      <div class="spinner-container container3">
        <div class="circle1"></div>
        <div class="circle2"></div>
        <div class="circle3"></div>
        <div class="circle4"></div>
      </div>
    </div>
  </body>
</html>
```

### css

reset.css:

```
@charset 'utf-8';

* {
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
}

html,body {
  width: 100%;
  height: 100%;
  background-color: #fff;
  -webkit-font-smoothing: antialiased;
}

article,aside,body,details,figcaption,figure,footer,form,h1,h2,h3,h4,h5,h6,header,hgroup,input,li,menu,nav,ol,p,section,select,textarea,ul {
  font-family: '微软雅黑',Ubuntu,Arial,'libra sans',sans-serif;
  /*font-family:"Microsoft JhengHei","微軟正黑體",PMingLiU,Arial,sans-serif;*/
  font-size: 12px;
  margin: 0;
  padding: 0;
}

p {
  line-height: 1.9em;
}

textarea {
  overflow: auto;
  resize: none;
}

li {
  list-style: none;
}

img {
  border: none;
  max-width: 100%;
}

article,aside,details,figcaption,figure,footer,header,hgroup,menu,nav,section {
  display: block;
}

a {
  color:#efe33f;
  transition: all .2s ease-out;
  text-decoration: none;
}

a:focus,input,select,textarea {
  outline: 0;
}

.clearfix:after {
  display: block;
  visibility: hidden;
  clear: both;
  height: 0;
  content: 'Thilina Fong';
}

.clearfix {
  zoom: 1;
}

.ellip {
  max-width: 300px;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}
```

### js

> jquery, bootstrap, vue, react, 算法

.eslintrc.js:

```
module.exports = {
  "env": {
    "browser": true,
    "jquery":true,
    "es6": true
  },
  "globals":{
    "Vue":true
  },
  "extends": "eslint:recommended",
  "rules": {
    "indent": ["error", 2],
    "semi": ["error", "always"],
    "comma-dangle": ["error", "never"],
    "eqeqeq": ["error", "always"],
    "quotes": ["error", "single"]
  }
};
```

.eslintignore:

```
/node_modules
```

### git

.gitconfig:

```
[user]
	email = 15915940450@139.com
	name = 15915940450
[alias]
	ss = status
```

.gitignore

### media

> 1520.mp3, EarthDay_2017_FF_768_HD_ZH-CN1190113803.jpg, HongKong_Sunset_FF_768_HD_ZH-CN950412909.jpg, ShanwangpingKarst_EN-AU5360258756_1920x1080.jpg, Microsoft JhengHei, PingFang.ttf, mysql.txt, #efe33f


###### $
