---
title: HH - Crypto
date : 2024-09-09 21:30:00 +0530
categories: [ctf, hackhavoc]
tags: [hackhavoc, ctf]
description: Crpyto Challenge Write-ups
---

## Green Flags 🟢

Description: *Flag Frenzy In a sea of encrypted flags, your mission is to unravel the chaos and reveal the hidden truth.*

*Flag_Format: CM{abcd_abcdefgh}*

NATO's Flaghoist communication was used here. I used the [Navy Signals Code](https://www.dcode.fr/maritime-signals-code) to decode the flags.

Do Check out this [NATO Codes](https://www.nato.int/nato_static_fl2014/assets/pdf/pdf_2018_01/20180111_nato-alphabet-sign-signal.pdf) for viewing the other methods of signals and codes used by NATO. A few re-appear in other CTF's as well.

> Flag: `CM{nato_signals}`

## I can't see it

Description: *In the land of secrets, where the ordinary becomes extraordinary, there’s a riddle that loves to play hide-and-seek. It's hiding in plain sight, yet elusive to the eye. Venture into the realm where invisible ink holds the clues, and remember*

We are given text in braille. I used [dcode braille](https://www.dcode.fr/braille-alphabet) to decode

Given Text: `⠉⠍⠸⠣⠹⠼⠁⠼⠑_⠃⠗⠼⠙⠼⠁⠇⠇⠼⠉_⠼⠁⠎_⠼⠙⠼⠉⠁⠇⠸⠜`

Flag: `CM{TH15_BR41LL3_1S_43AL}`

## Digital Black Hole

Description: *Imagine a digital black hole where secrets vanish into thin air. We've cast a cryptic message into this void, one that only the most adept machines can decipher*

Another easy question, Just had 3 binary encoding stacked + base62 encoding.

![crypt](/assets/posts/hackhavoc/crypt3.png)

## Dear Trithemius

Description: *The encryption method used in this cipher is a variation of the Caesar cipher, but with a twist. Each letter in the plaintext is shifted by a different amount depending on its position in the string. Non-alphabetic characters remain unchanged. To decrypt, reverse this shifting process.*

We have a simple encryption here. It is implementing a variation of caesar cipher by shifting each character differently. Wrote a simple decryption code using the existing functions and got the flag.

Also the given code was given a `.go` extension but it was python code.

```py
love_letter = "LPXH_Z_AZRDSQZWJI"

def to_my_honey(owo):
    return ord(owo) - 0x41

def from_your_lover(uwu):
    return chr(uwu % 26 + 0x41)

def decrypt(love_letter):
    billet_doux = ''
    for heart in range(len(love_letter)):
        letters = love_letter[heart]
        if not letters.isalpha():
            owo = letters
        else:
            uwu = to_my_honey(letters)
            owo = from_your_lover(uwu - heart)
        billet_doux += owo
    return billet_doux
```

Flag: `CM{LOVE_U_TRITHEMIUS}`

## My Secret X 'V' My Secret Y

Description: *A message from the cheeky code gremlins: Our secrets are hidden in plain sight, like a magician’s trick. Your task? Play peekaboo with bytes to reveal what’s concealed. Remember, it’s not about where they're hiding but who’s hiding!"*

*Hide: 6866507f43181e1874531b79741f59187448791f517256* & *Seek: ??????????????*

It was a simple XOR encryption. Used cyberchef to bruteforce the key.

[cyberchef recipe](https://gchq.github.io/CyberChef/#recipe=From_Hex('Auto')XOR_Brute_Force(1,100,0,'Standard',false,true,false,'')&input=Njg2NjUwN2Y0MzE4MWUxODc0NTMxYjc5NzQxZjU5MTg3NDQ4NzkxZjUxNzI1Ng)

`Key = 2b: CM{Th353_x0R_4r3_cR4zY}`

---

[back to index](/posts/hackhavoc-index/)