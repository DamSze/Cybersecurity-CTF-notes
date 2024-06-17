# CTF Name: CanYouSee

## Challenge Description

How about some hide and seek? Download this file here. 

## Solution

Let's see the .jpg:

![ukn_reality.jpg](/picoCTF/CanYouSee/resources/ukn_reality.jpg)

At the first glance we can't see anything special

Let's dive in deeper

Firtsly i run it through the `exiftool`

```
ExifTool Version Number         : 12.40
File Name                       : ukn_reality.jpg
Directory                       : .
File Size                       : 2.2 MiB
File Modification Date/Time     : 2024:03:12 00:05:57+00:00
File Access Date/Time           : 2024:06:17 10:02:56+00:00
File Inode Change Date/Time     : 2024:06:17 10:02:11+00:00
File Permissions                : -rw-r--r--
File Type                       : JPEG
File Type Extension             : jpg
MIME Type                       : image/jpeg
JFIF Version                    : 1.01
Resolution Unit                 : inches
X Resolution                    : 72
Y Resolution                    : 72
XMP Toolkit                     : Image::ExifTool 11.88
Attribution URL                 : cGljb0NURntNRTc0RDQ3QV9ISUREM05fZDhjMzgxZmR9Cg==
Image Width                     : 4308
Image Height                    : 2875
Encoding Process                : Baseline DCT, Huffman coding
Bits Per Sample                 : 8
Color Components                : 3
Y Cb Cr Sub Sampling            : YCbCr4:2:0 (2 2)
Image Size                      : 4308x2875
Megapixels                      : 12.4

```

Attribution URL looks like UTF-8 encoded text, let's try that:
```
mordzio-picoctf@webshell:~$ echo "cGljb0NURntNRTc0RDQ3QV9ISUREM05fZDhjMzgxZmR9Cg==" | base64 -d
picoCTF{ME74D47A_HIDD3N_d8c381fd}
```

And there's the flag :)