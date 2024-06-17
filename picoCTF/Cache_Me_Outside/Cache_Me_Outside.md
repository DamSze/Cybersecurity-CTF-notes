# CTF Name: Cache Me Outside

## Challenge Description

While being super relevant with my meme references, I wrote a program to see how much you understand heap allocations. nc mercury.picoctf.net 34499 heapedit Makefile libc.so.6

## Solution

In this challenge we get 3 files:
```
heapedit    libc.so.6   Makefile
```

When trying to run heapedit i get an error:
```
Inconsistency detected by ld.so: dl-call-libc-early-init.c: 37: _dl_call_libc_early_init: Assertion `sym != NULL' failed!
```

So as we can see there is some problem with the `libc` library

In the Makefile is:
```
all:
        gcc -Xlinker -rpath=./ -Wall -m64 -pedantic -no-pie --std=gnu99 -o heapedit heapedit.c

clean:
        rm heapedit
```

The option `-Xlinker -rpath=./` sets library search to the current directory.


# https://github.com/faisalmemon/picoCTF-cache-me-outside


# To Be Continued ...