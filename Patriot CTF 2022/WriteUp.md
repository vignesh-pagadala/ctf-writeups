# Patriot CTF 2022

* Author			: Vignesh Pagadala
* Date				: 29APR2022
* CTF alias 		: sh0tgun
* Team 				: VM2000
* Flags Captured	: 4
* Rank				: 85/436

---

## Web
### 1. Web Challenge 1

We are given a website with a username-password login field with no context. Entering ' on the page causes it to crash indicating that the form field might be vulnerable to SQL injection. I used the following payload ```' or 1=1 -- -``` and it worked, giving me the flag. 

### 2. Web Challenge 2

For the next challenge, we are given a web page with an input field. When text is entered into this input field, we get a response converting this text into 'memetext'. Had no luck with sqlmap, so I wondered if it was vulnerable to LFI or a dot-dot-slash attack. I tried the `/etc/passwd` payload in the input field, and it worked, returing the passwd file. I then tried looking around in the home directory and found three files:

![](https://github.com/vignesh-pagadala/ctf-writeups/blob/main/Patriot%20CTF%202022/Web/Screenshot%20from%202022-04-29%2020-42-02.png)

I accessed the flag-as98dc6rnv3p948r7asp98fdynp.jpg to get the flag. 

![](https://github.com/vignesh-pagadala/ctf-writeups/blob/main/Patriot%20CTF%202022/Web/Screenshot%20from%202022-04-29%2020-42-57.png)

### 3. Web Challenge 3

Accessing the challenge website, we see a set of links with text saying that the site is completely unhackable. 

![](https://github.com/vignesh-pagadala/ctf-writeups/blob/main/Patriot%20CTF%202022/Web/Screenshot%20from%202022-04-29%2021-09-36.png)

Viewing the HTML reveals the presence of the main.js JavaScript file, which I was able to access.

![](https://github.com/vignesh-pagadala/ctf-writeups/blob/main/Patriot%20CTF%202022/Web/Screenshot%20from%202022-04-29%2021-09-58.png)

Looking into this file, I could see some text being encoded using the atob() function three times. 

![](https://github.com/vignesh-pagadala/ctf-writeups/blob/main/Patriot%20CTF%202022/Web/Screenshot%20from%202022-04-29%2021-10-04.png)

I copied this text into dcode.fr and base64 decoded it three times. This revealed a new web directory. 

![](https://github.com/vignesh-pagadala/ctf-writeups/blob/main/Patriot%20CTF%202022/Web/Screenshot%20from%202022-04-29%2021-10-41.png)

Going to this location showed a Pastebin link, which had the flag. 

![](https://github.com/vignesh-pagadala/ctf-writeups/blob/main/Patriot%20CTF%202022/Web/Screenshot%20from%202022-04-29%2021-10-24.png)

### 4. Web Challenge 4

This was definitely more challenging. We are given a website and a form field, with the only other information being that it is running on top of a Golang server. I tried a few directory attacks using dirb, but that didn't reveal much except robots.txt which didn't have much. I then remembered that Golang has a in-built security feature to protect against Local File-Inclusion vulnerabilities. Any input containing '../' is stripped out, but this is only done for HTTP GET and POST requests. This gave me a clue that LFI might be involved. The LFI protection can be bypassed using the HTTP CONNECT method. I used curl with the -X CONNECT option, and the ../ payload worked! I was able to access the /etc/passwd file using /../../../etc/passwd as a payload, but wasn't sure how to proceed from here.

Later during the day, the admins provided a hint that the flag was in the /root/ directory. So we were provided with the location of the flag, but did not know the name of the file to curl into. So I used ffuf to fuzz the directory, and that revealed the flag in the recipe.txt file.  