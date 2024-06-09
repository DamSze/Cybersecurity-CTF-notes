# CTF Name: The numbers

## Challenge Description

The numbers... what do they mean?

## Solution

## Binwalk

Firstly i saw that the file was an image so i opened it

![the_numbers.png](https://jupiter.challenges.picoctf.org/static/f209a32253affb6f547a585649ba4fda/the_numbers.png)

Then i used binwalk to search for any hidden files, it turned out that there was .zlib compressed folder so i extracted it

```
binwalk -e the_numbers.png
```
But it was a dead end.

## Picture
Then i looked at the picture one more time and i noticed that the first part must be a picoCTF, so
```
16:p 9:i 3:c 15:0 3:C 20:T 6:F
```
It also shows that the representation is non case sensitive.


Then i noticed that the nubers are just the representation of alphabet so a=1 and so on...

### Function

I made a script that tested this approach

```
coded = [16,9,3,15,3,20,6,20,8,5,14,21,13,2,5,18,19,13,1,19,15,14]

alphabet = []

for i in range(ord('a'), ord('z')+1):
    alphabet.append(chr(i))

decoded=[]

for code in coded:
    decoded.append(alphabet[code-1])

res = ''.join(decoded)

print(f"Decoded message: {str(res)}")

```

And it turned out to be correct

```
mordzio@fedora:~/pico$ python3 solve.py 
Decoded message: picoctfthenumbersmason
```