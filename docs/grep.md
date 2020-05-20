# Grep

## Lines that begin with a slash and end with `.js`:

```
find . -type f | html-tool attribs src | grep '\.js$' | egrep '^ */'
```