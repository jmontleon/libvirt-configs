# FreeBSD
FreeBSD can use a pretty standard configuration.  
  
Replace %%DISK with a disk location that makes sense for your environment and install.  

The mouse may not work well until you install additional packages:    
`pkg install utouch-kmod xf86-input-evdev`  
  
Then add `utouch_load=YES` in `/boot/loader.conf`
VirtIO drivers can also be loaded here.
```
utouch_load="YES"
virtio_load="YES"
virtio_pci_load="YES"
virtio_balloon_load="YES"
virtio_blk_load="YES"
virtio_console_load="YES"
virtio_random_load="YES"
if_vtnet_load="YES"
```
  
# Links
https://www.freebsd.org/  
https://en.wikipedia.org/wiki/FreeBSD  
  
![screenshot](https://github.com/jmontleon/libvirt-configs/blob/main/FreeBSD/screenshot.png?raw=true)
