# omxplayer-sync_withNOOBS_forNOOBS
## a guide in setting up multiple Raspberry Pi's to play a video (or video's) synchronized with omxplayer

### Our RasPi will start up from NOOBS
* [Download NOOBS](https://www.raspberrypi.org/downloads/noobs/)
* Extract the zip
* Add the content of the zip-file to the microSD-card for the Raspberry Pi
* Make sure it’s not in a folder on the SD-card
* Put the SD-card in the Pi
* Power up the Pi
* Select the rasbian install
* Install rasbian 

### Set-up omxplayer sync
* Run Raspbian in desktop mode
* Open the terminal
* Give following commands:

`sudo apt-get install libpcre3 fonts-freefont-ttf fbset libssh-4 python3-dbus`
`sudo wget -O /usr/bin/omxplayer-sync https://github.com/turingmachine/omxplayer-sync/raw/master/omxplayer-sync`
`sudo chmod 0755 /usr/bin/omxplayer-sync`
`sudo wget https://github.com/turingmachine/omxplayer-sync/raw/master/synctest.mp4`

### Give the Pi's Static IP-adresses
* Right mouse click on the wifi-symbol
* Wireless & Wired Network Settings
* Interface//eth0
* Disable IPv6
* IPv4: 192.168.0.10/24
*the next pi should be: 192.168.0.11/24*
*the next one: 192.168.0.12/24*
*etc*
* Router: 192.168.0.1 [The same for every pi]
* DNS Servers: 192.168.0.1 [The same for every pi]

### Give more Performance-Powwah
* Click on the berry (upper left corner)
* Click on preferences
* Raspberry Pi Configuration
* Click on the tab Performance
* Set GPU Memory to 256

### Shut down the Raspberry Pi’s

### Test the omxplayer-sync
* Set everything up except the power; Ethernet-cable, usb, hdmi, …
* Power the Pi’s
* Open the terminal
* start the master

`omxplayer-sync -muv synctest.mp4`
* start the slave(s)

`omxplayer-sync -luv synctest.mp4`

### Play files from USB-sticks
* Power the pi's
* Open the terminal an type:

`omxplayer-sync -muv -b local /media/pi/NameOfYourUSB/NameOfYourMovie.mp4`
* Press enter
* Open the terminal on the other (slave) Pi’s an type:

`omxplayer-sync -luv -b local /media/pi/NameOfYourUSB/NameOfYourMovie.mp4`
* Press enter

### Sit back and enjoy your synchronized screens

## To Know
* Every video is to be created in mp4 with the H264 codec
* Every video needs exactly the same length!
* Every USB-disk needs exactly the same name!
* Every videofile needs exactly the same name!
* An ethernet(RJ45) cable must be connected before you start the master, otherwise it will not send sync data to the slave(s).
* Use videos which are min. 60 seconds or longer. It takes some time to sync.

## Options:
``
-h, --help            show this help message and exit

-m, --master          

-l, --slave           

-x DESTINATION, --destination=DESTINATION

-u, --loop            

-v, --verbose         

-o ADEV, --adev=ADEV  

-a ASPECT, --aspect=ASPECT  Aspect Mode - fill, letterbox, stretch``

## see [here](https://github.com/theBlackBoxSociety/omxplayer-sync) for more
