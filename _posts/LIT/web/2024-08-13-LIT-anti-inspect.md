---
title: Anti-Inspect
date : 2024-08-13 10:00:00 +0530
categories: [litctf]
tags: [litctf, ctf]
description: Anti-Inspect
---

## Description

can you find the answer? WARNING: do not open the link your computer will not enjoy it much. URL: http://litctf.org:31779/

Hint: If your flag does not work, think about how to style the output of console.log

## Solution

Straightforward question. I used curl to response from the website.

```bash
curl http://litctf.org:31779/
```

![antiresp](/assets/posts/LITCTF/antiresp.png)

The response had the const flag on the js code which was running infinitely... that's why the warning was given. ( and the computer was like *why am I here? just to suffer?* )

```js
const flag = "LITCTF{your_%cfOund_teh_fI@g_94932}";
while (true)
console.log(
    flag,
    "background-color: darkblue; color: white; font-style: italic; border: 5px solid hotpink; font-size: 2em;"
);
```

> I modified the script to run without the infinite loop.
{: .prompt-warning}

Run the original js code with console.log() to get the flag. ( or just remove the %c )

![anti1](/assets/posts/LITCTF/anti1.png)

> Flag : LITCTF{your_fOund_teh_fI@g_94932}

---

[back to index](/posts/LIT-Index/)