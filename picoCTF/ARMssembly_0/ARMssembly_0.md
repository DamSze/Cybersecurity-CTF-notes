# CTF Name: ARMssembly 0

## Challenge Description

What integer does this program print with arguments 1765227561 and 1830628817? File: chall.S Flag format: picoCTF{XXXXXXXX} -> (hex, lowercase, no 0x, and 32 bits. ex. 5614267 would be picoCTF{0055aabb})

## Solution

## Understanding the Problem

Classical approach, wgeting the file and then inspecting the content.\
Arm is a new thing for me at this point so i went to the docs and search content on the web and found out that firstly we need to look at the **main** 


I then saw that the function takes two arguments

```
	mov	w19, w0  "w19 -> arg1 after atoi"
	ldr	x0, [x29, 32]
	add	x0, x0, 16
	ldr	x0, [x0]
	bl	atoi
	mov	w1, w0  "w1 -> arg2 after atoi"
	mov	w0, w19 "w0 -> arg1 before func1"
	bl	func1

```


### Function

Then there is a time to investigate the function itself, and we can immediately notice that the function returns the lower of the two values -> min(a,b)

```
    cmp	w1, w0
    "if(arg2<=arg1)"
	bls	.L2
    "arg1=arg1"
	ldr	w0, [sp, 12]
	b	.L3

```

## Conclusions
It was a very fun challenge that made me look up ARM
