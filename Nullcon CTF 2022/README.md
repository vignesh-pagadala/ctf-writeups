# Nullcon HackIM 2022

\+ Author			: Vignesh Pagadala
\+ Date				: 08APR2022
\+ CTF alias 		: sh0tgun
\+ Team 			: V2000
\+ Flags Captured	: 1

---

## Web
### 1. Cookielover
Challenge consists of a web input form. When text is entered into this form field, the message gets signed and the signature is returned. When the text contains the word 'cookie', the text is not signed. We are also given the Python code which signs the text. The objective is to exploit the Python code and get the backend to sign the word 'cookie'. This can be validated with a public key that is also provided.    

## Misc
### 1. Sanity Check
A string is provided, that's it. It was clearly a base64 encoded string. We get the flag once this string is base64 decoded.