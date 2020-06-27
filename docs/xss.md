# XSS

For the advanced stuff, you're going to want to look into filter evasion techniques.

Know what encodings work natively in what spaces (text space, attribute space, URI space, script space). HTML encoded entities work in attribute space, for example.

Know what encodings to try to get the server to decode. Double Nibble Hex encoding, for example.

Have a solid understanding of SOP, CSP, and CORS.

Learn the sources and sinks (ins and outs) of DOM XSS.

XSS is nothing but HTML and javascript. If you don't know how those work, your potential will be very limited.

## Practice

* [The unescape() room](https://unescape-room.jobertabma.nl/) - Filter evasion practice
* [alf.nu's XSS Game](https://alf.nu/alert1) - Filter evasion practice
* [prompt.ml's XSS Game](http://prompt.ml/0)  - Filter evasion practice
* [pwnfunction's XSS Game](https://xss.pwnfunction.com/) - Filter evasion practice
* [Google Firing Range](https://public-firing-range.appspot.com/) - Real world scenarios.

## Cheatsheet

[Portswigger Cheatsheet](https://portswigger.net/web-security/cross-site-scripting/cheat-sheet)

## Learn

* [Intigriti](https://blog.intigriti.com/hackademy/cross-site-scripting-xss/)
* [Portswigger Labs](https://portswigger.net/web-security/cross-site-scripting)
* [Same Origin Policy](https://developer.mozilla.org/en-US/docs/Web/Security/Same-origin_policy)
* [Javascript Escapes](https://mathiasbynens.be/notes/javascript-escapes)

## Utilities

* [XSS Hunter](https://xsshunter.com/app) - Good for Blind XSS
* [Findom-XSS](https://github.com/dwisiswant0/findom-xss)

## Prevent XSS

[Is replacing special characters enough?](https://www.reddit.com/r/xss/comments/gqe7e3/is_this_enough_to_prevent_an_xss_attack/)

