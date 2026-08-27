# [Enhance!] - PicoCTF [2019]

**Category:** Forensics 
**Difficulty:** Medium 

--- 

## Description 

Download this image file and find the flag

Attachments: drawing.flag.svg 

--- 

## Analysis 

The attachment is a SVG file. Because is the SVG file so I use `cat` to read the data and realize many tspan split the characters of the flag. 
---

## Solutions 

I decide to write an script in Python just to graft all of the characters in the tspan into a text. The order in the file may not be sequential, so sorting by ID is necessary to reconstruct the correct flag.
``` python
import re
data = open('drawing.flag.svg').read()
parts = re.findall(r'id=\"tspan(\d+)\">([^<]+)', data)
parts.sort(key=lambda x: int(x[0]))
print(''.join(p[1].strip() for p in parts))
```

---

## Flag
picoCTF{3nh4nc3d_24374675}

---

## Takeaways 

- SVG is XML-based, so we can read the file in plain text.
- `grep` PCRE on Linux does not support variable-length lookbehind — use Python regex instead.
- Flag can be hidden by splitting characters across multiple XML elements.