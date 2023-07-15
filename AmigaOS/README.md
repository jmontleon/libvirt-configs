# AmigaOS 4.1

These instructions are adapted from:  
https://www.amiga-news.de/en/news/AN-2023-04-00086-EN.html  

It will be necessary to generate a custom ISO and gather the pegasos2 rom as described on the page above.  
  
You will also need to have QEMU 8 installed. Additionally, QEMU 8.1 fixes a shutdown bug. AmigaOS uses PPC emulation so ensure you have qemu-system-ppc installed.  
  
Once these files are available, update `%%ROM`, `%%DISK`, and `%%ISO` in the domain file, `AmigaOS.xml`, with values that make sense for your environment.  
  
If you take a few minutes to look at the config you may notice several strange things. First a bochs GPU is defined. Then it is overridden later. This is due to libvirt not recognizing the SM501 GPU and will not allow us to define it properly. There is also an additional sound card configured. It is not actually used by AmigaOS, but as far as I can tell libvirt will not properly configure audio so that it is played to the sound server unless there is a soundcard it recognizes configured. There are also many unsupported options we provide by the qemu command line.  
  
Technically none of the following is required, however as mentioned in the page above Pegasos 2 emulation requires you to enter `boot hd:0 amigaboot.of` on the serial console every time you want to boot. If you don't want to do this you can set up the qemu hook by copying it to `/etc/libvirt/hook/qemu` and ensuring it is executable. Then a user systemd service example is provided which can be placed in `~/.local/share/systemd/user` after which you should run `systemctl --user daemon-reload`. And finally an expect script you can place in `/usr/local/bin`. If placed elsewhere just ensure the service file matches and reload the daemon after editing it. The expect script will require expect to be installed to run as well. With this setup AmigaOS boots without user intervention.  
  
Some things I noted during install and initial setup:
- The instructions linked for install on the page above direct you to create a boot partition, but this did not seem necessary.
- On first boot I had corrupted graphics similar to what's described here. I just made my way to prefs as described and chose a resolution to fix it.  
http://zero.eik.bme.hu/~balaton/qemu/amiga/aos_lowres_mode.html  
- For audio I had to open AHI in Prefs, selected `Unit 0` from the drop down that says `Music unit` and selected `VIA-AC97: 16-bit stereo++` to get audio to work.
- For network I just selected the rtl8139 driver and configured it to use DHCP.
- RAM is currently limited to 1GB.
- Some SDL applications don't display correctly. Switching to the g3 processor from 7447 can work around this.

# Links
https://www.hyperion-entertainment.com/  
https://en.wikipedia.org/wiki/AmigaOS_4  
  
![screenshot](https://github.com/jmontleon/libvirt-configs/blob/main/AmigaOS/screenshot.png?raw=true)
