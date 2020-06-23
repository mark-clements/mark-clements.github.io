---
layout: default
title: Updating Linux Kernel
---

# Reverting / upgrading Linux Kernel 
If you decide to upgrade from the default 'nouveau' open source drivers, to one of the proprietary Nvidia versions (430, 435 etc), you can run into conflicts with the kernel. If after doing this, you find your system's suddenly unstable there's a few things worth trying. Below is a a short guide on how to change your kernel, now that Ukuu is no longer free. Caveat emptor... use at your own risk.   

### 1. Find the Complete Name of the Version You Want

```apt-cache search --names-only linux-image | grep -v unsigned | grep generic```  

*Here we've filtered out unsigned drivers, and looked for 'generic' drivers.*

*The package name of the kernel is linux-image- followed by the version, like linux-image-4.4.0-21-generic. The associated headers file for a kernel has the same package name with image replaced by headers*

### 2. Install driver and header file
```sudo apt-get install linux-image-5.0.0-44-generic linux-headers-5.0.0-44-generic```

### 3. Modify the bootloader (grub) to use the new kernel by default
1. Find the $menuentry_id_option for the submenu:  
```grep submenu /boot/grub/grub.cfg```

2. Find the $menuentry_id_option for the menu entry for the kernel you want to use:  
```grep gnulinux /boot/grub/grub.cfg```

3. Comment out your current default grub in /etc/default/grub and replace it with the sub-menu's $menuentry_id_option from step one, and the selected kernel's $menuentry_id_option from step two separated by >

e.g. in my case these were:  
Comments out original line: ```#GRUB_DEFAULT=0```  
Add new line: ``` GRUB_DEFAULT="gnulinux-advanced-462c8c72-e1e1-4f65-a1ce-fd4fdee4644b>gnulinux-5.0.0-44-generic-advanced-462c8c72-e1e1-4f65-a1ce-fd4fdee4644b"```

4. Update grub
```sudo update-grub```

### 4. Reboot

### 5. Verify Which Kernel you Booted into (by default)
```uname -a```

Original sources:  
https://www.digitalocean.com/docs/droplets/how-to/kernel/use-non-default/
https://unix.stackexchange.com/questions/198003/set-default-kernel-in-grub


[Back](./)
