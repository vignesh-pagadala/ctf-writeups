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
![](https://github.com/vignesh-pagadala/ctf-writeups/blob/main/Incognito%20CTF%202022/Web/Web%20Challenge%201/Screenshot%20from%202022-04-23%2008-59-43.png)




