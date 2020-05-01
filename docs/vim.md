# Vim Editor

## Execute shell command

```
:%! sort -u
```

## **In `fish` shell, make a universal variable**(or else vim won't work properly):

```
set -U EDITOR vim
```

## **Pipe data into a vim buffer:**

```
grep -Hnri * | vim -
```

## **Parse lines of data to `xargs`**(**-d** on linux):

```
:%! xargs -n1 -I{} sh -c 'echo {} | base64 -D'
```
