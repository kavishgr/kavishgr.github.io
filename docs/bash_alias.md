# Bash Alias

## Vim

### Sort by size

```
alias vimsize='find . -type f -exec ls -l {} \; | vim -'
```

Then run:

```
:%! sort -k5,5 -n
```

## Grep

### New version of grep:

```
alias egrep='/usr/local/opt/grep/bin/gegrep'
alias fgrep='/usr/local/opt/grep/bin/gfgrep'
alias grep='/usr/local/opt/grep/bin/ggrep --color=always'
```

### Find dotdot slash:

```
alias gdot='grep -Hrn "\.\./" * '
```

