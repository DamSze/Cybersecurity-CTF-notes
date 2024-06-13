# CTF Name: interncdec

## Challenge Description

Can you get the real meaning from this file. Download the file here. 

## Solution

Firstly i i opened the input file, since it was an ASCII text

```
YidkM0JxZGtwQlRYdHFhR3g2YUhsZmF6TnFlVGwzWVROclgyZzBOMm8yYXpZNWZRPT0nCg==
```

I saw the '==' at the end of the string so i run it through the base64 and the result was:

```
b'd3BqdkpBTXtqaGx6aHlfazNqeTl3YTNrX2g0N2o2azY5fQ=='
```

I skipped b'' characters and run it through the base64 again:

```
wpjvJAM{jhlzhy_k3jy9wa3k_h47j6k69}
```

We are getting closer to getting the flag because of the { }
Then i used CyberChef and selected the ROT13 brute force option for the first part of the string - wpjvJAM - it should give us picoCTF

![inter_sth.png](/Cybersecurity-CTF-notes/picoCTF/interncdec/resources/inter_sth.png)

We can see that the string needs to be rotated 19 times, final flag:

```
picoCTF{caesar_d3cr9pt3d_a47c6d69}
```

## Resources
[CyberChef](https://gchq.github.io/CyberChef)