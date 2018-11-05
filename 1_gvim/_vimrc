" ------------------------------
" Name: _vimrc
" Author:Thilina
" Email: 15915940450@139.com
" ------------------------------

let mapleader=","


" Startup {{{
  filetype indent plugin on
  " 啓動時窗口最大化
  autocmd GUIEnter * simalt ~x
  augroup vimrcEx
    au!
    autocmd FileType text setlocal textwidth=78
  augroup END
  augroup ft_vim
    au!
    " vim 文件折叠方式为 marker
    autocmd FileType vim setlocal foldmethod=marker
    " 打开文件总是定位到上次编辑的位置
    autocmd BufReadPost * if line("'\"") > 1 && line("'\"") <= line("$") | exe "normal! g`\"" | endif
  augroup END
" }}}

" General(set) {{{
  set nocompatible
  set nobackup
  set noswapfile
  set history=969
  set autochdir
  set whichwrap=b,s,<,>,[,]
  set nobomb
  set backspace=indent,eol,start whichwrap+=<,>,[,]
  set winaltkeys=no
  set autoindent
  set smartindent
  set tabstop=2
  set shiftwidth=2
  set softtabstop=2
  set expandtab
  set foldmethod=indent
  set fileencodings=utf-8,gbk2312,gbk,gb18030,cp936
  set encoding=utf-8
  set langmenu=zh_CN
  let $LANG = 'en_US.UTF-8'
  source $VIMRUNTIME/delmenu.vim
  source $VIMRUNTIME/menu.vim
  set cursorline
  set hlsearch
  set number
  "set lines=35 columns=135
  set splitbelow
  set splitright
  set guioptions-=T
  set guioptions-=m
  set guioptions-=L
  set guioptions-=r
  set guioptions-=b
  set guioptions-=e
  " set nolist
  "set listchars=trail:·,extends:>,precedes:<
  set laststatus=2
  set statusline +=%3*\ %{''.(&fenc!=''?&fenc:&enc).''}
  set statusline +=%4*\ %<%F%*
  colorscheme snow
  set background=light
  "desert light dark
  set guifont=Source\ Code\ Variable:h13:cANSI
" }}}

" copy {{{
  syntax on
  " Vim 的默认寄存器和系统剪贴板共享
  set clipboard+=unnamed
  "copy and paste
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
" }}}

" Plugin {{{
  filetype off
  set rtp+=$VIM/vimfiles/bundle/Vundle.vim
  call vundle#begin('$VIM/vimfiles/bundle')
  "  1.vandle,2.vim-airline,3.nerdtree,4.ctrlp,5.nerdcommenter,6.emmet,7.ultisnips,8.syntastic,9.bufexplorer,10.maximizer,11.easygrep,12.vue

  " ----- Vundle ----- {{{
  Plugin 'VundleVim/Vundle.vim'
  " }}}

  " ----- vim-airline ----- {{{
  Plugin 'vim-airline/vim-airline'
  " }}}
  " ----- nerdtree ----- {{{
  Plugin 'scrooloose/nerdtree'
   let NERDTreeIgnore=['node_modules','\.git$']
   let NERDTreeBookmarksFile = $VIM . '/NERDTreeBookmarks'
   let NERDTreeMinimalUI = 1
   let NERDTreeBookmarksSort = 1
   let NERDTreeShowLineNumbers = 0
   let NERDTreeShowBookmarks = 1
   let g:NERDTreeWinPos = 'right'
   let g:NERDTreeDirArrowExpandable = '+'
   let g:NERDTreeDirArrowCollapsible = '-'
   "
   "if exists('g:NERDTreeWinPos')
       "autocmd vimenter * NERDTree $HOME\gvimnerdtree
   "endif
  " }}}
  " ----- ctrlp ----- {{{
  Plugin 'kien/ctrlp.vim'
   let g:ctrlp_match_window = 'bottom,order:btt,min:1,max:10,results:10'
   set wildignore+=*\\node_modules\\*,*\\.git\\*,*\\es\\*,*\\eb_src\\*,*\\batterystation\\*,*\\ccbike\\*,*\\TEST\\*
   " Insert
  " }}}
  " ----- nerdcommenter ----- {{{
  Plugin 'scrooloose/nerdcommenter'
  " }}}
  " ----- emmet-vim ----- {{{
  Plugin 'mattn/emmet-vim'
  " }}}
  " ----- ultisnips ----- {{{
  Plugin 'SirVer/ultisnips'
    let g:UltiSnipsSnippetDirectories=[$HOME.'/UltiSnips']
    " Trigger configuration. Do not use <tab> if you use https://github.com/Valloric/YouCompleteMe.
    let g:UltiSnipsExpandTrigger="<tab>"
    let g:UltiSnipsJumpForwardTrigger="<c-b>"
    let g:UltiSnipsJumpBackwardTrigger="<c-z>"
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
  " ----- bufexplorer.zip ----- {{{
  Plugin 'vim-scripts/bufexplorer.zip'
  " }}}
  " ----- vim-maximizer ----- {{{
  Plugin 'szw/vim-maximizer'
  " }}}
  " ----- vim-easygrep ----- {{{
  Plugin 'dkprice/vim-easygrep'
    let g:EasyGrepRecursive=1
    let g:EasyGrepIgnoreCase=1
    let g:EasyGrepHidden=1
  " }}}
  " ----- vim-vue ----- {{{
  Plugin 'posva/vim-vue'
    "firstly install -g eslint eslint-plugin-vue babel-eslint
    autocmd FileType vue syntax sync fromstart
    autocmd BufRead,BufNewFile *.vue setlocal filetype=vue.javascript
  " }}}

  filetype on
  call vundle#end()
