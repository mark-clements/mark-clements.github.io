---
layout: default
title: z tool, better than cd?
---

Linux offers some versatile tools which can save you a lot of time. Here is a short list of my favorites.   

### 'Z' File Explorer
*Makes it trivial to jump to your most visited file directories in just a couple of key presses. It uses Frecency (sic) to try to get more intelligent in what it proposes, though it takes some time to build up a historic.

Installation steps:  

1. Download the script to your home folder:
```wget https://raw.githubusercontent.com/rupa/z/master/z.sh -O ~/z.sh```
2. Add to .bashrc for ease-of-use:
```sudo ln -s ~/bin/z.sh /usr/local/bin/z```
3. Make sure the script is executable
``` chmod u+x z.sh```
4. Open the terminal and cd to some of your most commonly used directories, for example:
```cd /some/very/long/path/i/keep/typing/here```
5. Now try typing:
```z here```

z should now autocomplete your full path for you! Learn more at the [Project home:] (https://github.com/rupa/z)

[back](./)


