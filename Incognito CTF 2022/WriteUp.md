# Incognito 3.0 2022

* Author			: Vignesh Pagadala
* Date				: 23APR2022
* CTF alias 		: sh0tgun
* Team 				: VM2000
* Flags Captured	: 3
* Rank				: 91/300

---

## Web
### 1. Web Challenge 1

We are provided a website with nothing visible in it, which is supposed to be a secretive dark net web forum, that requires an invite code to enter. The page loads with a gif and JavaScript element in the front. I removed the JavaScript using element filtering in the Chromium browser. Once again, we get a dark page with nothing obviously visible. 

I fired up Burpsuite, intercepted the request and found a form field hidden in the web page, asking for the invite code. 

![](https://github.com/vignesh-pagadala/ctf-writeups/blob/main/Incognito%20CTF%202022/Web/Web%20Challenge%201/Screenshot%20from%202022-04-23%2008-42-40.png)
![](https://github.com/vignesh-pagadala/ctf-writeups/blob/main/Incognito%20CTF%202022/Web/Web%20Challenge%201/Screenshot%20from%202022-04-23%2008-54-30.png)

I wasn't exactly sure in what direction I had to proceed, but tried an SQL injection on the input field, and it worked! I used the standard SQL injection paylod ```' or 1=1 -- -``` which gave me the first flag. Alternatively, entering 'admin' into the form field also worked. 

![](https://github.com/vignesh-pagadala/ctf-writeups/blob/main/Incognito%20CTF%202022/Web/Web%20Challenge%201/Screenshot%20from%202022-04-23%2008-42-25.png)


### 2. Web Challenge 2


In the next page, we are given a login page.

![](https://github.com/vignesh-pagadala/ctf-writeups/blob/main/Incognito%20CTF%202022/Web/Web%20Challenge%201/Screenshot%20from%202022-04-23%2008-59-43.png)

I immediately started scanning the page for an SQL injection vulnerability. Using sqlmap made this easier, but it was obvious that the input field was being filtered for SQL injection. So I tried typical filter-evasion techniques using encoded strings for the SQL OR and AND clauses. This approach worked, taking me to the next page with the flag.

![](https://github.com/vignesh-pagadala/ctf-writeups/blob/main/Incognito%20CTF%202022/Web/Web%20Challenge%202/Screenshot%20from%202022-04-23%2011-46-41.png)


### 3. Web Challenge 3

We have a form field asking for a 4-digit OTP. Using Burpsuite to perform a sniper brute-force attack on the OTP field revealed the next flag. 