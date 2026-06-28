---
date: '2025-05-04T07:54:12+01:00'
title: 'Fancy Terminal'
# weight: 1
tags: ["terminal", "ascii"]
showToc: true
TocOpen: false
hidemeta: false
comments: false
# description: "
# canonicalURL: "https://canonical.url/to/page"
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
ShowWordCount: true
ShowRssButtonInSectionTermList: true
UseHugoToc: true
---

## Graphics in the Terminal

If terminal leaves you an impression of dullness, black-and-white, and text-only, your impression may be wrong.
Terminal is capable of producing surprisingly smooth, user-friendly, and graphical interface.
Check [cmatrix](https://github.com/abishekvashok/cmatrix), [btop](https://github.com/aristocratos/btop), [cava](https://github.com/karlstav/cava) , and, may be most astounding of all, the [spinning doughnut](https://www.a1k0n.net/2011/07/20/donut-math.html).

Most of these are achieved by exploiting ANSI escaped sequence and termios POSIX standards.

This post is a short summary of common functionalities. 
For more, check [Wikipeida](https://en.wikipedia.org/wiki/ANSI_escape_code) and termios man page.

### The Escape Codes

In C, python, or other common programming language, you may use `"\n"` to denote newline character. 
The backslash 'escaped' the following `n`, telling the programming language to interprete it as an escaped character.

In terminal, single byte escape is achieved by `\`. 
Usually it is used to print ASCII characters.
ASCII is a standards that assigns raw one byte binary code, 0 to 255 in decimal, to common letters. Bell has code 07, `i` has 69. Both in hexadecimal.

```bash
echo -e "\x07"  # bell. -e flag tells echo to interpret escape sequence
echo -e "\x69"  # i
```

More complicated tasks are achieved by escaping more than one byte of data with `\x1b`. 27, which in hexadecimal is `1b`, is the ascii code for `ESC`.

This line will print red texts in the terminal
```bash
echo -e "\x1b[31mRed Text!\x1b[0m"   # -e flag enable escape sequences
```

`\x1b` is the escape sequence, `\x1b[` is the so called control sequence introducer (CSI). 
`\x1b[` with codos following it sends command to the terminal. 

Here, `\x1b[31m` tells the terminal to print red texts. `\x1b[0m` resets the color. 
If no `\x1b[0m` is issued, the terminal will continue to print red.

### A Short History of Terminal 

Most of the standards of terminal mentioned above are product of the legacy.
When computers were first invented, they are exclusively used by the government and coorporations (first personal computer was invented in 1970s). 
Terminal back then was the physical device to an end user uses to communicate with central computer. 
Thus comes the name terminal.

Initially terminals were solely black and white. 
Vendors of the terminals graduately introduced different functionalities, like coloring, and made standards on how to control these extra functionality. 
At that time the computer technologies were still in its infancy (mouse was not invented yet), and naturally all of these extra functionalities were controled directly by user input via escape sequences.
The escape sequences introduced above were were widely adopted and made into ISO standard 6429.

No one uses physical terminal today. 
Most mordern operation system feature exclusively graphical user interface (GUI). 
Yet, many still find terminal useful in certain circumstances, especially in coding.
The terminals in modern operating system are virtual terminals, which one application software out of many in a modern computer.
Virtual terminals imitate the behaviours of physical terminals and adhere to the various standards governing them.
