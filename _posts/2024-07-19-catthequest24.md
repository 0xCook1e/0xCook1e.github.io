---
title: Cat The Quest 2024
date : 2024-07-19 22:30:00 +0530
categories: [ctf, ductf]
tags: [ctf, writeups, ductf]
description: Cat The Quest 24 Write-Up
image: /assets/posts/CatTheQuest/header.png
---

Cat the Quest was a unique CTF with a lot of challenges involving series of challenges, ie a series of challenges that are related to each other.
I played Cat The Quest CTF with Team `MONST3RDECK` and we secured 3rd place in the competition. Here are the write-ups for the challenges I solved.

## Fpopo

*Identify the true identity of Fpopo, an individual mentioned in connection with the Flipper Cater Fpopo. Find the author and find the former name of the Flipper in USGS records.*

Flag Format: `CAT{Rufdfdf833_ffueyf}`

This was a OSINT Challenge where we had to find 2 parts of flag, First was finding the author of the book and second was finding the former name of the Flipper in USGS records.

The Part 1 was pretty straightforward, by using some keywords and Google Search, I stumbled upon a reddit post which said the name of their flipper zero was Fpopo. Now even tho this was a little vague, the username of commentor fit the flag format perfectly.

[Reddit Post](https://www.reddit.com/r/flipperzero/comments/1275a01/comment/jedxsoc/)

![fpopo](/assets/posts/CatTheQuest/fpopo.png)

The Part 2 was a little tricky and vague(r), So the Solve was similar you had to use Google Dorking or search using keywords.
After some experimenting this is what gave the result.

Google Dork: `"flipper", "fpopo" site:usgs.gov` This lead to a USGS pdf in which you had to search flipper.

[USGS PDF](https://pubs.usgs.gov/pp/0183/report.pdf)

![flipper](/assets/posts/CatTheQuest/fupper.png)

In the image you can see flipper appearing and reading as `fupper` which was the 2nd part of the flag.

The Challenge was a little tricky and a little vague. But it was fun to solve. *prolly also learnt dorking more properly*

> Flag: `CAT{Banshee888_fupper}`

*Will Be Updating Soon with more challs :D*
