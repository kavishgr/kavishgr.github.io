# sed

## Remove ANSI codes/colors

* On Linux:

```
./somescript | sed -r "s/\x1B\[([0-9]{1,3}(;[0-9]{1,2})?)?[mGK]//g"
```

* On OSX or BSD(in some cases use `-E`):

```
./somescript | sed $'s,\x1b\\[[0-9;]*[a-zA-Z],,g'
```