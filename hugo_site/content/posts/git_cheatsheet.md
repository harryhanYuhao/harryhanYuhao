---
date: '2025-04-21T12:14:12+01:00'
title: 'Git Cheatsheet'
# weight: 1
tags: ["git"]
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

## Git Commands 

### Multiple remote repositories

```bash
git remote set-url <remote-name> --push --add <url>
```

It seems like whenever this commmand is used, the original `--push` remote is removed. 
The work around is to use this command again and add the original `--push` remote url.

## TODO

h3 for command name seems to be too large.
Find a way to apply custom css only to this page.
h4 seems just write for command name, it does not show in the TOC.
