---
title: Anti-Inspect
date : 2024-08-13 10:00:00 +0530
categories: [litctf , ctf]
tags: [litctf, ctf]
description: Anti-Inspect
---

## Description

can you find the answer? WARNING: do not open the link your computer will not enjoy it much. URL: http://litctf.org:31779/

Hint: If your flag does not work, think about how to style the output of console.log

## Solution

Straightforward question. I used curl to get the flag.

```bash
curl http://litctf.org:31779/
```

the response had the flag on the js code which was running infinitely... that's why the warning was given.

```js
const flag = "LITCTF{your_%cfOund_teh_fI@g_94932}";
```

use url-decode or console.log() to get the flag. ( or just remove the %c )

> Flag : LITCTF{your_fOund_teh_fI@g_94932}

---

[back to index](/posts/LIT-Index/)