" }}}

" Function {{{
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

  let g:ft = ''
  function! NERDCommenter_before()
    if &ft == 'vue'
      let g:ft = 'vue'
      let stack = synstack(line('.'), col('.'))
      if len(stack) > 0
        let syn = synIDattr((stack)[0], 'name')
        if len(syn) > 0
          exe 'setf ' . substitute(tolower(syn), '^vue_', '', '')
        endif
      endif
    endif
  endfunction
  function! NERDCommenter_after()
    if g:ft == 'vue'
      setf vue
      let g:ft = ''
    endif
  endfunction
" }}}

" keymap快捷鍵 {{{
  "leader
  nmap <leader>s :source $MYVIMRC<cr>
  nmap <leader>e :e $MYVIMRC<cr>
  nmap <leader>tn :tabnew<cr>
  nmap <leader>tc :tabclose<cr>
  nmap <leader>r :%s/from/to/g
  nmap <leader>1 :only<cr>
  nmap <leader>2 :split<cr>
  nmap <leader>3 :vsplit<cr>
  nmap <leader>nm :NoMatchParen<cr>
  nmap <leader>dm :DoMatchParen<cr>
  nnoremap <leader><cr> :noh<cr>
  nnoremap <leader>w :set wrap!<cr>
  nmap <silent> <leader>x :!start explorer %:p:h<CR>
  nmap <silent> <leader>cmd :!start cmd /k cd %:p:h<cr>
  nmap <leader>fp :let @*=substitute(expand("%:p"), "/", "\\", "g")<CR>
  "==<leader>+b then e
  "==<leader>+b then s
  "==<leader>+b then v
  "==<leader>+v then o
  "==<leader>+v then v
  "==<leader>+v then r

  "ctrl
  inoremap <C-u> <esc>mzgUiw`za
  nmap <C-n> :NERDTreeToggle <cr>

  "alt
  nmap <M-a> <C-W>k
  nmap <M-z> <C-W>j
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

  "and...F
  nnoremap vv ^vg_
  nnoremap <F2> :setlocal number!<cr>
  nmap <F3> a<C-R>=strftime("%Y-%m-%d %a %I:%M %p")<CR><Esc>
  nnoremap <silent><F6> :MaximizerToggle<CR>
  vnoremap <silent><F6> :MaximizerToggle<CR>gv
  inoremap <silent><F6> <C-o>:MaximizerToggle<CR>
" }}}

"1.startup directory(https://stackoverflow.com/questions/1180955/vim-change-start-up-directory)
:cd $HOME\ili\AppServ\www

" $
