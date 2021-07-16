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

## WIFI packets capture using LimeSDR 
In this part we will use gr-802-11 — a GNU Radio based OFDM transceiver for IEEE 802.11a/g/p networks — can be used with the LimeSDR Usb to observe and record Wi-Fi signals.  
The Wi-Fi signal is captured to a file which can then subsequently be read by the popular network protocol analyser, Wireshark. The benefits of using an SDR with Wireshark instead of 802.11 hardware include that you don’t need to worry about whether your WLAN adapter is filtering packets, and of course you’re free to modify the physical layer since it’s software.  
The instructions to download the gr-ieee802-11 are available in https://github.com/bastibl/gr-ieee802-11.  
After correctly following the instructions by installing all the necessary packages and ressources, you should lanch GNU radio companion and open the wifi_rx.grc which is a flowgraph that allow us to capture wifi packets using several sources ( osmocom source, limeSDR , UHD ...). Since we are using LimeSDR you should replace the UHD source with the LimeSDR source (RX) which is available in the GNU radio companion block and to do the following changes :  
* put "freq" as frequency and "samp_rate" as Sample rate 
* Set the LNA path to auto for the channel A and select it 
* modify the default value of freq in the QT GUI Chooser and set it to 2.412G instead of 5G 
* Enable the wireshark blocks 

You can fin the modified flowgraph in the repo as Wifi_rx.grc.  
To start the wifi packets capture, you have to connect the limeSDR usb to the raspberry PI and then execute a script wich is available in the gr-ieee802.11 file  which will lanch the wifi_rx and open a wireshark window at the same time. You should tune the gnu radio companion to capture packets in a particular frequency channel or sample rate, constelations will appear if packets are captured.


