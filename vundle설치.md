# 프로그래밍을 위한 vim 세팅
## 복사/붙여넣기
- virtualbox 5.1.28에서 macos용이 게스트 확장이 안되고 있습니다. 맥사용자는 불편하더라도 당분간 아래 방법을 써야 합니다.
- centOS에서 브라우저 내용을 복사해서 터미널로 붙여 넣을 때는 ``Shift+Ctrl+v``
- 또는 Alt + 마우스 왼쪽클릭 하면 팝업메뉴가 나옵니다. 붙여넣기 선택
- 또는 터미널 메뉴의 편집 > 붙여넣기를 선택합니다.
## git 설치

```sh
$sudo yum install git
```
- sudo 가붙은 명령은 관리자 비밀번호 입력해야 합니다.
## gvim설치
```sh
$sudo yum install gvim
```
- gvim을 설치하는 이유는 클립보드로 복사, 붙여넣기를 해야 하기 때문입니다.
- vim에서 클립보드 내용을 붙여 넣으려면 "+P
- vim의 내용을 클립보드로 복사 하려면 "+Y

## .bash_profile 수정
```sh
$cd ~
$vi .bash_profile
```
```vim
" 마지막에 줄에 아래문장을 붙여 넣습니다.
alias vi="gvim -v"

:wq
```
```sh
$source .bash_profile
# 이제부터 vim에 브라우저 소스를 복사해서 붙여 넣을 때는 "+P
```

## .vim 디렉토리 생성 및 vundle clone
```sh
$cd ~
$mkdir -p .vim/bundle
$git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim
```
## .vimrc 생성

```sh
$vi
```
```vim
:!cp -i $VIMRUNTIME/vimrc_example.vim ~/.vimrc
```
## vundle 설치
``.vimrc`` 파일을 오픈합니다.
```vim
:e ~/.vimrc
```
``.vimrc`` 파일이 열리면 아래 내용을 복사해서 맨 위에 붙여 넣습니다.  
vim에서 붙여넣기 할 때는 "+P 를 차례로 입력합니다.  
클립보드 붙여넣기 명령입니다.  
shift+ctrl+v는 문자가 잘립니다.  
```vim

"=================================================
" Vundle
" https://github.com/gmarik/vundle
"=================================================
set nocompatible
filetype off
set rtp+=~/.vim/bundle/Vundle.vim
call vundle#begin()

Plugin 'VundleVim/Vundle.vim'
Plugin 'tpope/vim-fugitive'

" All of your Plugins must be added before the following line
Plugin 'altercation/vim-colors-solarized'  " solarized 테마
Plugin 'scrooloose/nerdtree' " 파일/폴더관리
Plugin 'terryma/vim-multiple-cursors'  " 멀티커서 
Plugin 'kien/ctrlp.vim'
"==============    SnipMate  =====================  # 코드단축
Plugin 'MarcWeber/vim-addon-mw-utils'
Plugin 'tomtom/tlib_vim'
Plugin 'garbas/vim-snipmate'
Plugin 'honza/vim-snippets'
"=================================================

Plugin 'davidhalter/jedi-vim'	"파이썬 ide
Plugin 'vim-airline/vim-airline'	"vim 꾸미기
Plugin 'vim-airline/vim-airline-themes'	"vim 꾸미기 테마
Plugin 'tpope/vim-surround'		"문자 감싸기
Plugin 'suan/vim-instant-markdown'  " 마크다운 미리보기
Plugin 'VisIncr'  " 자동증감01234
Plugin 'klen/python-mode' " ide
"==============  마크다운   ======================
Plugin 'godlygeek/tabular' 
Plugin 'plasticboy/vim-markdown'
Plugin 'mzlogin/vim-markdown-toc'
"=================================================
"Plugin 'joshdick/onedark.vim'
"Plugin 'vim-pandoc/vim-pandoc'
"Plugin 'vim-pandoc/vim-pandoc-syntax' 
"Plugin 'junegunn/goyo.vim'
"=====================================
"Plugin 'dbext.vim' " dbms관리
"=====================================
"
call vundle#end()
filetype plugin indent on
" To ignore plugin indent changes, instead use:
" filetype plugin on
"

" Brief help
" :PluginList       - 설치된 플러그인 목록 보기
" :PluginInstall    - 플러그인설치; append `!` to update or just
" :PluginUpdate		- 플러그인 업데이트
" :PluginSearch foo - 플러그인 검색; append `!` to refresh local cache
" :PluginClean      - 사용하지 않은 플러그인 삭제; append `!` to auto-approve removal
" .vimrc에 플러그인을 추가했으면
":w 저장 
":source %  ".vimrc 다시 로드
":PluginInstall				"플러그인 설치
" http://vimawesome.com		"플러그인 조회 사이트
" http://vimcast.org		"강좌
" see :h vundle				"for more details or wiki for FAQ
" Put your non-Plugin stuff after this line

" Use Vim settings, rather than Vi settings (much better!).
" This must be first, because it changes other options as a side effect.
"============================================================="
```
아래내용을 맨 아래 붙여 넣습니다.

