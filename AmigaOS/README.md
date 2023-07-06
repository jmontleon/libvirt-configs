# AmigaOS 4.1

## Usage
These instructions are adapted from:  
https://www.amiga-news.de/en/news/AN-2023-04-00086-EN.html  

It will be necessary to generate a custom ISO as described in the page linked above, have available the pegasos2 rom, etc.  
  
You will also need to have QEMU 8 installed. For Fedora 38 this was as simple as rebuilding the source package for Fedora 39 and updating.  
  
Once these files are available, update %%ROM, %%DISK, and %%ISO in the domain file, AmigaOS.xml with values that make sense for your environment.  
  
If you take a few minutes to look at the config you may notice several strange things. For a bochs GPU is defined. Then it is overridden later. This is due to libvirt not recognizing the SM501 GPU and will not allow us to define it properly. There is also an additional sound card configured. It's not actually used, but as far as I can tell libvirt will not properly configure audio so that it is played to the sound server unless there is a soundcard it recognizes configured.  

Pegasos 2, as mentioned in the page above requires you to enter `boot hd:0 amigaboot.of` on the serial console every time you'd like to boot your system. If you don't want to do this you can set up the qemu hook, which should be located at /etc/libvirt/hooks/qemu and be user executable, a user service which can be placed in ~/.local/share/systemd/user, and an expect script you can place in /usr/local/bin or elsewhere; just ensure the service file to match. With this setup AmigaOS boots without user intervention. The instructions linked for install on the page above direct you to create a boot partition, but this did not seem necessary.

On first boot I had corrupted graphics similar to what's described here. I just made my way to prefs as described and chose a resolution to fix it.  
http://zero.eik.bme.hu/~balaton/qemu/amiga/aos_lowres_mode.html  
  
For audio I just went to AHI in Prefs, selected `Unit 0` from the drop down that says `Music unit` and selected `VIA-AC97: 16-bit stereo++` and from then on sound worked.  
  
For network I just selected the rtl8139 driver and configured it to use DHCP.

![img]screenshot[/img](https://github.com/jmontleon/libvirt-configs/blob/main/AmigaOS/screenshot.png?raw=true)
