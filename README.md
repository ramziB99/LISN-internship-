# Data collection based on radio signal strength analysis 
## PiSDR
The PiSDR is a Raspbian based operating system for the Pi pre-loaded with multiple Software Defined Radio software. It was created to serve as a fast and reliable bootstrap for SDR projects.  
There is a few steps to follow in order to install PiSDR :  
1. install the PI imager that suits your OS available in https://www.raspberrypi.org/software/
2. Download the version 5.0 (latest for now) of PiSDR available in https://github.com/luigifcruz/pisdr-image/releases/tag/v5.0.0 as an img file (1.5gb), provide at least 10gb of space in your hard drive.  
3. Insert the SD card (at least 16gb) in your computer, open the PI imager and select the SD card as device and the PiSDR img that you previously download as an OS.  

Since Wireshark is not included in the softwares pre-loaded in the PiSDR you will have to download it by typing the following commands :   
```
$ sudo apt-get update && sudo apt-get upgrade -y
$ sudo apt-get install wireshark 
```
For the permission configuration you will have to execite the following steps: 
```
$ sudo groupadd wireshark
$ sudo usermod -a -G wireshark pi
$ sudo chgrp wireshark /usr/bin/dumpcap
$ sudo chmod 750 /usr/bin/dumpcap
$ sudo setcap cap_net_raw,cap_net_admin=eip /usr/bin/dumpcap
```
After completing those steps you should reboot and run your raspberry pi. 
