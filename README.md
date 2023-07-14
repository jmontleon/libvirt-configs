# Libvirt Configs
Libvirt domain examples. Especially for less typical operating systems. Have some fun, try something new, and learn something different.

| OS  | Free | Video | Network | Audio |
|---|---|---|---|---|
| [AmigaOS](AmigaOS/README.md) | :x: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: |
| [ArcaOS](ArcaOS/README.md) | :x: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: |
| [Debian Hurd](Debian-Hurd/README.md) | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :x: |
| [FreeBSD](FreeBSD/README.md) | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark:
| [Haiku](Haiku/README.md) | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: |
| [MorphOS](MorphOS/README.md) | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: |

# Creating a disk image
In most cases I prefer to use qcow2 images, and in the linked examples direct you to create your own and replace the path in the domain XML. To create a new one for any example you can run, for example: `qemu-img create -f qcow2 disk.qcow2 128G`.

A typical place to do this when using `qemu:///session` is `~/.local/share/libvirt/images`. For `qemu:///system` `/var/lib/libvirt/images/` is typical.

Preallocation options like `-o preallocation=metadata` or `-o preallocation=falloc` may provide some performance improvement, but can also have ramifications for backup scenarios (rsync'ing 'large' sparse files depending on the situation can take a long time), so you'll want to decide what works best for you.

# Manipulating the CD-ROM drive
Many of the examples include a line in the config, such as:  
`    <qemu:arg value='if=ide,bus=1,media=cdrom,file=%%ISO'/>`  
  
During install it's generally easier to just replace %%ISO with the path to the install iso. Afterward though the line can be changed to:  
`    <qemu:arg value='if=ide,bus=1,media=cdrom'/>`  
  
If you want to insert an ISO using AmigaOS as an example run:  
`virsh qemu-monitor-command --domain AmigaOS --hmp change ide1-cd0 updates.iso`  

Later if you want to eject it:  
`virsh qemu-monitor-command --domain AmigaOS --hmp eject ide1-cd0`
