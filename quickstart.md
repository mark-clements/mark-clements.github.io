---
layout: default
title:  Quick starting shell (.sh) scripts
---

# Quick starting shell (.sh) scripts
One small tradeoff with the versatility of Linux is that it needs a little bit of configuration to make it easy to launch scripts without typing the full path. The following is a small guide for one of many ways to address that. (Note, we won't be covering how to make shell (.sh) scripts here.)   

### Setting up a local bin folder    
(1) Check if you already have local bin folder:   

```cd ~/.local/bin```

If you don't, you can create one with:  

```mkdir ~/.local/bin```  

(2) Check if location is already added to the *PATH* variable (some systems do this by default):

``echo $PATH``  

Otherwise, add the folder to your system's PATH variable. We're going to use the echo command to append these to the *.profile* file, though if you prefer you can just edit the file yourself.

```echo 'export PATH=~/bin:$PATH' >> ~/.profile```  

You should now have *~/bin/:*  added to the start of $PATH  

> *Side note*: The *$PATH* variable is one of the default environment variables in linux. It is used by the shell to look for executable files. You can see it by typing *echo $PATH*  

(3) Reload your shell so that it's using this updated *.profile* file:

```source ~/.profile```

### Creating symlinks and making them executable
(4) Create a symlink (shortcut) to the script that you'd like to be able to quickstart:  

```sudo ln -s ~/path/to/my.sh ~/.local/bin```  

This will create a symlink in the local 'bin' folder. Alternatively, you can in certain cases just put the .sh file there directly.

(5) Ensure that your script is executable  

```chmod u-x ~/path/to/my.sh```

(6) Type the name of you bash script on the command prompt. It should now work from any location

**Now that this is setup, you need only do steps 4-5 to add any new links.**

Sources:  
https://unix.stackexchange.com/questions/26047/how-to-correctly-add-a-path-to-path/26059#26059

[Back](./)

