# [Information] - PicoCTF [2021]

** Category: Forensics 
** Difficulty: Easy 

--- 

## Description 

Files can always be changed in a secret way. Can you find the flag? 

Attachments: cat.jpg 

--- 

## Analysis 

- The attachment is a JPEG file. My first approach was to check 
for readable strings embedded in the binary:
``` bash
strings cat.jpg | grep -i "picoCTF" 
```
=> So the reason why I use this command because it helps to find the text that human can read (Every files like music, pictures usually saved as binary code).
The strings command help extract and display the human-readable strings. Beside the "grep" command search for the keywords that I want to find.  
=> But it just return null so I try another methods 

---

## Soultions 

- Using the command: 
``` bash
exiftool cat.jpg
```
=> Reason: exiftool is a tool just for read and write the Metadata (EXIF) that dip into the structure of the file. 

**What is EXIF metadata?**  
Metadata is embedded data that describes a file — camera model, 
date, location, copyright info, etc. It's stored inside the file 
structure but not visible when you open the image normally.

=> Output: The `License` field contained a suspicious string:
cGljb0NURnt0aGVfbTN0YWRhdGFfMXNfbW9kaWZpZWR9

This looks like Base64. Decoded it with:
```bash
$ echo "cGljb0NURnt0aGVfbTN0YWRhdGFfMXNfbW9kaWZpZWR9" | base64 -d
```
---

## Flag
=> It gaves me the output "picoCTF{the_m3tadata_1s_modified}" and it is the correct answer.

---

## Takeaways 

- Knows about the Metadata (What is means, What is about and What is include) => and the command to read the Metadata of a file. 
- The `license` and the `comment`, `copyright` in Metadata of the file sometimes is the place to hind the flag.
- When `strings + grep` fails, go deeper into file structure with
tools like `exiftool` or `binwalk`.