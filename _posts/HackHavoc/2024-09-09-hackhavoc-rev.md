---
title: HH - Rev
date : 2024-09-09 21:30:00 +0530
categories: [ctf, hackhavoc]
tags: [hackhavoc, ctf]
description: Rev Challenge write-ups
---

## Rev is Easy!!

Description: *Welcome to the “Rev is Easy!” challenge at CyberMaterial! Think you’re clever enough to outsmart our file? Prove that “Rev” isn’t just short for “Reverse Engineering,” but also for “Really Easy Victory!”*

Just open the program in a decompiler like Ida, You will see the flag. OR run strings on binary to see the flag.

![reviseasy](/assets/posts/hackhavoc/rev1.png)

> Flag: `CM{ReV_i5_Easy}`

## Go Crazy!!

Description: *In a small, dimly lit room, a determined hacker named killswxtch sits in front of an old, flickering computer screen. They find a book with a note that reads, "Check the sequence." Using this clue, killswxtch deciphers the password and enters it, unlocking a hidden door that reveals secret manuscripts.*

Open program in decompiler like Ida, You will notice the password and the flag itself.

![gocrazy](/assets/posts/hackhavoc/rev2.png){: w="400"}

> Flag: `CM{5O_MuCh_7un}`

## Who’s Really Dunked?

Description: *Cosmicgurl::92 says, "R47RoO7::47 is drunk!" 🍻 R47RoO7::47 responds, "JavaScript::00 is drunk!" 🤪 And then, out of nowhere, JavaScript stumbles in and says, "Yep, I'm actually drunk!" 🍹

So, let’s do a reverse cosmic dance to figure out who’s really had one too many. Spoiler alert: it looks like JavaScript is the real party animal! 🚀🥳*

We are provided with a `PARTY.txt` file. Opening it we see garbage text. I used dcode identifier it was base92 encoded. then ROT47 and I got the js code. Also the problem statement was kinda hinting at the numbers `92` and `47` although I didn't notice it before. Another reason to pay attention to the problem statement. Sometimes you get valuable information from it.

