# PCBWay RGB Glow Tube DIY Clock

This repository has been created for users like me how bought PCBWay RGB Glow Tube DIY Clock with plenty of options but no software or firmware provided.

After some research I foundn that [one](https://elekstube.com/blogs/news/instructions-on-elekstube-clock-for-gen2-systems) but don't try it, it will just brick your clock.

Please PCBWay provide official software to have our clock working as described on your site and be able to configure it.

As I bought 2 clocks, I was able to read back firmware from the working one and flash back the faulty one.

I wasn't able to read more than 1M from esptool (not sure why) but I read firmware on 4 bunch of 1M files since the ESP32 on the clock has 4M

## How to flash back

Just donwload the 4 binary files from here and type the following commands (change serial port name of course)


```shell
 esptool.py -p /dev/tty.usbserial-1320 -b 230400  write_flash 0x300000 flash_4M.bin 
 esptool.py -p /dev/tty.usbserial-1320 -b 230400  write_flash 0x200000 flash_3M.bin 
 esptool.py -p /dev/tty.usbserial-1320 -b 230400  write_flash 0x100000 flash_2M.bin 
 esptool.py -p /dev/tty.usbserial-1320 -b 230400  write_flash 0x000000 flash_1M.bin 
```

Please star this repo if I saved your awesome clock :-)
