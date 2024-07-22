---
title: Cat The Quest 2024
date : 2024-07-19 22:30:00 +0530
categories: [ctf, writeups]
tags: [ctf, writeups, catthequest24]
description: Cat The Quest 24 Write-Up
image: /assets/posts/CatTheQuest/header.png
---

Cat the Quest was a unique CTF with a lot of challenges involving series of challenges, ie a series of challenges that are related to each other.
I played Cat The Quest CTF with Team `MONST3RDECK` and we secured 3rd place in the competition. Here are the write-ups for the some of the challenges we solved.

## Portail Captif (Fpopo)

#### Description

*Identify the true identity of Fpopo, an individual mentioned in connection with the Flipper Cater Fpopo. Find the author and find the former name of the Flipper in USGS records.*

Flag Format: `CAT{Rufdfdf833_ffueyf}`

#### Solution

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

## Atlantide Series

It was a 3 part series of challenges which were related to each other in some way or other.

### Atlantide - Strange Account

#### Description

Challenge: Twilight falls upon the forest when your attention is drawn to an unusual glint. Nestled between the gnarled roots of a centuries-old oak tree, a fragment of yellowed paper catches your eye. Intrigued, you pick it up and discover a headline that makes your heart leap: Atlantis Found with a link leading to the dark web. Perplexed, you scan your surroundings. How could such a document end up in this remote forest? Driven by curiosity, you hasten to follow the link. The article that appears on the screen takes your breath away. The evidence presented seems irrefutable, the explanations for the concealment of this discovery from the public, terribly plausible. Yet, you feel deep down that something is off. Is it an elaborate hoax or the greatest discovery in history? Determined to unravel this mystery, you take on the role of debunker. Armed with your critical thinking and thirst for truth, you embark on a perilous quest. You decide to first look at the account of the person who posted the article. It seems that the location of Atlantis can be found from the profile.WARNING: THE FLAG MUST BE SENT IN FRENCH, WITHOUT ANY ACCENT MARKS OR UPPER CASE. e. g If the answer is Black Sea the flag will be CAT{mer-noire}

> Hint: You must understand the meaning of the profile description

#### Solution

In this challenge we were given a md file with some information like Public Email, Number of likes, Number of posts by user, Description and Last connection. Judgeing by the description I thought it was related to finding a user which leading nowhere.

I then read the hint and it said to understand the meaning of the profile description. So I carefully observed the given file. and I noticed there were some numbers hidden in between the whole file.

I extracted the numbers which were `87 254 98 7 3` and then I thought of merging the last 2 single digits and the final number was `87 254 98 73`. These numbers looked like IP address to me and I reverse searched the IP leading knowhere. Then I thought they might be coordinates as the challenge was related to finding the location of Atlantis.

After using the coordinates `87.254, 98.73` in google maps, It lead to arctic ocean, and as said in description I converted it into french and matched the flag format and it was the correct flag.

![arctic ocean](/assets/posts/CatTheQuest/arctic.png){: width="400"}

> Flag: `CAT{ocean-arctique}`

### Atlantide - A Strange Discovery

#### Description

Challenge: As you delve into this intriguing enigma, one question lingers: How could scientists have missed this discovery for so long? However, a disturbing detail catches your attention: how could the member have his e-mail address validated if the domain was never rented? Could you be on the trail of a much bigger mystery than you had imagined? Driven by adrenalin, you decide to continue your investigations, but you must nevertheless advance into the forest. After entering the ruins, you come across another piece of paper, and before moving on, I should start by understanding this one. Suddenly, a thought crosses your mind: maybe some of the elements found in the previous step, coupled with the TXT, can help me move forward. Maybe I should coNSult the different elements I have at my disposal. A ray of hope then appears in your mind, prompting you to explore these unexpected clues in greater depth. With determination and curiosity, you embark on this new phase of your investigation, ready to unravel the mystery unfolding before you. The question remains, what have you discovered?

#### Solution

