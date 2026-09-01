# [extensions] - PicoCTF [2019]

**Category:** Forensics 
**Difficulty:** Medium 

--- 

## Description 

This is a really weird text file. Can you find the flag?

flag.txt

--- 

## Analysis 

After downloading the file and trying to open it, the content was unreadable. So I used the `file` command to check its magic bytes and discovered it was actually a PNG image — its extension had been changed to `.txt`, which is why it couldn't be opened normally.

```bash
file flag.txt 
```

![alt text](image.png)

---

## Solutions 

Since the extension was wrong, I used `mv` to rename it to the correct type. After that, opening the renamed file revealed the flag.

```bash
mv flag.txt flag.png
```
![alt text](image-1.png)

---

## Flag!

picoCTF{now_you_know_about_extensions}

---

## Takeaways

- **Extension Spoofing** — A file's extension (`.txt`, `.jpg`, etc.) is just a label in the filename and does not determine the actual file format. The real format is defined by the **magic bytes** (file signature): a fixed sequence of bytes at the beginning of the file that identifies its true type. Attackers (and CTF challenges) often rename files to mislead tools or users.

- **`file` command** — Reads the magic bytes of a file and reports its true format, regardless of its extension. Always run this when a file behaves unexpectedly.
  ```bash
  file flag.txt
  # Output: flag.txt: PNG image data, ...
  ```

- **`mv` command** — Used to rename or move files. In this case, renaming the file to the correct extension allowed the OS to open it properly.
  ```bash
  mv flag.txt flag.png
  ```
