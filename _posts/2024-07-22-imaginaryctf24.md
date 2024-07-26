---
title: Imaginary CTF 2024
date : 2024-07-21 00:30:00 +0530
categories: [ctf, ictf]
tags: [ctf, writeups, ictf]
description: Write-up for Imaginary CTF 2024
image: /assets/posts/Imaginary/header.jpg
---

All the original challenges can be found on imaginary CTF [github challenge repo](https://github.com/ImaginaryCTF/ImaginaryCTF-2024-Challenges-Public)

## Forensics

### bom (100 pts) - 882 solves

In this challenge we are given a simple text file which on initial viewing seems chinese but it's not.. opening the file in hex editor we can see that the text is encoded in `UTF-16BE` encoding. We can say that because of the BOM (Byte Order Mark) at the start of the file which is `FE FF` in hex.

![bom](/assets/posts/Imaginary/bom2.png)

More info about [BOM](https://en.wikipedia.org/wiki/Byte_order_mark)

![bom](/assets/posts/Imaginary/bom1.png)

> Flag: `ictf{th4t_isn7_chin3se}`

### packed and routed

These are 2 Challenges but I combined them as they shared the same attachment

#### Description

author: Eth007

**packed (100 pts) - 605 solves**

Packet Tracer is a cross-platform visual simulation tool designed by Cisco Systems that allows users to create network topologies and imitate modern computer networks. The software allows users to simulate the configuration of Cisco routers and switches using a simulated command line interface. (same attachment as routed)

**routed (100 pts) - 157 solves**

Can you dig a bit deeper? (same attachment as packed)

There are some fake flags; this is unintentional. The real flag is not in plaintext.

#### Solution

In given attachment was `packed.pkz` which is a packet tracer file but it was actually a zip file as well as indicated by the file header `PK` which is the magic bytes for a zip file.

![packed](/assets/posts/Imaginary/packed1.png)

So after extracting it its pretty simple. There was the same packed.pkz inside but there were another files as well. One of it was `secret.png` which had the flag in it.

![packed](/assets/posts/Imaginary/packed.png)

> Flag: `ictf{ab4697882634d4aeb6f21141ea2724d0}`

For the second part I loaded up the packet tracer file in the packet tracer software and this was the network topology.

![routed](/assets/posts/Imaginary/routed1.png)

Now, I have used packet tracer before and I know that the routers can be configured to have a password and the password can be extracted from the configuration file of the router and the name hinted at router as well so I went to the router configuration and extracted the configuration file.

![routed](/assets/posts/Imaginary/routed2.png)

The Password was in the configuration file in the password was encrypted using the type 7 encryption which after googling I found was a weak encryption and can be decrypted easily online.

![routed](/assets/posts/Imaginary/routed3.png)

the encrypted password = `020F074F0D1D0728484A0C173A191D1F330C2B382C2D3728`

![routed](/assets/posts/Imaginary/routed4.png)

> Flag: `ictf{hidden_not_hashed}`

### Sleepy Alarm (471 pts) - 19 solves

![nayuki](/assets/posts/Imaginary/nayuki.png)

#### Description

Author: Minerva

Yuuichi woke up for his school, but the alarm audio seems to have an extra jingle in it. Maybe you can help him uncover the secret?

Hint: The flag length, including ictf and enclosing braces, is 39.

#### Solution

We are given a mp3 file which is `Nayuki's Alarm Clock` from the anime `Kanon`.

After opening the file in Audacity and switching to the spectogram view I see soemthing suspicious in the spectogram at around 8khz frequency.

![sleepy](/assets/posts/Imaginary/sleepy1.png)

Now what i thought was i needed to see what was going on at 8khz frequency so I applied a EQ filter (Graphic EQ) and lowered all the other frequencies to 0 except 8khz. I repeated it around 2-3 times until i was able to see something

![noisy](/assets/posts/Imaginary/sleepy2.png)

The waveform was starting to look like a message. It looked like binary code which after the ctf i got to know is called `Amplitude Shift Keying` which is a form of modulation. This was how i did it the first time which had a lot of noise in some parts of the message. I tried to decrypt the message ( *I did it manually please do not judge me 😭* ) but due to the noise i was unable to get it. which came out to like `ictf{A_sl33p5_gqYuEi_alarm_&rh34dc1bb2}`

Afterwards my teammate found a different effect which produced much cleaner results, using the `special > vocal reduction and isolation`

Now I messed around with this effect and i found a perfect setting which was using the option `remove center` and setting the threshold values which isolated the 8khz frequency and got us a much cleaner message.

![special](/assets/posts/Imaginary/sleepy3.png)

After that I used the EQ filter again the increase the amplitude of the 8khz frequency and I was able to see the message clearly.

![clean](/assets/posts/Imaginary/sleepy4.png)

Now I decoded the message and got the flag. ( *maually again :<* )

> Flag: `ictf{1_sl33py_NaYuKi_alarm_2a634dc1bb2}`




## OSINT

### dog-mom (100 pts) - 271 solves

#### Description

author: Eth007

i'm a dog mom i 🩷 dogs

Find where this picture was taken; submit your flag as ictf, both rounded to three decimal places. (example: ictf{-12.345_66.533})

#### Solution

So, We are given this image from top of a building and the phrase `i'm a dog mom i 🩷 dogs` carved or written onto a wooden bar? the background which has more interesting information about the location like surrounding buildings and structures is a little blur.

![dog-mom](/assets/posts/Imaginary/dogmom1.png)

Well the written text doesn't seem to be much interesting after observing it more closely but it might come in handy if other methods fail. So I'll keep that as the backup.

Next, I check the metadata as the image was quite large in size *~9mb*. So, I ran exiftool on it and.. nothing interesting..

Next, I do a reverse image search on google and keep adjusting the cropping and looking at the few top results, I usually like to see around top 15-20 results as it reduces the changes of missing something obvious.

![reverse search](/assets/posts/Imaginary/dogmom2.png)

Well after adjusting it for a while I find a extremely similar image which also had the same angle and the image poster actually added the name of the location in the title `Cathedral of Learning` Nice!

Now I head onto Google Maps and search for `Cathedral of Learning` and I copy the coordinates from the search bar and..... no flag.. well turns out the flag was a little bit around and not exact so I had to trial and error some coordinates and then it finally worked.

Thats one the of the annoying parts of Geo-OSINT challenges that sometimes the coordinates don't work as expected and you have to try a few more times.

> Flag: `ictf{40.444_-79.954}`

### Cartesian Series

> Cartesian is a 3 part challenge series (I, II, III) and all were based on the same person, Terrence Descartes.
{: .prompt-info}

#### Description

Author: Eth007

**cartesian-1 (100 pts) - 550 solves**

Greetings. You have been tasked with investigating the whereabouts of a potential recruit. To perform this top-secret background check, we must gather as much information as possible.

Please investigate Terrence Descartes. We know that his social accounts are relatively new, so please do not attack anything out of scope. For the sake of this series of challenges, nothing pertaining to Terry has existed before July 17, 2024. Do not investigate anything posted online before then.

**cartesian-2 (100 pts) - 95 solves**

Please keep digging into Descartes. We have reason to suspect that there might be more to him that it seems. Look into his trip last summer. See if you can find anything up with him.

**cartesian-3 (100 pts) - 91 solves**

We have reason to believe that Terrence is up to no good... we need to gather evidence. To do that, we need you to reset his password so we can have access to his accounts. With all the research you've done, it should be done in no time!

http://cartesian.chal.imaginaryctf.org/

Update - 7/20/24 00:25 UTC: The challenges cartesian-2 and cartesian-3 have been updated. Terrence has posted information online that will be relevant in solving these challenges. I apologize for the oversight.

#### Solution

Alright so this is a long challenge which had 3 parts. I'll start by talking about solving part 1 and move 1 by 1 to the next parts.

The first 2 cartesian challenges were based purely on finding flag using OSINT but the 3rd one we had to answer a questionairre to get the flag the questionairre was based on the information we gathered from the previous 2 parts on *Terrence Descartes*

So, the first thing I tend to do in a OSINT challenge when a person's name is given is I start off by searching the name on popular social media platforms like `Twitter, Instagram, LinkedIn.` altho there are other platform I prefer these for collecting information first.

So, I start off by searching the name `Terrence Descartes` on Twitter and there's no one.

I move on to the next platform *Instagram*, After searching on instagram the profile pops up immediately as its the only one that matched the search query.

![instasearch](/assets/posts/Imaginary/terrence1.png)

This is how the profile looks like and the [link](https://www.instagram.com/descartes.terry2001/) to the profile, if you want to continue investigating yourself.

![instaprofile](/assets/posts/Imaginary/terrence2.png)

I go through the posts 1 by 1 and I notice potentially interesting information we might need to use in the upcoming parts which I'll get to later.

Then I view the stories posted by Terrance and there's a story which has the flag for the first part. The stories also included more information which we will be using in the next parts.

![cartesian1](/assets/posts/Imaginary/terrence3.png){: width="50%"}

> cartesian 1 Flag: `ictf{i_love_revealing_info_on_the_internet}`

The cartesian 1 was pretty simple and required very basic OSINT skills.

Next, We continue investigating on Terrance Descartes. I go through the posts on instagram again trying to see if there was any more information that I could extract.

Summary from Instagram:

- Terrance travelled to `New York City` in Winter, went to central park and Times Square at night and complained about ads on the screens.
- Terrance finished his last summer classes and was travelling in a car back to his home and was 300miles away, The photo's were AI generated but the car was undeniably a `Honda Civic`
- Had a pet dog named `bonnie`
- Posted on 19th July about *half birthday vibes* and mentions it was in *January*
- The Birthday has a location tagged *Dave and Busters* which I searched on maps and was in a few cities in the US.
- Follows 5 accounts all are the poet `Robert Frost`.

I move on to finding more online presence as I extracted almost all of the information from Instagram. 

I find more social media profiles just by searching the name on `LinkedIn` and `Github`.

Lets dive into `LinkedIn` first, On LinkedIn there is a post with part 1/2 of flag, which I am assuming is for the second part of the challenge.

![linkedin](/assets/posts/Imaginary/terrence4.png)

Summary from [LinkedIn](https://www.linkedin.com/in/terrence-descartes-54642831a/):

- Chief Execution Officer at `Cohort Calculations`
- Location: `San Diego` Metropolitan Area
- Experience:
  - Cohort Calculations (2023 - Present)
  - Goose Farmer, `Farmer Johnson's` Goose Company · Part-time, Greater Los Angeles, California, United States
- A post referencing to his mom

![mom](/assets/posts/Imaginary/terrence5.png)

Summary from [Github](https://github.com/descartes1337):
  
- 1114 miles from Seattle 😢
- Has a repository with a interesting commit that redacted sensitive information.

![commit](/assets/posts/Imaginary/terrence6.png)

- Checked the `.patch` file and found the email address of Terrence
  
![email](/assets/posts/Imaginary/terrence7.png)

Now, with the email in hand and it being a gmail a tool comes to mind `Ghunt` which is a tool that can be used to gather information from google accounts.

Ghunt is free to use tool and can be found [here](https://github.com/mxrch/GHunt)

I run the command ```ghunt email terrencedescartes@gmail.com``` and I see 3 calender events scheduled

![ghunt](/assets/posts/Imaginary/terrence8.png)

I run the command again with JSON output to see in more detail and BINGO! there's flag part 2/2 for the second part of the challenge in the description of the summer trip event.

[ghuntjson](/assets/posts/Imaginary/terrence.json)

> cartesian 2 Flag: `ictf{wh3n_th3y_s4y_publ1c_th3y_m3an_publ1c_9f1b2314}`

Now that we have gathered all the data it's time to answer the questionairre on the website, I'll cover the questions one by one.

1. What is your email?

    The email was found using the `.patch` file which was `terrencedescartes@gmail.com`

2. On what day were you born? (YYYY-MM-DD)

    Using the Instagram post we know that Terrance's half birthday was on 19th July and he mentioned it was in January so we can calculate the birthday as `2024-01-19` but that wasn't the answer so I tried 1 day before and it worked `2024-01-18`

3. What is the name of your favorite pet?

    The pet's name was `bonnie` as mentioned in the Instagram post.

4. What city have you primarily lived in for the past three months?

    The location was found on LinkedIn as `San Diego` as the location of the company he works at currently. So, its safe to assume he lives there.

5. In what city did you grow up?

    Well this was a tricky one as there was no direct information on this but We had 3 clues on this:

   - Birthday was celebrated at `Dave and Busters` which is in a few cities in the US. Might have been in the city he grew up in. Not sure though.
   - 2139 miles from New York City which was mentioned in NYC trip in the calender description
   - 1114 miles from Seattle which was mentioned in the Github profile

    Well using the New York City Information only I found the city which matched the exact distance which was `Pheonix` and it worked from [here](https://www.distancefromto.net/city-west-new-york-us)

    ![distance](/assets/posts/Imaginary/terrence9.png)

6. What is the name of your favorite poet?

    The favorite poet was `Robert Frost` as he followed 5 accounts of him on Instagram.

7. What was the make and model of your first car?

    The car was a `Honda Civic` as extracted from the image of car posted on Instagram.

8. In what year was your father born?

    The father's birth year was not explicitely given but we can calculate it using the github commit history as his father turned 43 in year 2024 so we can calculate the birth year as `1981`

9. What is your mother's maiden name?

    Using the LinkedIn post we know that his mother's maiden name was `Jackson`

10. At what company do you work at?

    Mentioned in the LinkedIn profile as `Cohort Calculations`

11. In what city did you go on vacation last summer?

    This we had to find using the deleted maps comment on [`Como Park Zoo & Conservatory`](https://www.google.com/maps/place/Como+Park+Zoo+%26+Conservatory/@44.9812012,-93.1550234,17z/data=!3m1!4b1!4m6!3m5!1s0x52b32b10dbc7cde5:0x45abc97da82f5f5a!8m2!3d44.9812012!4d-93.1524485!16zL20vMDVmamI2?entry=ttu) which is based in the city `Saint Paul`

12. What are you supposed to do on August 21?

    The calender event mentioned that he was supposed to `Drop off top secret information` on August 21.

13. Who was your boss in your first job?

    The first job was at `Farmer Johnson's Goose Company` and the boss was `Farmer Johnson`

After answering all the questions correctly I got the flag! for the 3rd part which was the final flag for the series.

> cartesian 3 Flag: ![flagfinal](/assets/posts/Imaginary/terrence10.png)

This was a really fun challenge to solve and I enjoyed it a lot.
