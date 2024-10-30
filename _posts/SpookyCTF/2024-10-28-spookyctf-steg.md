---
title: Spooky CTF 2024 - Steg
date : 2024-10-28 05:00:00 +0530
categories: [ctf, spookyctf]
tags: [spookyctf, ctf]
description: Steg Challenge Write-up
---

## devil's-secret-stash

`easy`-`50 points`-`169 solves`

Description: *In the depths of the Pine Barrens, a cryptic legend whispers of the Jersey Devil guarding a picture. Tales speak of forgotten knowledge sealed within, but only those sharp enough to see the truth can unlock its secrets. The key? The key hiding in plain sight, woven into the eerie folklore itself, waiting for the chosen few to discover and reveal the dark treasures within.*

### Solution

As usual, I approach any steganography challenge by running `exiftool` just to check for any metadata. In this case, there was quite a bunch of metadata but I didnt find anything particularly interesting.

Next up, We have `strings`. This produced interesting results. I see `flag` in strings at the very end. Now I have done quite a few challenges and this usually tends to be file hidden at the end of a image. So, My next step was to view in hex editor.

![strings](/assets/posts/Spooky/steg1.1.png)

I make use of hexinator, but you may use any hex editor doesnt matter. Well, after opening you can see the `PK` header. This is a zip file. and there's a file `flag` in the ZIP file.

![hex](/assets/posts/Spooky/steg1.2.png)

Extract the file by copying the hex data and converting it into a file. You can use commandline or use tools like `CyberChef` to do the same. I'll give command for anyone who wants to use it.

```bash
echo "<hex>" | xxd -r -p > flag.zip
```

After getting the zip file, you'll notice it is password protected. Now, we have to find the password... or crack it.

I used `zip2john` and `john` to crack the password.

![zip2john](/assets/posts/Spooky/steg1.3.png)

After using the password on the zip, you'll get the flag.

> `NICC{J3rS3y_D3v1l_Arch1V3}`

## set-your-intentions-right

`easy`-`50 points`-`311 solves`

Description: *Mary and Maya wanted to spend the rest of their Friday evening having more fun. They decided to go raundonauting, they set their intentions to paranormal and it sounds like they needed to end up hiding from what they found.*

### Solution

Pretty Easy Challenge. We are provided with a mp3. I loaded up the mp3 file in `Audacity` switched over to spectrogram view and found the flag.

This is a pretty common technique for audio steganography challenges.

![spectrogram](/assets/posts/Spooky/steg2.1.png)

> `NICC{UR_4SAK3N_D3CISION}`

## whispers-in-morse

`easy`-`50 points`-`333 solves`

Description: *Mary got a letter from Maya talking about seeing a cryptid sighting but doesn't want other people to know, the only thing attached is this picture? She wonders if there could be a secret message hidden inside.*

### Solution

After running `strings` on the given image. I found a interesting string.

`Password: M.A.__.R.Y`

![strings](/assets/posts/Spooky/steg3.1.png)

I used `steghide` to extract the hidden message.

```bash
steghide extract -sf MaryMorse.jpg
```

![steghide](/assets/posts/Spooky/steg3.2.png)

That is it. We acquired the flag.

> `NICC{tHe_whIspeRz_iN_Th3_aiR}`

## Phenominal-Photo

`easy`-`147 points`-`133 solves`

Description: *Simon was spotted dwelling under the clock-tower yet again, this time taking pictures. He seems to have captured a strange object in the far far distance going left, right, up, and down seemingly lost or out of control. There is a strange aura radiating from the photo, pulsations even, like an SOS. Can you figure out this strange phenomenon??*

### Solution

Another Image Steganography. I follow my routine - `exiftool`, `strings`.

I dont find anything interesting so I move on to `stegseek`.

![stegseek](/assets/posts/Spooky/steg4.1.png)

After running `stegseek`, we get a zip file from it.

Extract the zip file and we are presented with yet another zip file and a text file.

The zip is password protected, and i assume the text file might have the password. I open the text file and I am presented with alien language.

```plaintext
⋔⏃⌿: ⌰⟒⎎⏁, ⎍⌿, ⎅⍜⍙⋏, ⌰⟒⎎⏁, ⎅⍜⍙⋏, ⍀⟟☌⊑⏁, ⍀⟟☌⊑⏁, ⎅⍜⍙⋏, ⌰⟒⎎⏁, ⎍⌿, ⌰⟒⎎⏁, ⍀⟟☌⊑⏁, ⎍⌿

⍀⟒⋔⟟⋏⎅⟒⍀ ⏁⊑⏃⏁ ⍜⎍⍀ ☌⌿⌇ ⟟⌇ ⏃ ⌰⟟⏁⏁⌰⟒ ⎎⎍⋏☍⊬, ⟟⏁ ⍜⋏⌰⊬ ⏁⏃☍⟒⌇ ⏁⊑⟒ ⎎⟟⍀⌇⏁ ⌰⟒⏁⏁⟒⍀ ⍜⎎ ⟒⏃☊⊑ ⎅⟟⍀⟒☊⏁⟟⍜⋏ ⍙⟒ ⍙⏃⋏⏁ ⏁⍜ ☌⍜ (⌇⏁⎍⌿⟟⎅ ⋔⟒⋔⍜⍀⊬ ⋔⏃⋏⏃☌⟒⋔⟒⋏⏁)
```

