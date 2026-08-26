# [GloryoftheGarden] - PicoCTF [2019]

**Category:** Forensics 
**Difficulty:** Easy 

--- 

## Description 

This file contains more than it seems

Attachments: garden.jpg

--- 

## Analysis 

The attachment is a JPEG file. My first approach was to check for readable strings embedded in the binary by using the `cat` for the raw content but most of the output was unreadable binary characters.
---

## Soultions 

Use `strings + grep` to extract the human-readable text specifically start with `picoCTF`.
```bash
strings garden.jpg | grep -i "picoCTF" 
```

---

## Flag
picoCTF{more_than_m33ts_the_3y395e12915}

---

## Takeaways 

- Data can be hidden by appending text after a valid image file, the image still opens normally but carries extra content. 
- And `strings` is the fastest way to find readable text in an binary file. 