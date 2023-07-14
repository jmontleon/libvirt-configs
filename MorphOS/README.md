# MorphOS

These instructions are adapted from:  
https://www.amiga-news.de/en/news/AN-2023-04-00086-EN.html  
  
MorphOS is free to use in a VM but it will start to slow down after 30 minutes and become unusable after some time. It is not possible to register MorphOS from within a VM.  

For audio and network to work you must use QEMU 8+. To resolve a shutdown issue you must use 8.1+. Networking will initially be broken until a workaround is implemented post-install.
  
Once these files are available, update `%%ROM`, `%%DISK`, and `%%ISO` in the domain file, `MorphOS.xml`, with values that make sense for your environment.  
  
If you take a few minutes to look at the config you may notice several strange things. First a bochs GPU is defined. Then it is overridden later. This is due to libvirt not recognizing the ati-vga GPU and will not allow us to define it properly. There is also an additional sound card configured. It is not actually used by AmigaOS, but as far as I can tell libvirt will not properly configure audio so that it is played to the sound server unless there is a soundcard it recognizes configured. There are also many unsupported options we provide by the qemu command line.  MorphOS benefits from adding a USB mouse nad keyboard in some cases. On my desktop the mouse would stutter incessantly, while on my laptop it did not. Adding it doesn't hurt anything either way though.

To work around the broken networking move `SYS:MorphOS/Devs/AudioModes/PEGASOS` somewhere else. I moved it to `Work:PEGASOS`. If you now reboot networking should work, but now audio is broken. To get audio functioning again modify SYS:S/user-startup and add a line to run another script:
```
RUN >NIL: EXECUTE Work:start-ahi
```

And then add `Work:start-ahi` and mark it executable.
```
wait 30
AddAudioModes Files Work:PEGASOS
```

If all goes well after rebooting you should find that both audio and networking work.  
  
Technically none of the following is required, however as mentioned in the page above Pegasos 2 emulation requires you to enter `boot hd:0 boot.img` on the serial console every time you want to boot. If you don't want to do this you can set up the qemu hook by copying it to `/etc/libvirt/hook/qemu` and ensuring it is executable. Then a user systemd service example is provided which can be placed in `~/.local/share/systemd/user` after which you should run `systemctl --user daemon-reload`. And finally an expect script you can place in `/usr/local/bin`. If placed elsewhere just ensure the service file matches and reload the daemon after editing it. The expect script will require expect to be installed to run as well. With this setup AmigaOS boots without user intervention. 
  
# Links
https://www.morphos-team.net/  
https://en.wikipedia.org/wiki/MorphOS
  
![screenshot](https://github.com/jmontleon/libvirt-configs/blob/main/MorphOS/screenshot.png?raw=true)
