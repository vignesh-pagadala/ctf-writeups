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



I fired up Burpsuite, intercepted the request and found a form field hidden in the web page, asking for the invite code. 

![](https://github.com/vignesh-pagadala/ctf-writeups/blob/main/Incognito%20CTF%202022/Web/Web%20Challenge%201/Screenshot%20from%202022-04-23%2008-42-40.png)