[cyberchef recipe](https://gchq.github.io/CyberChef/#recipe=From_Base92()ROT47(47)&input=NEQkaighVF85fFY2PlghQkgkJHlvPy5BW2ZINW4qWyE8LDA9IU0xU1pUKTInXHp6Oj4keW83K0JtSE5LUXFELDlbaUkqaC1tRV9eXms7VTY3Ujs7b0kxU1pUKSg5R3hJLUc7S283LjFETEVAaUFsbzpAaUxwXCsyRExSYyRvKyUzXVtfdHdaTkU7OF1sSSFhLUFcaW8uLkI5YlEwOUZaezg4UiZPRFloJEQ4YWs7VTY3Ujs7b0xYNDQoRUI9PGc1OkBpTHBcKzJFX1dOOUYhQi09JFR7e1tDQEo4YT5IIVY1KVIjSzEuMT9HTlRnXj5OLT0jSCFFLjIpMVJtO0ElVDhWUUYoITJGOiRHSygyMDUlWmpGXS9QaWxDZUNRcWc1Nk5cbWleVF9KZUU/JG8lVDUndEAuZVBsbUBSWiZwdS41ZjA0bzlZOVVBbyYpMFYhPG8xdjRBJDxcQGU0LD4zVjREXG4hQVRhP1M4XSckYUw3LyUqJ3ctbCM7Tk4%2BYTBtLT87O21lLlEuWEp4PHcwXi1BXGlvLitjbThJSDlGZE04NlImdHgtKyMvSjdTWHJlQH0lQTRBJ10hYzhha3V1PjphaVEpQi08eT5ebCdVMF45WSRIdHlbIz5vVChURjNNRnsla0gwMUFKTk0qU2t4KjUsI0hhTlRhZmwpLSRuIUItPSNHT0RZa21YU0RVIzBjOFd1WUFXLS0/P1E1J31hTDhXdCtPRldvbWFIOjtBYXQtQ3R0aV5bQkRWVG0pZyMzSEQlQTRBJ10hYzhYJG4hQi09I0dPRFlrbVhTRFUjMGM4V3VZQVctLT8/UTUoKWl7OVtbYSwtLGlEeWx4KVdvPkBhc3t5MytRP0VROlNqZnJILVthMnlQayFjOFgkbiFCLT0jR08zJ10hYzhha3V1MDdTJH1vSV5UWlQpKDlGIUItPSNHTzMnXSFjOFgkbiFCLURqXU9fLSxbakp3VEVsezUlJEh5KStyI1dKfD1SIWg2LGd4I2lYU0peVUQ5RiFCLT0jR08zJ10hYzhYJG4hQi1AXF0pNStjbThJTStQIVk3UTp7UGpYU0peVVtQMD47JVUjR08zJ10hYzhYJG4hQi09I0dPUjJUJExPdD06emstQS9MJlhafSNRTysoKWl3LT90S2lcJ14zfFF7U2EhYzg0JFR7e1tDPm9UKFRGM005d1pjTzMnXSFjOFgkbiFCLT0jR08zJ15bTThmbGlVPjphbCd7didiaHRvJikwdTI7R1JXQ3gvQ2xDOFgkbiFCLT0jR08zJ10hYzhYJG4hQi09JEh5KStyI3xvJikwdTI7R1EuOk8kPFp7OFgkbiFCLT0jR08zJ10hYzhYKHFGYSZXOXZPMyddIWM4WCRuIUItPSNHTzMsN0oqX0Rqd3VCNSVdSiEyNSdodDhlQkN1MjldXTo6RidfZmwpLSRuIUItPSNHTzMnXSFjOFgkbiFCLT0jR3BiV29PZGJYJG9TJzdRaU0pRypPKXorMVFvIUItPSNHTzMnXSFjOFgkbiFCPUpaYzRBJ10hYzhYJG4hQi09I0dPMyddIWNKeGlCZE4zXl1BbzBZKTQoSCgrUkR5LUMyUnt1LDc/P05PP11mcjxmWmNPMyddIWM4WCRuIUItPSNHTzMnXSFjOFgmcHUuNWYle2EoMD9QRkZlU2FhVzpEMXY0QSddIWM4WCRuIUItPSNHTzMnXSFjWHQ5RUZhLT0jR08zJ10hYzhYJG4hQi09I0dwYldvT2RiWCRvUmE%2BWzkpMC5QayFjOFgkbiFCLT0jR08zJ10hYzhoVzwjOTYsaGx3Viw3SipSYT06IVY4V2lFKm1YUz5vSjZVIWlhN3I7U2xLWFQ5NVJhPTohWDtoL1tsUVhTPm9KNlUhaU0lVSNHTzMnXSFjOFgkbiFCLT0jR089LTx4dFJaJmk8JTUnUiZvOGR7LmdKMitQIXRGQXYxbithXjpnZioqXTlbRV06b3B0X2c/N2oxU1IzTEU%2BJktWWTNrNCFoKDx4K08zY3Y1bW4rVUV8ayMrISMuNU1cVVBiYiM6Y0VJQVZdeyZXOXZPMyddIWM4WCRuIUItPSNHTzMsN0oqX0E8dy1zQF50S2lcMU8kRG85JG5hYjh3aG0pQCtGSk5RfEA5IW8mVzl2TzMnXSFjOFgkbiFCLT0jR08zJ10hYzhdJ1x6ejhXXF1LLVo9UHdbO1Rdem45WztUKmlXcD9HTzJsUU9DLyovW08%2BWWkuTjheVSQ7Xz5SJXpPPllpLk5hMlAwPk4tPSNHTzMnXSFjOFgkbiFCLT0lSU8%2BLGk5YjhkIy8%2BTi09I0dPMyddIWM4WCRuIUItPSNHTzMnXjl2Tk8nXHUyQmpdKXI4XUBQRkZnJ3YrJTREW19wYldvUSc4WT5IPk4zXiQ0dHdfSClVbVc5RiFCLT0jR08zJ10hYzhYJG4hQi1CZyowOCddIWM4WCRuIUItPSNINjI0XGxDOFgkbiFCLT0jSDYyNFxsQzhYJG4hcUEqOSkwTyQ8WlQpPFc8Izw6YnQoKUItPHgrUmMkblp7N3QwQSlAJ107LXIkKlUuQy1AL0wneFE9W01TRmssMGM4V3Myc0stfVZUSnpsOTNcQH0lQTRBJ10hYzhhazwwbzlcczJsUFwoKS9POj0rKyUzX1xdcFwtfVZUXl8nJFVjRT1eJ0Q6W0Moa0VCPTtkQTg4MEEpUTJFP0dJUlUjMSRAPy9cLy4xU1pUKThQMD47JVxqXU81LjEuZVJaKClpdy0/UVFpXllpRS9JUlAwPmM2LGhsd3JeVEo&oeol=CRLF)

The flag was being build in the code using some checks.

> Flag: `CM{News_Alerts_Incident}`

## The Key to Nowhere

Description: *You’ve got your hands on a mysterious file called wkwkwkkw, and the word on the street is that only those with a sharp mind and a good sense of humor can unlock its secrets. Legend says it holds the key to something... static, perhaps? Who knows?*

### Initial Analysis

I usually begin analyzing the file using `file` command to get information about the given binary. The file was a `ELF 64bit executable`

![rev4](/assets/posts/hackhavoc/rev4.1.png)

I ran strings on binary and noticed quite a lot of python related information like modules and python version like `3.10` .

![rev4.2](/assets/posts/hackhavoc/rev4.2.png){: w="400"}

After some researching using Google and Chatgpt, I found the binary may be bundled using [`PyInstaller`](https://pypi.org/project/pyinstaller/) which is a tool to convert python scripts into standalone executables. I continued my searched and found out a tool called [`pyinstxtractor`](https://github.com/extremecoders-re/pyinstxtractor) which can extract the contents of file bundled using PyInstaller.

### Extracting the contents

I cloned the repo and ran the tool on the file and it extracted the contents of the file to a folder.

The repo also suggested to use a decompiler on the extracted `pyc` files.

![rev4.3](/assets/posts/hackhavoc/rev4.3.png)

### Decompiling the code

```bash
└─$ file 3.pyc
3.pyc: Byte-compiled Python module for CPython 3.10, timestamp-based, .py timestamp: Thu Jan  1 00:00:00 1970 UTC, .py size: 0 bytes
```

I searched for a CPython decompiler and found [`pycdc`](https://github.com/zrax/pycdc)

After cloning the repository run the following commands in the directory of the downloaded repository:
> cmake .
>
> make
>
> make test

This will build the decompiler and run the tests.

> Some of the tests may fail, but the decompiler should work fine.
{: .prompt-info}

Run the command `./pycdc <filename>` to decompile the file.

After decompiling you may see this specific function in the code which was generating the flag. (The decompiling is not perfect and you have to understand the code yourself)

```py
def get_hidden_flag():
    '''Retrieve the hidden flag.'''
    return ''.join((lambda .0: for c in .0:
chr(c))((82, 51, 86, 95, 68, 52, 84, 52, 95, 72, 51, 114, 79)))
```

The basic idea here is the code is converting the values to ascii and joining them to get the flag.

after converting to ascii we get `R3V_D4T4_H3rO` which was the flag

> Flag: `CM{R3V_D4T4_H3rO}`

## Awwwwwwwwwwwwwww!!

Description: *So Much Awwww & Awaaaaaaaaaaa by Jelly Hoshiumi*

*Flag: Enclosed string with CM{....}*

![aww](/assets/posts/hackhavoc/awa.png){: w="300"}

We are given a `Awaaaaaaaa.png` (not the one above) and a `Awwwww.txt` which consisted of awa5.0 code. The png file was running the same code given to us in the online Awa5.0 interpreter. The input was supposedly the flag ( hidden ) and output was visible, which looked like the shuffled flag.

![awaaaaa](/assets/posts/hackhavoc/awa2.png)

I read the docs of awa5.0 and found it uses `awascii` instead of ascii, and not all characters were used.

The length of the flag was 32. So I typed in 32 characters supported by awascii and it gave the shuffled result. Now i had to just map the shuffled characters to the original characters.

```py
def get_shuffle_pattern(original, shuffled):
    pattern = []
    for char in shuffled:
        pattern.append(original.index(char))
    return pattern

def unshuffle_string(shuffled, pattern):
    unshuffled = [''] * len(shuffled)
    for i, pos in enumerate(pattern):
        unshuffled[pos] = shuffled[i]
    return ''.join(unshuffled)

original_string = "AWawJELYHOSIUMjelyhosiumPCNTpcnt" # Input given by me
shuffled_string = "eSlyhosaiuEmHPICJWNTLpcntMAwYOUj" 

pattern = get_shuffle_pattern(original_string, shuffled_string)
print(f"Shuffle pattern: {pattern}")

input_string = "owoosHiai1w1aia_awJ3ally!0awwa_o" # Output from the image given
unshuffled_string = unshuffle_string(input_string, pattern)

print(f"Unshuffled string: {unshuffled_string}")
# Unshuffled string: awawawawaawa_0oooosHii11i_J3lly!
```

> Flag: `CM{awawawawaawa_0oooosHii11i_J3lly!}`

---

[back to index](/posts/hackhavoc-index/)