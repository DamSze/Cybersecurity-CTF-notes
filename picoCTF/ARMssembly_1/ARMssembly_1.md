# CTF Name: ARMssembly 1

## Challenge Description

For what argument does this program print `win` with variables 85, 6 and 3? File: chall_1.S Flag format: picoCTF{XXXXXXXX} -> (hex, lowercase, no 0x, and 32 bits. ex. 5614267 would be picoCTF{0055aabb})


## Solution

Firstly I looked up the main function and saw that it takes one argument and then passes it to the function. Another thing is that in order to see a `win` message the **return value of function needs to be 0**


Function
-----


Then i inspected the function and saw that:
1. Left shift operation is performed - res = 85 << 6
2. division operation - res = res/3
3.  input variable is substracted from res - res = res - input

```
func:
        sub     sp, sp, #32
        str     w0, [sp, 12]  "str -> store register"
        mov     w0, 85        "w0 = 85"
        str     w0, [sp, 16]  "store w0 on sp+16"
        mov     w0, 6
        str     w0, [sp, 20]
        mov     w0, 3
        str     w0, [sp, 24]
        ldr     w0, [sp, 20]
        ldr     w1, [sp, 16]
        "w0 = 85 << 6"
        lsl     w0, w1, w0
        str     w0, [sp, 28]
        "w1 = w0"
        ldr     w1, [sp, 28]
        ldr     w0, [sp, 24]
        "w0 = w1 / 3"
        sdiv    w0, w1, w0
        str     w0, [sp, 28]
        ldr     w1, [sp, 28]
        "w1 = w0"
        ldr     w0, [sp, 12]
        "w0 = w1 - x"
        sub     w0, w1, w0
        str     w0, [sp, 28]
        ldr     w0, [sp, 28]
        add     sp, sp, 32
        ret
```
So the final result was

1. res = 5440
2. res = 1813
3. input = 1813 = 0x715


So the flag:
```
picoCTF{00000715}
```

