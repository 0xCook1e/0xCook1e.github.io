---
title: Retro Cookie Clicker
date : 2025-03-17 00:30:00 +0530
categories: [ctf, utctf, rev]
tags: [ctf, writeups, utctf, rev]
description: UTCTF 2025 Retro Cookie Clicker
image: /assets/posts/UTCTF2025/header.png
---

## Description

Gotta click em all!

by sasha (@kyrili on discord)

---

## Tools Overview

This is a GameBoy reversing challenge

> You can also disassemble a game boy ROM image using a ghidra extension [GhidraBoy](https://github.com/Gekkio/GhidraBoy) which might come in handy in some challenges
{: .prompt-info}

I used 2 tools ( emulators ), 1 being `mGBA` and the 2nd `bgbw` , I’ll get to the benefits of both in a minute. Although i am sure you are able to complete this challenge using others which allow you to edit the memory live.

---

## Analysis

![image.png](/assets/posts/UTCTF2025/image.png)

- The game worked by increasing the cookies counter by 1, when clicked, and after 12 cookies +1 dozen got added and cookies are reset to 0, pretty simple.
- The program says getting `max dozen` for the flag
- As of now we don’t know what `max dozen` means but it hints towards manipulating the dozen count.

---

## Solution

Ok, now we know what we might be supposed to do, first thing to find out is where in memory is the `dozens` value stored

- Using `mGBA` we can find out the memory address as it has a tool to inspect memory and a fantastic search option.

![image.png](/assets/posts/UTCTF2025/image%201.png)

- To search more efficiently lets get the `dozen` number up a little so we have less results
- So at around 12 dozen we can see results which we can easily monitor ( there can be others )

![image.png](/assets/posts/UTCTF2025/image%202.png)

- what we do now is to continue adding, so lets make the `dozen = 13` , and hit refresh so that the program doesn’t search for new addresses rather updates the already searched memory addresses.

![image.png](/assets/posts/UTCTF2025/6c80ea64-c1d4-4296-9da6-c4654934cd2f.png)

- We can see something interesting in address `cb96` it increased by 1 after refreshing, just to confirm we perform the same experiment again.

![image.png](/assets/posts/UTCTF2025/ef439219-0dc7-464a-b0bf-aa94039910f7.png)

- Yup!! that is the memory address. Unfortunately, I couldn’t find a way to edit memory in `mGBA` , So we continue the rest of the challenge on `bgb gameboy emulator`

![image.png](/assets/posts/UTCTF2025/image%203.png)

- Start the debugger on bgb and head towards the memory address `cb96`
- After editing the memory we can confirm that this is indeed the address.

![image.png](/assets/posts/UTCTF2025/image%204.png)

- Now we just have to find the right value, after messing around a bit. and changing value to `FFFF`  we can see it overflows, and the returned value is negative.
- After messing around a bit we can get the flag at `7fff` which is `16 bit signed integer` max value.
  
> Also you need to refresh the game by adding cookies so that it refreshes the values.
{: .prompt-info}

![Screenshot 2025-03-29 204922.png](/assets/posts/UTCTF2025/flag.png)

---

> Flag - `utflag{1337hax0r}`

---
