# Libvirt Configs
Libvirt domain examples. Especially for less typical operating systems.

- [AmigaOS](AmigaOS/README.md)
- [ArcaOS](ArcaOS/README.md)
- [Debian Hurd](Debian-Hurd/README.md)
- [Haiku](Haiku/README.md)

In most cases I prefer to use qcow2 images, and in the linked examples direct you to create your own and replace the path in the domain XML. To create a new one for any example you can run, for example: `qemu-img create -f qcow2 disk.qcow2 128G`. A typical place to do this when using `qemu:///session` is `~/.local/share/libvirt/images`. For `qemu:///system` `/var/lib/libvirt/images/` is typical.
  
Preallocation options like `-o preallocation=metadata` or `-o preallocation=falloc` may provide some performance improvement, but can also have ramifications for backup scenarios (rsync'ing 'large' sparse files depending on the situation can take a long time), so you'll want to decide what works best for you.