```vim
set nu		" 줄번호를 보여줌

" 탭설정 하기
set ts=4	" 탭의 4의 공백 폭을 
"set sts=4	 "탭을 눌렀을 때 스페이스(ascii-0x20) 4개가 삽입되도록 합니다.
"set sw=4	 "'<'나 '>'키로 줄 전체를 밀거나 당길 때 참조되는 폭입니다.
"set et		 "set expandtab 탭을 공백으로 바꿈
"retab		 "et를 다시 적용
set bs+=indent,eol,start	"들여쓰기된 스페이스를 지울 때 백스페이스를 여러번 누르지 않도록 하기 위해 sts 설정값만큼 백스페이스가 적용됩니다.

"==========    instant_markdown     ======================
"마크다운 문서를 작성시 브라우저로 미리 보기
"let g:instant_markdown_slow = 1
let g:instant_markdown_autostart = 1 "자동실행 방지 0

"========     vim_markdown    ============================
" 마크다운 편집을 도와줌
let g:vim_markdown_folding_disabled = 1
let g:vim_markdown_toc_autofit = 1
let g:vim_markdown_math = 1
let g:vim_markdown_frontmatter = 1
let g:vim_markdown_toml_frontmatter = 1
let g:vim_markdown_json_frontmatter = 1

"===================================================================
" 컴파일 , 키맵
" c언어,pytyon
" compile and Run
" java는 eclipse에서 컴파일
au FileType c map <F5> :w<Enter>:!gcc % -o %<.o<Enter>:!./%<.o<Enter>
au FileType python map <F5> :w<Enter>:!python %<Enter>
au FileType rube map <F5> :w<Enter>:!rube %<Enter>


"외부에서 파일변경시 자동으로 읽어들임
"이클립스, xcode 사용시 
set autoread< 

"클립보드사용
set clipboard=unnamed

"===============   airline    ===============
" 화이트 스페이스 체크 안함. 
let g:airline#extensions#whitespace#enabled = 0		
let g:airline#extensions#tabline#enabled = 1 
" vim-airline 버퍼 목록 켜기
" let g:airline#extensions#tabline#fnamemod = ':t' 
" vim-airline 버퍼 목록 파일명만 출력
" let g:airline#extensions#tabline#buffer_nr_show = 1 
" buffer number를 보여준다
let g:airline#extensions#tabline#buffer_nr_format = '%s:' 
" buffer number format
"let g:airline_powerline_fonts = 1
let g:airline_theme='solarized'
let g:airline_solarized_bg='dark'
set laststatus=2
colorscheme solarized
let g:solarized_termcolors=256
"===============   airline    =================

let mapleader=","  " 리더키를 , 로 변경 주석처리하면 원상태
nnoremap <Leader>ex !!$SHELL<CR> ",ex로 외부명령을 실행
"nnoremap <Leader>rc :tabnew $MYVIMRC<CR> "새탭으로 오픈
"nnoremap <Leader>rc :rightbelow vnew $MYVIMRC<CR>" 오른쪽에 오픈
nnoremap <Leader>rc :e $MYVIMRC<CR> ",rc로 .vimrc파일 오픈
"nnoremap <Leader>n :NERDTreeToggle<CR>
"nnoremap <C-F> :NERDTreeFind<CR>

"================  약어  (abbreviations)  ======================
" snippet은 tab을 눌러야하고 약어는 자동으보 바뀜
" snippet은 자동완성, 
"ab la Los Angeles(L.A) 이렇게 사용해야함.
"한글 약어는 안되는 단어도 있음.
ab 컨브 Ctrl+v
ab 컨씨 Ctrl+c
ab 컨엠 Ctrl+m
ab 이시 Ctrl+[ or \<Esc\>
ab 노모 Normal mode
ab 커모 Command mode
ab 비모 Visual mode
ab 인모 Insert mode
ab 로렘 정당은 법률이 정하는 바에 의하여 국가의 보호를 받으며, 국가는 법률이 정하는 바에 의하여 정당운영에 필요한 자금을 보조할 수 있다. 대통령의 임기연장 또는 중임변경을 위한 헌법개정은 그 헌법개정 제안 당시의 대통령에 대하여는 효력이 없다. 위원은 탄핵 또는 금고 이상의 형의 선고에 의하지 아니하고는 파면되지 아니한다. 제3항의 승인을 얻지 못한 때에는 그 처분 또는 명령은 그때부터 효력을 상실한다. 이 경우 그 명령에 의하여 개정 또는 폐지되었던 법률은 그 명령이 승인을 얻지 못한 때부터 당연히 효력을 회복한다.
ab 배요일 "월", "화", "수", "목", "금", "토", "일"
ab 배코이름 "유재석", "박명수", "강호동", "신동엽", "박미선"
ab 배색깔 "빨강", "주황", "노랑", "초록", "파랑", "남", "보라"
ab 브이아이 VI
ab 빔 VIM

```
저장하고 .vimrc를 다시 읽어들입니다.
```vim
:w
:so %
```
플러그인을 설치합니다.
```vim
:PluginInstall
```
vim을 종료했다 다시 시작합니다.

## 터미널 Solarized Theme 적용
```sh
$cd ~
$mkdir -p Projectes/Solarized
$cd Projectes/Solarized
$git clone https://github.com/sigurdga/gnome-terminal-colors-solarized.git
$cd gnome-terminal-colors-solarized
$./install.sh

색상선택을 dark로 선택
저장할 프로파일을 물으면 solarized 입력
오류가 날 경우 터미널 메뉴에서 
파일>새프로파일 선택후 프로파일명에 solarized 입력후 닫기 후 재실행후 색상과 프로파일명 입력
터미널 메뉴에서 프로파일 변경
편집>프로파일 기본설정에서 solarized를 선택
화면이 짙은 녹색으로 나오면 성공

```