The first thing I noticed was random capitalized letters in the description and I stored then down for later `TXT NS`

Now moving on to the attachment of a image file which had some interesting instructions on it, and it was related to arrangement of some `Numbers` we found. And YES! it was related to the numbers we found in the previous challenge.

The Instructions (and the attached photo):

![instructions](/assets/posts/CatTheQuest/instructions.png)

After thinking about those for a while it didn't make much sense, So I uploaded to image to an online tool called as [aperisolve](https://www.aperisolve.com/) which is a image steganography tool which runs some basic analysis on the image using some popular tools and image filters. And this I found some hidden text in the image.

![hidden text](/assets/posts/CatTheQuest/hiddentext.png)

So, what the hidden text says is:

- Perform OR operation on each individual digit of a number and the result of the OR operation will be the score of the number.

- Sort the numbers according to the score in descending order.
  
- Perform AND operation if there are numbers with the same score.

- Sort the numbers with same score in ascending order of the AND operation score.

I used python to do these operation, didn't write a script and just did them manually as there werent a lot of them.

These were the results:

OR results:

```txt
8 | 7 -> 15
2 | 5 | 4 -> 7
9 | 8 -> 9
7 | 3 -> 7
```

> The operators `|` and `&` are bitwise OR and AND operators respectively.
{: .prompt-info}

sequence after OR operation: `87 98 73 254`

AND results:

```txt
2 & 5 & 7 -> 0
3 & 7 -> 3
```

Final Sequence: `87 98 254 73`

Now I re-analyzed the description and tried to figure what it was hinting at.

The description said `how could the member have his e-mail address validated if the domain was never rented?` and the capitalized letters were `TXT NS` which was hinting at `TXT Records` and `Name Servers` or `nslookup` tool, and the answer is using a `Custom DNS Server`.

Also, The number sequence looks suspiciously similar to an IP address. Maybe this is the DNS server? `87.98.254.73`

Also the previous email was `verite@the87Atlantide.com` which gives us the domain name `the87Atlantide.com`

![ns lookup](/assets/posts/CatTheQuest/nslookup.png)

After using nslookup on the domain `the87Atlantide.com` with the custom DNS server we get a new IP address, which lead to a website.

new IP - `164.92.184.7`

![website](/assets/posts/CatTheQuest/websitefound.png)

And we get the flag from the website.

> Flag: `CAT{Les-Preuves-Origielles}`

### Atlantide - The Strange Website

#### Description

As you stand before this faulty WordPress site, a question persists: how can a site so poorly maintained present no security flaws? You decide to investigate a bit more deeply.

#### Solution

The website the question was referring to was the website we found in the last challenge `http://164.92.184.7` and it was a wordpress site.

So I started by running `wpscan` on the website to find any vulnerabilities.

![wpscan](/assets/posts/CatTheQuest/wpscan.png)

Which gave us the author information `mathys` and `Platon`

So we tried some basic passwords on the `wp-login` page but to no success. We then confirmed if bruteforcing the login was allowed and we were not given the permission so we had to find another way.

As this was listed under `stegano` and `web` category, I thought of downloading the images in the website and running some tools on them. Which was another wild goose chase. and lead to nothing

Then I reset my thinking and tried to find new way, then I thought of checking the source code which I should have done in the first place and I found a pastebin link commented in the source code.

![pastebin](/assets/posts/CatTheQuest/pastebinlink.png)

