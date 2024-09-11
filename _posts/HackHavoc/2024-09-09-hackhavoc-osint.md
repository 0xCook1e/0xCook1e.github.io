---
title: HH - OSINT
date : 2024-09-09 21:30:00 +0530
categories: [ctf, hackhavoc]
tags: [hackhavoc, ctf]
description: OSINT challenge write-ups
---

## CyberMaterial’s Cyber-Sleuth Newsletter

Description: *This month, there was an incident, and CyberMaterial is fast in publishing the newsletter, as you know. A Hacker leaked unreleased Netflix content, with Netflix hit by a major data breach as episodes of Arcane and Heartstopper leaked online.*

*But wait, they got the scoop before anyone even knew about the hack? 🧐*

*Let's see if you caught that.*

So I searched for Cybermaterials newsletter and found a newsletter on linkedin. After going through a few of the newsletter I found which had the flag and the article about the Netflix Leak.

![news](/assets/posts/hackhavoc/osint1.png)

## Meet me here !

Description: *You have received an exclusive invitation to a secret CyberMaterial party. The invitation includes a single photo. The message reads, "Can't wait to see you there! Bring your best detective skills. Don't be late!"*

*Flag Format: CM{abcdef_abcd_ab}*

We are given a image. I noticed few things about it.

1. The image was taken at a gas station. Most likely in USA.
2. The image had a signboard of WAFFLE INN.
3. A subway in the gas station.
4. Cover6 Solutions T-shirt.

So, I started by searching Cover6 Solutions, which was in Washington. So I searched WAFFLE INN in nearby areas of Washington. I found Waffle Inn in Verona previously WAS foundable using google maps but now I cannot find it, directly as the shop closed down.

The authors released another photo with 'color' and different angle which i could reverse search and found the location of the shop.

![waffle](/assets/posts/hackhavoc/osint2.1.png)

The flag is the name of the road, all in lowercase and in the flag format given.

![waffle2](/assets/posts/hackhavoc/osint2.2.png){: w="700"}

> Flag: `CM{laurel_hill_rd}`

## APT Intel Hunt

Description: *You’re up against one of the most notorious APT groups—Lazarus. These cyber troublemakers have been causing chaos, and it’s up to you to outsmart them before they can make their next move.*

*Word on the street is that they’ve dropped some hints about their latest scheme. A recent CyberMaterial report on their mischievous sub-group, Andariel, might just be the treasure map you need. But remember, Lazarus is like a sneaky cat—hard to catch and always up to something devious.*

*Can you unravel their devious plans and find the flag before they hit their next target? Put on your detective hat, crack the code, and save the day! The world’s fate might just hang in the balance. 🕵️‍♂️🔓*

So I Searched about cybermaterial and they had a website where they posted articles. I searched in Threat actors for The lazarus group and found an article. After going through the [article](https://cybermaterial.com/andariel-lazarus-group-threat-actor/) there was a link hidden to a pastebin.

![lazarus](/assets/posts/hackhavoc/osint3.png)

The pastebin had some suspiciously scattered Hex values in the content. I tried to decode them and got the flag.

[pastebin link](https://pastebin.com/QUwg950y)

> Flag: `CM{4pT_Gr0uP5_L4z4Ru5}`

## Catch Me !!

Description: *We’ve got a hot case for you! A beggar on the street is actually a member of Al Capone's mob, and the FBI needs your help to track him down—fast.*

*We've intercepted a suspicious phone number that seems to be connected to this individual—702.724.86XX. However, two digits are missing. se this along with the provided image and other clues to identify his exact location.*

*Report back the name of the building infront of which he is sitting flag format CM{abc_abc_abcdefg}*

So I searched for the phone number and found it was a Las Vegas number.

I analyzed the given image and it was a street view image. and a visible icon was seen. I searched the icon and it apparently meant a museum.

![museum](/assets/posts/hackhavoc/osint4.png)

![museum2](/assets/posts/hackhavoc/osint4.2.png)

So I searched for museums in Las Vegas and found the musuem.

`The Mob Museum`

![museum3](/assets/posts/hackhavoc/osint4.3.png){: w="700"}

Which was also the flag.

> Flag: `CM{the_mob_museum}`

## Oops! Where Did I Hide the Flag?

Description: *Oops! In the midst of creating this OSINT challenge, I might’ve forgotten where I hid the flag in a video post. I remember it was about some interesting news, alerts, and incidents—so many things. Who knew social media could be so… forgettable? 😅*

*Put on your detective hat, dive into the social media jungle, and show me you can find what even I forgot! 🕵️‍♂️💡*

At this stage i was aware of the social media accounts of cybermaterial. LinkedIn seemed highly unlikely for this one as 1 flag was already acquired through there.

Instagram and Youtube seemed highly probable considering the description. I checked the youtube channel and I was first looking at the wrong spot as I misread the question. I was looking for flag inside the video. Then I realized it might be hinting at the text content of the video 'post' which is the description.

After going through a few videos I found the flag in description hidden in '#tags'

![osint5](/assets/posts/hackhavoc/osint5.png)

[Video Link](https://www.youtube.com/watch?v=iM4vtqkhmIo)

> Flag: `CM{SuB5cR1b3_t0_0ur_Y0u7ub3_Ch4nN3L}`

---

[back to index](/posts/hackhavoc-index/)