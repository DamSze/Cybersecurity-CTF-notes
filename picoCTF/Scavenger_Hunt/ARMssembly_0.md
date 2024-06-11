# CTF Name: Scavenger Hunt

## Challenge Description

There is some interesting information hidden around this site http://mercury.picoctf.net:44070/. Can you find it?

## Solution

## Understanding the Problem

Firstly i looked through the web and noticed the hint about html, css and javascript, so i looked through the source html and found the first part of flag there


```
<!-- Here's the first part of the flag: picoCTF{t -->
```
then i found the next part in css:

```
/* CSS makes the page look nice, and yes, it also has part of the flag. Here's part 2: h4ts_4_l0 */
```

## Robots.txt

Then i looked through the javascript and found next hint: 
```
/* How can I keep Google from indexing my website? */
```
It's about robots.txt file, after wisiting: http://mercury.picoctf.net:44070/robots.txt


I found :
```
# Part 3: t_0f_pl4c
# I think this is an apache server... can you Access the next flag?
```

## .htaccess

There is another hint.
I don't know more about apache servers and couldn't find anything on the web so i looked it up in the writeup for this chellenge:



It turned out that i have to visit **.htaccess** file which is basically a configuration file for the apache server:
```
# Part 4: 3s_2_lO0k
# I love making websites on my Mac, I can Store a lot of information there.
```
## .DS_Store

Another hint and once more time for research because i have no idea what this is about...

Unfortunately no luck here as well so i looked at the writeup again and found out that there is some **.DS_Store file** that stores additional visual info for mac computers, anyways after accessing http://mercury.picoctf.net:44070/.DS_Store:
```
Congrats! You completed the scavenger hunt. Part 5: _7a46d25d}
```

## Conclusions
New things learned:
- .htaccess
- .DS_Store
<br></br>

Revised:
- robots.txt


## Resources
https://www.cloudflare.com/learning/bots/what-is-robots-txt/

https://help.one.com/hc/en-us/articles/115005586169-What-is-htaccess

https://en.wikipedia.org/wiki/.DS_Store
