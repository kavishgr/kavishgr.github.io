# Regex For Burp Suite search

## Find JWT token

```
\b(ey[a-z0-9+\-\._]+[=|==|\s|;|"])
```

## Email ID

```
\b[\w\.\!\$\+\-\/\=\?\_\~]+@[\w]+\.[\w]+\b
```

## Subdomains

```
\b[\w\.\-\\\/%\*]*(\.twitter)\.(com)\b 
```

## Find IP addresses

```
\b\d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3}\b
```

## Internal IP address

```
\b(192|10|172)\.(\d\d\d|\d\d|\d)\.(\d\d\d|\d\d|\d)\.(\d\d\d|\d\d|\d)\b
```
