# PCBWay RGB Glow Tube DIY Clock

This repository has been created for users like me how bought PCBWay RGB Glow Tube DIY Clock with plenty of options but no software or firmware provided.

After some research I foundn that [one](https://elekstube.com/blogs/news/instructions-on-elekstube-clock-for-gen2-systems) but don't try it, it will just brick your clock.

Tool from @PCBWay:
[here](https://pcbwayfile.s3.us-west-2.amazonaws.com/web/230620/EleksTube%20IPS.V1.1.zip)

Please @PCBWay provide official software to have our clock working as described on your site and be able to configure it.

As I bought 2 clocks, I was able to read back firmware from the working one and flash back the faulty one.

I wasn't able to read more than 1M from esptool (not sure why) but I read firmware on 4 bunch of 1M files since the ESP32 on the clock has 4M

## PCBWay tool
The tool from PCBWay creates the images in the data directory (under esptool) and then creates a spiffs bin file (data.bin) with them. Names as follows. The 0-9.jpg are the DIY images - the other two sets are what comes with the clock. 

Using the tool from PCBway to generate new data.bin files is possible if you rename the path of the directory to not have any unicode in it - at least under Windows 11. The push from the tool to the clock doesn't seem to work, but you can do it manually after the "compile" step.

```shell
esptool.exe --chip esp32 --port COM3  --baud 921600 --before default_reset --after hard_reset write_flash -z --flash_mode dio --flash_freq 40m --flash_size detect 0x290000 bin\data.bin
```

```
./mkspiffs -l Downloads/EleksTube/esptool/bin/data.bin
19405   /0.jpg
45006   /RETRO9.jpg
10970   /1.jpg
15226   /2.jpg
15887   /3.jpg
15080   /4.jpg
18157   /5.jpg
18128   /6.jpg
12108   /7.jpg
18199   /8.jpg
17684   /9.jpg
21904   /PUNK0.jpg
17356   /PUNK1.jpg
23104   /PUNK2.jpg
23625   /PUNK3.jpg
20122   /PUNK4.jpg
44007   /RETRO7.jpg
23189   /PUNK5.jpg
21096   /PUNK6.jpg
18614   /PUNK7.jpg
26364   /PUNK8.jpg
22299   /PUNK9.jpg
47466   /RETRO0.jpg
45183   /RETRO1.jpg
45527   /RETRO8.jpg
45723   /RETRO2.jpg
45781   /RETRO3.jpg
44182   /RETRO4.jpg
44826   /RETRO5.jpg
45104   /RETRO6.jpg
```
## How to flash back

Just download the 4 binary files from here and type the following commands (in the following order)

```shell
 esptool.py -p /dev/tty.usbserial-1320 -b 230400  write_flash 0x300000 flash_4M.bin 
 esptool.py -p /dev/tty.usbserial-1320 -b 230400  write_flash 0x200000 flash_3M.bin 
 esptool.py -p /dev/tty.usbserial-1320 -b 230400  write_flash 0x100000 flash_2M.bin 
 esptool.py -p /dev/tty.usbserial-1320 -b 230400  write_flash 0x000000 flash_1M.bin 
```

PS : You need to change serial port name of course

I've tried to make only one firmware file addind 4 files into one, this is confirmed to work.


```shell
 esptool.py -p /dev/tty.usbserial-1320 -b 230400  write_flash 0x000000 flash_full.bin 
```


Please star this repo if I saved your awesome clock :-)
