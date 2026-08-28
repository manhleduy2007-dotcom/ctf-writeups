# [SleuthkitIntro] - PicoCTF [2022]

**Category:** Forensics 
**Difficulty:** Medium 

--- 

## Description 

Download the disk image and use `mmls` on it to find the size of the Linux partition. Connect to the remote checker service to check your answer and get the flag.

Download disk image : disk.img.gz 

--- 

## Analysis 

First I realize the file disk.img.gz is the combination between two popular file format: disk image and Gzip compression standard. Inside the archive is raw disk image file (disk.img), so I extracted it using `gunzip`.
``` bash
gunzip -c disk.img.gz > disk.img
```

Second I connect the remote check service by using the command nc 
```bash
nc saturn.picoctf.net 57571
```

---

## Solutions 

Use `mmls` for the disk.img to display the partition layout of the disk image. The partition layout provides specifically such as: Start, End, Description (count in sector) of each layout.

```
DOS Partition Table
Offset Sector: 0
Units are in 512-byte sectors

     Slot      Start        End          Length       Description
000: Meta      0000000000   0000000000   0000000001   Primary Table (#0)
001: -------   0000000000   0000002047   0000002048   Unallocated
002: 000:000   0000002048   0000204799   0000202752   Linux (0x83)
```

When I connect with server, I receive a question: 
```
What is the size of the Linux partition in the given disk image
Length in sectors:
```

So 002 stands for Linux partition and Length is 202752. That the answer for the Length in sectors. Enter it and receive the flag 


---

## Flag

picoCTF{mm15_f7w!}

---

## Takeaways 

- **TSK (The Sleuth Kit)** is the digital forensic toolkit, often use to analyse disk image in CTF Forensic and investigate incident in real world. 

- **mmls** is a command in TSK use for listing partition table of a disk image. Output of each partition: `Slot`, `Start`, `End`, `Length` (count in sector) and `Description`. 

- **Sector** is the base storage unit on a disk (typically 512 bytes). `mmls` counts in sectors by default, so always check the unit before submitting an answer.

- **Gzip (`.gz`)** is a common compression format on Linux. A `.img.gz` file is simply a compressed disk image — always decompress first with `gunzip` before running any disk forensics tool on it.
