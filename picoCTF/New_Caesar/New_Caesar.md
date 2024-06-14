# CTF Name: New Caesar

## Challenge Description

We found a brand new type of encryption, can you break the secret code? (Wrap with picoCTF{}) 
```
mlnklfnknljflfmhjimkmhjhmljhjomhmmjkjpmmjmjkjpjojgjmjpjojojnjojmmkmlmijimhjmmj
```
## Solution


We are provided with a script new_caesar.py
I looked briefly through it but firstly i want to start with testing the algorithm.

My first approach was to give alphabet as a string to encrypt and a one letter char as a key i chose 'a'

```
flag = "".join(ALPHABET)
key = "a"
```

The result i got was this:
```
gbgcgdgegfggghgigjgkglgmgngogpha
```
First things i notice about this is that the length of string doubled 16 -> 32.

Now let's take a look on the code
-----

First thing to notice is the key conditions,
```
assert all([k in ALPHABET for k in key])  ## key in range (a,p)
assert len(key) == 1 #  key only one letter long
```
Now the b16_encode function - It padds each letter to eight bits and then splits it in half, so it returns two letters in range (a,p) 

```
def b16_encode(plain):
    enc = ""
    for c in plain:
        binary = "{0:08b}".format(ord(c)) ## padd char to 8 bits
        enc += ALPHABET[int(binary[:4], 2)] # 0-3 bits - first char
        enc += ALPHABET[int(binary[4:], 2)] # 4-7 bits - second char
    return enc
```

and shift function that shifts the letters:

```
def shift(c, k):
    t1 = ord(c) - LOWERCASE_OFFSET
    t2 = ord(k) - LOWERCASE_OFFSET
    return ALPHABET[(t1 + t2) % len(ALPHABET)]    
```

## Solving

My approach to solving this problem was very chaotic and for sure not optimal but it worked.

Firstly i made an array of all printable ASCII characters
```
'0123456789abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ!"#$%&\'()*+,-./:;<=>?@[\\]^_`{|}~'
```

Then i used all possible keys to encode this characters (a-p)  an then i used a notepad++ app to scan the solutions fastly and narrow it down to only few possible keys 

![crypto_ex.png](/picoCTF/New_Caesar/resources/crypto_ex.png)

My final possibilities were f,g,h and then i added some lines to the code:
```
keys = "g"
#assert all([k in ALPHABET for k in key])  ## key in range (a,p)
#assert len(key) == 1 #  key only one letter long
ds = {}
for key in keys:
    b16 = b16_encode(flag)
    enc = ""
    for i, c in enumerate(b16):
        enc += shift(c, key)
j=0
for i in range(0, len(enc), 2):
    if i != 0:
        j = int(i/2)
    ds[enc[i:i+2]] = flag[j]

print(ds)
to_dec = "mlnklfnknljflfmhjimkmhjhmljhjomhmmjkjpmmjmjkjpjojgjmjpjojojnjojmmkmlmijimhjmmj"
dec = ""
for i in range(0, len(enc), 2):
    dec += (ds[to_dec[i:i+2]])
    print(dec)
```

If the key gave me an error i switched to the next one

Finally i got a correct flag:

```
picoCTF{et_tu?_a2da1e18af49f649806988786deb2a6c}
```

## Thoughts

My approach was not optimal and it took my some time to get it right but hey at the end of the day it did ok and gave me correct sollution. But i am for sure going to read a writeup to learn a better approach xd