[PasteBin Link](https://pastebin.com/xfp6UrgH)

There was a / at the start of paragraph which was suspicious and maybe hinted at a directory.

The pastebin also hinted at checking the UPPERCASE TEXT so I ran a simple regex `[A-Z]+` on the whole paragraph and came up with this string `HYWIHYIAYANCIY`

And then I just tried the endpoint on the website and there we go!! We find the hidden directory which contained the flag and some funny text.

![hidden directory](/assets/posts/CatTheQuest/hiddendir.png)

> Flag: `CAT{Y0u-@v3-SolV3-tHe-mYst3ry}`

## Oxym0r

#### Description

A post relaying the attack against CatTheFlag would have been posted on a social network by someone called OxymOrH4z4RD, it's up to you to find this person and what they are hiding

#### Solution

This was a OSINT challenge where we had to find the social media account of the user `OxymOrH4z4RD`

I searched the username of twitter and found the user, and the user had a post and the post contained a bunch of binary numbers.

[OxymOrH4z4RD Twitter/X Account ](https://x.com/0xym0rH4z4RD)

![twitter](/assets/posts/CatTheQuest/oxy1.png)

I then converted the binary to ascii using cyberchef it turned out to be base64 so I decoded it and got a link to a website.

![base64](/assets/posts/CatTheQuest/oxy2.png)

The website source contained the flag.

![flag](/assets/posts/CatTheQuest/oxy3.png)

> Flag: `CAT{Welc0me_t0_CatTheQuest_h4z4rd}`

## Old Friend

#### Description

Our dear H4z4rd is back, do you remember him? He remembers you. He has used the same communication place as last time for your next mission. Complete it.

#### Solution

We Actually first blooded this challenge and we had perfect team sync for this challenge.

This was a OSINT challenge leading back to our old friend `OxymOrH4z4RD` and the communication place was the twitter account. So we visit the account once again and we see a new post.

![twitter](/assets/posts/CatTheQuest/oxy4.png)

The first part was actually really simple after analyzing the string for a while it was a simple `fill_in_the_blanks` string.

`_y @ i_ _he __y _o __c_y_t` -> `my @ is the key to decrypt`

So the key was `0xym0rH4z4RD`

The second part was a post with only emoji's. Now there are actually ways in which you can encrypt text into emojis so I searched for online tools for emoji decryption and on my 2nd try we found a tool that worked perfectly for the emoji string `😯🙍👚👮👭👢👩🙄😲👵👸😯😶😳😲👚🙄🙎👴👖🙈👏🙈👣😷👡🙊👕👐🙇🙃😰👮😶🙇👹👦👫😴👱👬🙅😶👗😲👫😴👥😵👬🙊🙆👕👦`

[Emoji Decryptor](https://txtmoji.com/)

![emoji](/assets/posts/CatTheQuest/oxy5.png){: width="600"}

The decrypted text was a link to a website `https://riddle.catthequest.com` which had a simple form to submit answer to a riddle.

![riddle](/assets/posts/CatTheQuest/oxy6.png){: width="600"}

the riddle was hidden in the source code and it was a text file.

```txt
Vm0wd2QyUXlVWGxWV0d4V1YwZDRWMVl3WkRSWFJteFZVMjA1VjAxV2JETlhhMk0xVmpKS1IySkVUbGhoTWsweFZqQmFZV015U2tWVWJHaG9UVlZ3VlZadGNFdFRNVWw1VTJ0V1ZXSkhhRzlVVmxaM1ZsWmFkR05GWkZwV01VcEpWbTEwYTFkSFNrZGpTRUpYVFVad1NGUlVSbUZrUlRGWlkwZDRVMkpXU2twV2JURXdWakZXZEZOclpGaGlSMmhoV1ZSS2IxSkdXbGRYYlhSWFRWaENSbFpYZUZOVWJVWTJVbFJDVjAxdVVuWldha3BIVWpGT2RWUnRjRk5pVjJoWFZtMTBWMlF5VWxkalJtaHNVakJhY1ZscmFFTlNiRnBZWlVoa1YwMUVSbGRaTUZaelZqSktWVkZZYUZkaGEzQklXWHBHVDJSV1ZuUmhSazVzWWxob1dGWnRNSGRsUjBsNFUydGtXR0V5VWxsWmJHaFRWMFpTVjJGRlRsUmlSM1F6VjJ0U1UxWnJNWEpYVkVwWFlsaFNNMVpxU2t0V1ZrcFpXa1pvVjJKV1NrbFhXSEJIVkRKU1YxWnVUbGhpVjNoVVdWUk9RMWRHV25STlZFSlhUVlV4TkZaWGRHdFdNV1JJWVVac1dtSkdXbWhaTVZwaFpFZE9ObEpzYUdsU00yaFlWbXBLTkZReFdsaFRhMlJxVWtWYVYxWnFUbTlsYkZweFVtMUdVMkpWVmpaWlZWcHJZVWRGZUdORVdsZGlXRUpJVmtSR2ExWXlUa1phUjJoVFRXNW9WVmRXVWs5Uk1XUnpWMWhvWVZKRlNtRldiWE40VGtaa2NsWnRkRmROYTNCNVZHeGFjMWR0U2tkWGJXaFhZVEZ3VkZacVJtdGtWbkJHVGxaT2FXRXdjRWxXYlhCTFpXczFWMWRzYUZSaE1sSnhWVzE0ZDFkR2JITmhSazVPVFZad2VGVnRNVWRWTWtwV1lrUmFXR0V4Y0ROWmEyUkdaV3hHY21KR2FGaFRSVXBKVm10U1MxUnRWbGRVYmtwaFVteEtjRlpxVG05V1ZtUlhWV3M1VWsxWFVsaFdNV2h2VjJzd2VWVnJPVmRpV0ZKWVZHeGFZV1JGTlZaUFYyaHBVbGhDV2xac1pEUmpNV1IwVTJ0a1dHSlhhRmhaVkVaM1lVWndSbHBHVGxSU2EzQXdXbFZrYzFVeVNuSlRhM1JYVFc1b1dGZFdXbEpsVmtweVdrWlNXRkl5YUZwWFZ6QjRUa1paZUZWc1pHRlNlbXhQVkZaYWQyVkdWblJrU0dScFVqQndWMVl5ZEhkV01ERjFZVWRvV2xaWFVrZGFWV1JQVTBVNVYxcEhiRmhTVlhCS1ZqRmFVMU14VVhsVVdHaHFVbGQ0Vmxsc1pHOVdSbEpZVFZjNWJHSkhVbGxhVldNMVlWVXhXRlZ1Y0ZkTlYyaDJWakJrUzFKck5WZFdiRlpYWWtoQ1dWWkhkR0ZaVjFKSVZXdG9hMUp0VW5CV2JHaERUbXhhVlZOVVJsVk5WbkF3VlRKNGMxWnRSbkpPVjBaVlZucFdkbFpyV21GalZrcDBaRWQwVTJFelFYZFhiRlpoWVRKR1YxcEZaRk5oYkhCWVdWZDBkbVF4V2xWU2JGcHNVbTFTTVZVeWN6RldNa3BYVTI1b1YxWXphSEpaYWtaclVqRldjMkZGT1ZkV1ZGWldWbGN4TkdReVZrZFdibEpPVmxkU1dGUlZVa2RsVmxKelZtMDVWMDFWYnpKVmJYUnZWakZhUmxkcmVGZGhhM0JRVlcxNFlXTXhjRWhpUms1T1ZsWlplbFp0ZUdGVk1VbDRZa1prV0dKcmNFOVdiWGgzVjBac1dXTkdaRmRTYkZwNVZtMTBZVlF4VmxWTlJHczk=
```

I immediately recognized the base64 string and tried to decode it..... but it was not 1.. not 2... but 13 times base64 encoded. 

![base64x13](/assets/posts/CatTheQuest/oxy7.png){: width="600"}

We get a code to submit in the riddle form, and after submitting we are presented with the flag.

![oldfriend](/assets/posts/CatTheQuest/oxy8.png){: width="600"}

> Flag: `CAT{77ce9338-MjAyNC0wNy0yMiAyMzoxNjowNg--b2d5fa50f5dc56e536ce13c7e471f6b2e05f73216f4024fd96a100c44eb4cc17}`

