---
title: Traversed
date : 2024-08-13 10:00:00 +0530
categories: [litctf]
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

![traversed1](/assets/posts/LITCTF/traversed1.png)

The flag was on `../flag.txt` path and we could read it by visiting the following url:

```bash
http://litctf.org:31778/..%2Fflag.txt
```

![traversed2](/assets/posts/LITCTF/traversed2.png)

> `Flag: LITCTF{backtr@ked_230fim0}`

## Why URL Encode ?

I have seen some questions on discord regarding why we are URL encoding and why can't we just visit `../flag.txt` instead.

Well, most web servers out there filter out the `../` sequence but forget to filter out the url-encoded version so encoding `../` using a tool like CyberChef, it becomes `%2E%2E%2F` which lets us bypass that filter easily.

Also, The WebServer was not filtering it out this time, but the browser itself. You can verify this by using curl with `--path-as-is` flag, which tells curl to not strip out the `../` sequence.

```bash
curl --path-as-is http://litctf.org:31778/../flag.txt 
```

---

[back to index](https://p-pratik.github.io/posts/LIT-Index/)
