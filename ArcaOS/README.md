# ArcaOS
ArcaOS runs fine once it's installed, but I have not had any success booting the installer in qemu.  
  
I follow the instructions to install in VirtualBox. Afterwards I convert the disk:  
`qemu-img convert -f vdi -O qcow2 ArcaOS.vdi ArcaOS.qcow2`   

Once the disk is converted it boots and works normally with a configuration like the one here. Just replace %%DISK in the domain xml before running virsh define. Graphics, audio, and network all work fine. Using SATA causes problems for me so I use IDE here.

# Links
https://www.arcanoae.com/
https://en.wikipedia.org/wiki/ArcaOS

![screenshot](https://github.com/jmontleon/libvirt-configs/blob/main/ArcaOS/screenshot.png?raw=true)
