# Vim Editor

## Vimrc:

```
let mapleader = "\<space>"

syntax on

let g:pymode_python = 'python3'


" sort the buffer for unique lines
nmap <Leader>s :%!sort -u --version-sort<CR>

" Base64 decode word under cursor
nmap <Leader>b :!echo <C-R><C-W> \| base64 -D<CR>

set hlsearch
```

## Open file under cursor in a new tab:

```
# Press CTRL+'w' then 'f'
<C-W>f
```

## Execute shell command on the data that is in the vim buffer or file

```
:%! sort -u
```

## Run shell commands and put the output in the vim buffer or file:

Hit `!` twice, and you'll get a vim prompt in the bottom left corner that looks like this:

```
:.!
```

Then just type your command and press enter:

```
:.!whoami
```

## **In `fish` shell, make a universal variable**(or else vim won't work properly):

```
set -U EDITOR vim
```

## **Pipe data into a vim buffer:**

```
grep -Hnri * | vim -
```

## Sort the fifth column:

```
# find . -type f -exec ls -l {} \;
# to look at content size

:%! sort -k5,5 -n
```