I use the tool `dcode.fr` to identify the cipher.

![alien](/assets/posts/Spooky/steg4.2.png)

The text translates to

```plaintext
MAP: LEFT, UP, DOWN, LEFT, DOWN, RIGHT, RIGHT, DOWN, LEFT, UP, LEFT, RIGHT, UP

REMINDER THAT OUR GPS IS A LITTLE FUNKY, IT ONLY TAKES THE FIRST LETTER OF EACH DIRECTION WE WANT TO GO (STUPID MEMORY MANAGEMENT)
```

Using the clues provided, I use the first letter of each direction to get the password. `LUDLDRRDLULRU`

Using this password on the zip file, we get the file inside. Its the flag but in alien language again.

> `⋏⟟☊☊{⊑⟒⌰⌿_⋔⟒_⎎⟟⋏⎅_⏁⊑⟒_⌿⌰⏃⋏⟒⏁_⏚0⍜}` -> `NICC{HELP_ME_FIND_THE_PLANET_B0O}`

## photo-clue

`hard`-`966 points`-`49 solves`

Description: *A seemingly innocuous old photo file has emerged, but Mary Morse suspects it may hold the key to deciphering The Consortium's next move. Your task is to analyze the metadata, uncover the true nature of the file, and submit the flag before The Consortium acts. Time is running out—can you crack the mystery behind the photo?*

*(Note: If you choose to use volatility2.6, use profile Win10x64_19041)*

### Solution

#### Memory Dump Analysis

Let's gooo! memory forensics. I love this stuff.

Ok, So I'll be using a tool called `volatility 3` throughout this challenge for analyzing the memory dump. To learn more about `volatility 3`, you can check out the [official documentation](https://volatility3.readthedocs.io/en/latest/)

Now, These kind of challenges can be a bit tricky. If you are not familiar with memory forensics or you basically don't have much idea what you are trying to do, you might get lost. So, I'll try to explain as much as I can.

Initially I went down the wrong path because I didn't think what I should be looking for in the memory dump and spent a bunch of time trying to do stuff which was not needed.

First, You need to know what you are looking for. In this case if you read the description. It suggests that there is a photo which might be hiding some data.

So, Using that information, You can start by trying to find any image files (jpg, png, etc) in the memory dump.

Now, to do that, there is a plugin called `filescan` in `volatility 3` which can be used to find files in memory.

```bash
python3 vol.py -f memory.dmp windows.filescan
```

If you have never run `volatility 3` before, it will take a little bit longer for the first time. And also the time a command takes to run is proportional to the size of the memory dump. So, try to run it on your main machine if possible. As for me running vol3 on my VM, it takes A LOOOOONG time for a single command to run.

After running the command, you'll get a list of files found in memory, with their `memory addresses` and `file paths`.

Now, u can output the data to a file before hand using `> output.txt` to the end of the command or you can copy it from terminal.

We will now try to grep for image files using their extensions.

```bash
grep -iE ".jpg|.png|.jpeg" output.txt
```

Now when you do this there are quite a few results.

![filescan](/assets/posts/Spooky/steg5.1.png)

But these in particular are more interesting.

`0xb70fca699c30  \Users\johndoe\Desktop\REDACTED.jpg`

This `REDACTED.jpg` looks suspicious. So, let's try dumping this file from the memory to get a look at it.

```bash
python3 vol.py -f memory.dmp -o ".\op\" windows.dumpfiles --virtaddr 0xb1084089e960 
```

- `--virtaddr` is the memory address we get from the `filescan` output.

- The `-o` flag is used to specify the output directory. You can use any directory you want. If not used it will dump the files in the current directory.

![REDACTED](/assets/posts/Spooky/steg5.2.jpg){: w="500"}

This is the `REDACTED` image found from the memory. You can use this image if you'd like to proceed yourself.

#### Image Analysis

Now, to analyze to given image. I do a few basic things like `exiftool`, `strings`, `stegseek`.

After running `stegseek`/`steghide` with no password. We get a pdf file from the image.

The pdf file is password protected. So I cracked the password using `john` and `pdf2john`.

![pdf2john](/assets/posts/Spooky/steg5.3.png)

After opening the pdf file, you get a interesting text which is in binary.

```plaintext
01001110 01001001 01000011 01000011 01111011 01001101 00110000 01110010 01110011 
01100101 01011111 01010000 01101000 00110000 01110100 00110000 01011111 01010011 
00110011 01100011 01110010 01100101 01110100 01110011 01111101 00001010 00001010
```

![pdf](/assets/posts/Spooky/steg5.4.png)

I used `CyberChef` to convert the binary to text.

![binary](/assets/posts/Spooky/steg5.5.png)

and we get the flag

> `NICC{M0rse_Ph0t0_S3crets}`

All in all this was a fun challenge. You require a bit of memory forensics knowledge as well as some steganography knowledge to solve this. The first part is the hardest part of the challenge. Once you get past that, the rest is pretty straightforward.

Keep practicing memory forensics by solving more and more challenges, there's no easy way to get good at it. Just keep practicing. I myself am not that good at it but I try to solve as many challenges as I can to get better.