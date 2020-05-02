# Vim Editor

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
