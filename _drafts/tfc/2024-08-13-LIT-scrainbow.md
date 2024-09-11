---
title: Scrainbow
date : 2024-08-13 10:00:00 +0530
categories: [litctf]
tags: [litctf, ctf]
description: scrainbow
---

## Description

Oh no! someone dropped my perfect gradient and it shattered into 10000 pieces! I can't figure out how to put it back together anymore, it never looks quite right. Can you help me fix it? URL: http://litctf.org:31780/

## Task at hand

Our task was the fix the gradient on the webpage. The webpage had a 100x100 grid scattered with multiple colors and we had to arrange the colors in this form:-

```plaintext
Can you rearrange the grid to be a rainbow gradient from top left to bottom right (red -> rainbow -> red)?
Click on a square to select it, then click on another square to swap them.
```

![scrainbow](/assets/posts/LITCTF/scrainbow1.png)

## Analysis

On initial inspection of the webpage, we could see a 100x100 grid with multiple colors. The colors were scattered and we had to arrange them in a rainbow gradient from top left to bottom right.

What we could do was `swap` 2 pieces of the grid by clicking on them.

In the source of the webpage, we could see the interesting part of the code.

```javascript
// the data used to generate the grid
const data = await fetch("/data").then((r) => r.json());

// move history was being recorded 
const moveHistory = [];
const move = (i, j) => {
    if (selected === -1) {
        selected = j * gridSize + i;
    } else {
        const temp = data[selected];
        data[selected] = data[j * gridSize + i];
        data[j * gridSize + i] = temp;
        moveHistory.push([selected, j * gridSize + i]);

        selected = -1;
    }
};

// the test function was used to check if the grid was arranged correctly
document.querySelector("#test").addEventListener("click", async () => {
    const res = await fetch("/test", {
        method: "POST",
        headers: {
            "Content-Type": "application/json",
        },
        body: JSON.stringify({
            data: moveHistory,
        }),
    })
        .then((r) => r.text())
        .then((r) => alert(r))
        .catch((e) => alert(e));
});
```

All this was wrapped in a `async` function which was being called at the end of the script.

We could see the `/data` fetched in the network tab, and the `/test` data ie the `moveHistory` was being sent to the server to check if the grid was arranged correctly.

The `/data` was always the same and didn't change so we could use that data as it is without getting newer data each time.

![data](/assets/posts/LITCTF/scrainbow2.png)

I tested the website by clicking the first 2 squares and last 2 just to get a feel of how the `/test` data was being sent so we could later use that information to send our own array later on.

![test](/assets/posts/LITCTF/scrainbow3.png)

## Writing the script


---

[back to index](/posts/LIT-Index/)