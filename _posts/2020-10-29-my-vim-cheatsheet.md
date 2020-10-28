---
layout: post
title: "My Vim Cheatsheet"
date: 2020-10-29 00:45:00 +8
comments: true
categories:
---


I am trying to empower Vim as my primary IDE. But I am not gonna jump straight into it, I will do it step by step. I have to admit that I do not recognize Vim's commands but I will make my self getting used to it. It is all about habit I suppose. My typing speed also not quite fast but hell yeah I am joining the Vim cult!

So in this post I will make my own Vim Cheatsheet. Let's go.

## .vimrc 

Here is my `.vimrc` file default setup. These commands are very useful when writing code.

```
# enable syntax highlighting
syntax enable

# show line number
set number

# set tabspace to 4 spaces
set ts=4

# auto add indent when moving to next line while in insert mode
set autoindent

# shift lines by 4 spaces when using >> or << commands
set shiftwidth=4

# show visual line under cursor's current line
set cursorline

# show matching part of brackets pair
set showmatch
```

## Find string

/<search pattern>

## Find string and replace in the current file

:%s/<search pattern/<replacement>/g

'g' means find from the beginning to the end of file.

## Visual mode

In visual mode we can select multiple lines.

v: Enter visual mode
V: Enter visual mode with current cursor's line selected

## Copy, Cut, Delete, Paste

yy, Y: Copy the current entire line the including newline character at the end of the line<br/>
y: Copy selected area/lines in visual mode <br/>
yiw: Copy current word excluding surrounding spaces
yaw: Copy current word including surrounding spaces
yt(x): Copy from current cursor position until before (x) character
yf(x): COpy from current cursor position until (x) character included
x: Delete character above the cursor
d: Cut or delete selected area/lines in visual mode <br/>
dd: Cut/delete the entire line
dw: Delete the word with trailing blank space. If put in the middle of word, will delete the rest of the word with followed trailing space
P: Paste before cursor
p: Paste after cursor

# Navigation / Go To

0, ^: The beginning of line
$: The end of line
A: The end of line with insert mode
w, W: Move cursor right 1 word
b, B: Move cursor left 1 word
H: Move to the top of the screen
M: Move to the middle of the screen
L: Move to the bottom of the screen
gg: The beginning of file
G: The end of file

## Happy Vim-ing!

This post will be updated if I found or regularly use another command. Cheers!
