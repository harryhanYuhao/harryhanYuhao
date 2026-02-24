---
date: '2026-02-24T20:47:23+01:00'
title: "Tips on Vscode"
---

I believe mastering the techniques of Vim dramatically increase one's coding efficiency. 
Yet in the meantime Vim runs in a terminal, and persisting to code a in terminal nowadays (time of writing was 2026) seems a little too obstinate, considering so many recent advancements on UI that are too difficult to replicate in a terminal.

I believe Vim mode in VSCode gives a perfect solution.

## Vim Mode in VSCode

The Vim hotkeys may collide with VSCode hotkeys. 
I recommend to ignore certain vim hotkeys by adding the following into `settings.json` (which can be opened by search for User Setting in VSCode)

```json
"vim.handleKeys": {
    "<C-s>": false,
    "<C-f>": false,
    "<C-p>": false,
    "<C-v>": false,
    "<C-c>": false
}
```

