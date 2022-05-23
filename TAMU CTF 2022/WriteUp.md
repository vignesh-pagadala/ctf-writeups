# TAMU CTF 2022

* Author			: Vignesh Pagadala
* Date				: 15APR2022
* CTF alias 		: sh0tgun
* Team 				: VM2000
* Flags Captured	: 4
* Rank				: 177/476

---

## Web
### 1. Lock Out
Challenge consisted of a PHP web form with a single input field, on an nginx server. Looking at the HTML didn't throw up anything. Doing basic directory traversal attack reveals the presence of the 'login.php' page (which we are unable to view in the browser). I fired up Burpsuite, enabled the proxy, entered a random value into the form field, and hit submit. Intercepting the request, we get:

```
HTTP/1.1 302 Found
Server: nginx/1.18.0 (Ubuntu)
Date: Sat, 16 Apr 2022 05:47:01 GMT
Content-Type: text/html; charset=UTF-8
Content-Length: 414
Connection: close
X-Powered-By: PHP/7.2.34
Location: login.php

<p>gigem{if_i_cant_wear_croc_martins_to_industry_night_then_im_not_going}</p>
<!DOCTYPE html>
<head>
    <link rel="stylesheet" href="/static/admin.css">
</head>
<body>
    <h1>Industry Night Shopping List</h1>
    <p>Croc Martins</p>
    <img src="static/crocmartins.jpg" alt="Croc-Martins">
    <form action="admin.php" method="get">
	<input type="submit" name="PrintFlag" value="PrintFlag">
    </form>
</body>
```
Clearly, we can see the existence of a web form that would print the flag when the correct POST request is sent (with the PrintFlag paramter set to 'PrintFlag'). So we craft the following POST request and send it to the server using the Repeater in Burpsuite.

```
POST /admin.php HTTP/1.1
Host: lockout.tamuctf.com
Content-Length: 42
Cache-Control: max-age=0
Upgrade-Insecure-Requests: 1
Origin: http://lockout.tamuctf.com
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/95.0.4638.69 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Referer: http://lockout.tamuctf.com/login.php
Accept-Encoding: gzip, deflate
Accept-Language: en-US,en;q=0.9
Connection: close

PrintFlag='PrintFlag'
```  

This gives us the flag. 

## Crypto
### 1. Taxes
We are given an encrypted PDF that we have to break in to. Not much is revealed, except that the PDF is someone's tax return. I initially tried looking at the PDF metadata, and binwalk, with no luck. I tried a dictionary attack using rockyou.txt wordlist, which did not work either. 

![](https://github.com/vignesh-pagadala/ctf-writeups/blob/main/TAMU%20CTF%202022/Crypto/Taxes/Screenshot%20from%202022-04-16%2021-49-05.png)

Then I noticed some additional information provided in the challenge description - that it is someone's tax return being returned back to them. It is revealed that the tax preparer has used the customer's SSN to encrypt the PDF - this is the solution. Normally, brute-forcing the PDF would not be feasible, but since this information is provided, we can use it to limit the brute-force search space. In this case since customer SSN is used to encrypt the data, the key is 9 characters, where each character is the digit 0-9. I used pdfcrack with the following parameters to appropriately limit the search domain:

```pdfcrack -c0123456789 -m 9 -n 9 2021-return-encrypt.pdf```

After running for about 2 hours, the decryption key was revealed to be 694705124. Using this to unlock the PDF reveals the flag. 

![](https://github.com/vignesh-pagadala/ctf-writeups/blob/main/TAMU%20CTF%202022/Crypto/Taxes/Screenshot%20from%202022-04-16%2021-48-58.png)

![](https://github.com/vignesh-pagadala/ctf-writeups/blob/main/TAMU%20CTF%202022/Crypto/Taxes/Screenshot%20from%202022-04-16%2021-48-38.png)

## Misc
### 1. Gamer
A file is provided, opening it reveals some sort of a JSON script, but I was unable to identify which application it belonged to. Copy-pasting a portion of the script in a search engine revealed it to be a Minecraft script that spawns objects in-game. I tried to find some sort of an online simulator that could render the JSON, but had no luck. Finally I decided to install a demo version of Minecraft to try the script. Ran Minecraft in Creator Mode, and figured I couldn't run large scripts using the command field. A bit of Googling showed I needed a 'Command Block' which I had to craft and insert the JSON script into. Activating the Command Block with a lever spawned a bat with the flag.