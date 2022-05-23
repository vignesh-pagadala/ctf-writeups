# Patriot CTF 2022

* Author			: Vignesh Pagadala
* Date				: 29APR2022
* CTF alias 		: sh0tgun
* Team 				: VM2000
* Flags Captured	: 3
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

