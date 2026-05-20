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
## Managing Remotes

### Multiple remote repositories

```bash
git remote set-url <remote-name> --push --add <url>
```

It seems like whenever this commmand is used, the original `--push` remote is removed. 
The work around is to use this command again and add the original `--push` remote url.

### Revert pushed commits to remote

This action is _**dangerous!!!**_ Only do it if you understand its consequences.

```
git reset --hard HEAD~7  # reset the local head to 7 commits ago 
git push -f origin HEAD:master  # force the remote head to become local head
```

### Push to different remote branches

Assuming the remote is named `origin`.
The ususal configuration is that the local branch `main` will track the `main` branch of `origin`. 

If there is a new local branch `dev`. 
This command
```
git push -u origin dev
```
will create a new remote branch `dev`, which our local branch `dev` will track.

Forcing the local brach to track a remote branch of a different name can be achieved by
```
git push -u origin <local-branch>:<remote:branch>
```

specifically to set the local branch `dev` to track the remote branch `main` we use

```
git push -u origin dev:main
```

## Git log

### A nice git log format

The following command creates a nice compact view of past git commits 

```
git log --graph --abbrev-commit --decorate --format=format:'%C(bold blue)%h%C(reset) - %C(bold green)(%ar)%C(reset) %C(cyan)%s%C(reset) %C(dim green)- %an%C(reset)%C(auto)%d%C(reset)' --all
```

For a convenient usage, we can set git the following git alias. 
Place the following line in `~/.gitconfig`. Create `~/.gitconfig` if it does not exist.
Now `git lg` will invoke our nice log summary.

```
# ~/.gitconfig
[alias]
    lg = "log --graph --abbrev-commit --decorate --format=format:'%C(bold blue)%h%C(reset) - %C(bold green)(%ar)%C(reset) %C(cyan)%s%C(reset) %C(dim green)- %an%C(reset)%C(auto)%d%C(reset)' --all"
```
