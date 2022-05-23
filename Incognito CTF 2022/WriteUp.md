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

We are provided a website with nothing visible in it, which is supposed to be a secretive dark net web forum, that requires an invite code to enter. The page loads with a gif and JavaScript element in the front. I removed the JavaScript using element filtering in the Chromium browser. Once again, we get a dark page with nothing obviously visible. I fired up Burpsuite, intercepted the request and found a form field hidden in the web page. I wasn't exactly sure in what direction I had to proceed, but tried an SQL injection on the input field, and it worked! I used the standard SQL injection paylod ```' or 1=1 -- -``` which gave me the first flag. 


