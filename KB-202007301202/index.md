---
title: Compare two folders' contents in Terminal
zid: KB-2007301202
tags:
- cli
- terminal
- mac
---

#### by Rob Griffiths, [www.macworld.com](https://www.macworld.com/article/1132219/termfoldercomp.html) ▪ Friday, February 22, 2008, 12:00 AM

Have you ever wanted a quick way to compare two directories (folders), in order to see which files may differ between the two? Back in 2006, [we discussed FileMerge](http://www.macworld.com/article/49584/2006/03/cmpfldr.html) (part of Apple’s Xcode developer tools), which can do just that. There are other third-party GUI tools as well, but there’s actually a free folder comparison tool built into every Mac—it just requires a quick trip to Terminal to put it to use. The program is called `diff`, and it’s quite simple to use.

Launch Terminal (in Applications -> Utilities), and then use the cd command to change to the directory containing the folders you’d like to compare. (The folders can be located anywhere, of course, but it’s easiest if they’re in the same folder.). Once there, just run this command:

diff -rq folder1 folder2

This is a pretty simple command, with two command-line switches (`-rq`). The `r` tells `diff` to look at each directory recursively, including subdirectories. The `q` switch sets `diff` brief mode. If we didn’t set brief mode, `diff` would not only tell you which files are different between the two folders, but also show the actual line-by-line differences for any text files that exist in both locations but are not identical. Given that we’re just interested in comparing the folders’ contents, we don’t need that level of detail, so we’ll use brief mode to suppress it. And that’s all there is to it. Here’s how it looks in action:

$ cd phpcode
$ diff -rq comments\_new comments\_old
Only in comments\_new: config.php
Only in comments\_old: config\_old.php
Only in comments\_old: functions.inc

Obviously, this is a simplistic example, but it works just as well on a large folder with hundreds of files. If you want to do more with `diff`, of course, it’s capable of much more than just simple folder comparisons; type `man diff` to read about its full capabilities.

Note: When you purchase something after clicking links in our articles, we may earn a small commission. Read our [affiliate link policy](https://www.macworld.com/about/affiliates.html) for more details.

---

Clipped on Friday, July 31, 2020, 12:02 PM