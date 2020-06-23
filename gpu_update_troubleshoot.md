## Ubuntu boot troubleshooting

#### Stuck after bootload with message "loading RAMDISK"
Did you recently update a Nvidia GPU driver? If so try reinstalling the driver.

Preliminary steps: 

- On Grub bootloader select 'Advanced
- Select the recovery mode version of your existing Linux kernel (the one below)
- On the menu drop to root and try the following steps:


> sudo apt purge nvidia-*
> sudo apt autoremove


#### Reinstall driver
Check which drivers are available:
> sudo ubuntu-drivers devices

sudo apt install nvidia-driver-<number>
Check the card is selected:
> prime-select query 

If it doesn't say nvidia, and your system has a integrated graphics intel PSU, you can swap to the nvidia profile with the command:  
> sudo prime-select nvidia
(or sudo prime-select intel)

Restart machine
> sudo shutdown -r now
(Cross your fingers)

If your machine succesfully boots you can confirm which driver is now in use with:
> sudo lshw -c display

This should say nvidia)

[sources](https://www.linuxbabe.com/ubuntu/install-nvidia-driver-ubuntu-18-04)


