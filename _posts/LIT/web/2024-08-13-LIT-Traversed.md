---
title: Traversed
date : 2024-08-13 10:00:00 +0530
categories: [litctf , ctf]
tags: [litctf, ctf]
description: Traversed
---

## Description

I made this website! you can't see anything else though... right?? URL: http://litctf.org:31778/

## Initial Analysis

On initial inspection of the webpage.. there was nothing interesting as said by the description. Nothing hidden in source code.
No robots.txt file as well.

## Exploit

The webpage was vulnerable to directory traversal. We could travel to `/etc/passwd` and read the contents of the files. We just had to url encode the rest part of the path.

`http://litctf.org:31778/..%2F..%2F..%2F..%2Fetc%2Fpasswd`

The flag was on `../flag.txt` path and we could read it by visiting the following url:

```bash
http://litctf.org:31778/..%2Fflag.txt
```

> `Flag: LITCTF{backtr@ked_230fim0}`

---

[back to index](/posts/LIT-Index/)