# xargs

## Decode base64 inside vim 

**Parse lines of data to `xargs`**(**-d** on linux):

```
:%! xargs -n1 -I{} sh -c 'echo {} | base64 -D'
```

> Note: Omit `sh -c` if you're using bash
