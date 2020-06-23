## Machine will only booot with charger (AC) connected
Try adding kernel parameters :  

- Open the file at the location below with your editor of choice, e.g.:  
> vi /etc/default/grub

Edit the end of thhe line *GRUB_CMDLINE_LINUX_DEFAULT="quiet splash dis_ucode_ldr"*

Then  
>sudo update-grub

Restart machine
> sudo shutdown -r now

Cross your fingers.
