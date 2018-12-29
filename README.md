# kaipod2
Networked music player for kids
## kaipod 2.0
This is a project I did to build a networked portable radio for my 4 year old son. I had previously built a simple radio using an arduino UNO and a MP3 shield, housed in a wooden enclosrue I also made. The aim was to make an easy to use music player that was solidly built. I was not happy with the offerings of MP3 radios for kids which were either too complicated, ugly, or cheaply made. Also many of them included a microphone permanently attached, however not all kids want to sing along. I have not documented that build and it has been a couple of years but I may go back and document it as the radio is still in heavy use. The issue is that my 4 year old's 2 year old brother has taken over the radio. Its simple and sturdy design makes it easy for my 2 year old to operate and abuse. 
So now it was time to upgrade my oldest son. I still wanted the small lunchbox sized wooden design but had a list of things I wanted to address.
* First, we have been using a Pine64 single board computer with Volumio installed to run an iPod Hifi unit as the main source of music in the house. The sound of this short lived speaker unit is still in my opinion great and the software enables it to be an Airplay receiver and music server that can be controlled on the local network through a web interface. A nice feature is that if you have multiple units running Volumio on the network they show up to be quickly selected and controlled from the web interface. I often found myself sneaking into my son's room at night to turn down or turn off his radio. Building the radio around Volumio I would be able to control it remotely. Also as it is netoworked I can upload new music and do software maintenance without having to physically connect to the device or pull the SD card. As the device could be controlled through the web interface I can quickly create new playlists or change the music up ont he device and it still acts as an Airplay receiver. Volumio will also broadcast its own hotspot so even out of the house the device can be controlled through the webinterface and be used as an Airplay speaker.
* Second, I had powered the first radio with just an off the shelf powerbank, the unit has some issues, mainly it does not put out power when charging up. It also is just a battery so tapping into power for other things isn't cleanly done. I chose to use the Powerboost 1000c from Adafruit and a 4400 mAh lithium ion battery for the power.
* Third, using Volumio headless and without an external device like a phone or tablet would mean my son would have less options to change the music if he wanted than the simple arduino device which gave him 9 playlists to choose from at the touch of a very clicky button. To remedy this I wanted to incorporate a touchscreen interface and chose the PiTFT+ 3.5" resistive touchscreen from Adafruit.
* Fourth, I wanted to incorporate a switching headphone jack so my son could listen to his music privately and really apreciate the solitude. I had gotten him some nice childs headphones that had volume limiting, they look like baby beats and actually dont sound too bad, and a terrible "childs" portable MP3 player for a trip we took. I could barely figure out the MP3 player but when I got it playing music he enjoyed just sitting and listening to his favorite Pixar and Disney scores. The headphones have the added bonus of blocking the sound from his brother which can sometimes bother him as little brothers do.
* Fifth was in regards to the enclosure, I have a great interest in woodworking and wanted to up the fit and finish of the enclosure. How to mount the touchscreen was a big issue I wanted to address cleanly, without access to a laser cutter or CNC router I would need to plan and cutout the window for the display. I chose to do this with a template and a flushcut bit on a router. This also gave the window rounded corners which look nice with the overall friendly wooden toy aesthetic.

List of components:
* Raspberry Pi 3 B+ (this project could have been done with as little as a Raspberry Pi Zero W, but I wanted to have the added oomph availible if need. And although I have not implemented it or tried it, Kodi can be installed along with Volumio if I ever wanted to allow myson to watch videos on the device and its tiny screen. As a general rule we heavily limit screen usage so currently don't want him to be able to watch videos in his room)
* Micro SD Card 8gb or higher, I went with a 16gb SanDisk
* Adafruit PowerBoost 1000c https://www.adafruit.com/product/2465 
* Adafruit PiTFT Plus 3.5 Resistive LCD https://www.adafruit.com/product/2441
* Adafruit Stereo 2.1W Class D Audio Amplifier https://www.adafruit.com/product/1552
* Gikfun 2" 4Ohm 3W speakers x2 https://www.amazon.com/gp/product/B01CHYIU26/ref=oh_aui_detailpage_o04_s00?ie=UTF8&psc=1 (used these for the previous radio, and impressed with the sound and price. Especially as they are being used ona volume limited childs radio I haven't had issues with distortion or overdrive from them)
* 3.5mm 3-pole Female Stereo TRS Balanced Socket with Switch https://www.amazon.com/gp/product/B00ZYWJ1DG/ref=oh_aui_detailpage_o02_s01?ie=UTF8&psc=1
* 3.5mm (1/8inches) Stereo Audio Male to AV 3-Screw Terminal Female Phoenix Adapter Connector https://www.amazon.com/gp/product/B01LWK3G1L/ref=oh_aui_detailpage_o00_s00?ie=UTF8&psc=1 (at one point was going to use more permanent soldered connectors but never got around to it or saw the point once I had it all together and working)
* on/off toggle switch, I had one laying around but here is a similar one https://www.amazon.com/Uxcell-a13042900ux0068-Position-Toggle-Replacement/dp/B00E6KA19K/ref=sr_1_12?s=industrial&ie=UTF8&qid=1546056601&sr=1-12&keywords=metal+toggle+switch+2+position
* Sanwa clone arcade buttons https://www.amazon.com/gp/product/B01N5JRU2R/ref=ppx_od_b_detailpages00?ie=UTF8&psc=1
* GPIO ribbon cable for connecting the display allowing more positioning options of the components https://www.amazon.com/gp/product/B01L6THEE8/ref=oh_aui_detailpage_o07_s00?ie=UTF8&psc=1
* Various hookup wire, most 22AWG and some jumper wires
* Heatshrink tubing, zip ties, hotglue solder etc...

Software things
* Volumio for Raspberry Pi https://www.volumio.org/get-started/
* PiTFT+ Easy install script https://learn.adafruit.com/adafruit-pitft-28-inch-resistive-touchscreen-display-raspberry-pi/easy-install-2
* Volumio touch display plugin (installed through Volumio web interface) https://github.com/volumio/volumio-plugins/tree/master/plugins/miscellanea/touch_display
* Volumio GPIO button plugin (installed through the Volumio web interface) https://github.com/volumio/volumio-plugins/tree/master/plugins/system_controller/gpio-buttons

### Raspberry Pi 3 B+ & Volumio

#### Initial Setup
1. Flash latest version of Volumio2 from https://www.volumio.org/get-started/ (at time of build current version was 2.513)
2. Boot into Volumio for first time, connect to the volumio hotspot netowrk it creates with password **volumio2** if using wireless, then connect on the local network http://volumio.local
    * run through configuration wizard and reboot
    * connect to Volumio again to enable SSH through the dev panel http://volumio.local/dev (if you changed the name of the device replace the local name i.e. *http://yourchosenname.local/dev*)
3. SSH into device Username is **volumio** Password is **volumio** 
```
ssh volumio@volumio.local
``` 
4. Install PiTFT+ from Adafruit using easy install script
    * https://learn.adafruit.com/adafruit-pitft-28-inch-resistive-touchscreen-display-raspberry-pi/easy-install-2
    * chose no for showing console and for mirroring HDMI
5. From the Volumio frontend install the Touchscreen Plugin and enable then restart Volumio
6. You should now see the Volumio interface on the PiTFT+ however the touchscreen is likely not repsonding properly, we will need to apply additional transformations to the touchscreen.
    * connect via ssh and edit /usr/share/X11/xorg.conf.d/40-libinput.conf
    ```
    sudo nano /usr/share/X11/xorg.conf.d/40-libinput.conf
    ```
    Add the following to the touchscreen section
    If you are rotating 90°
    ```
    Option "TransformationMatrix" "0 1 0 -1 0 1 0 0 1"
    ```
    If you are rotating 270°
    ```
    Option "TransformationMatrix" "0 -1 1 1 0 0 0 0 1"
    ```
7. You will need to restart but before we do lets make a quick edit to disable showing the cursor on the screen by editing /lib/systemd/system/volumio-kiosk.service
```
sudo nano /lib/systemd/system/volumio-kiosk.service
```
Find the line "ExecStart" and add '-- -nocursor' at the end of the line so it looks like this
```
ExecStart=/usr/bin/startx /etc/X11/Xsession /opt/volumiokiosk.sh -- -nocursor
```
now reboot the device, at this point the touchscreen should be working to navigate, we will make some modifications to the UI css to make the browse tab easier to navigate on the small screen.

#### Modify the CSS
On the 3.5" screen the UI elements in the browse tab are evry cramped and hard to navigate. Add in the fact that I am using a resistive touch screen and the experience is not somehting I would expect my 4 year old to have an easy time with. I followed the guidance by user andib on the Volumio forums from this post https://volumio.org/forum/change-size-elements-disable-elements-browse-tab-t9053.html and played with the values to resize the elements.
For ease of editing I downloaded the  /volumio/http/www/styles/app- ..... .css (the numerical value is different for every install) and opened in VS Code. I searched for
```
.browseTable .listWrapper.grid .itemWrapper
```
and as andib stated in the post found 4 instances of this
```
1. .browseTable .listWrapper.grid .itemWrapper{float:left;width:50%; ....
2. .browseTable .listWrapper.grid .itemWrapper{float:left;width:25%; ....
3. .browseTable .listWrapper.grid .itemWrapper{float:left;width:16.6667%; ....
4. .browseTable .listWrapper.grid .itemWrapper{float:left;width:16.6667%%; ....
```
I then ended up changing the values to the following
```
1. .browseTable .listWrapper.grid .itemWrapper{float:left;width:20%; ....
2. .browseTable .listWrapper.grid .itemWrapper{float:left;width:12%; ....
3. .browseTable .listWrapper.grid .itemWrapper{float:left;width:12%; ....
4. .browseTable .listWrapper.grid .itemWrapper{float:left;width:12%; ....
```

#### GPIO button control
I used the arcade style buttons for volume up and down, Play/Pause, Previous, and Next. I connected to the 2x13 pinout of the PiTFT+ and the solderpads on the PiTFT+ as follows.
| GPIO and Physical Pin     | Function    |
|------------------|-------------|
| BCM 2 Pin 3      | Play/Pause  |
| BCM 3 Pin 5      | Previous    |
| BCM 4 Pin 7      | Next        |
| Ground Pin 9     | Ground      |
| BCM 5 Solder Pad | Volume Down |
| BCM 6 Solder Pad | Volume Up   |

The ground for all the buttons are just daisy chained.
In Volumio install the GPIO button plugin through the web interface, enable and then assign the GPIO pins accordingly.

### Final Thoughts and Issues to be addressed

#### Issues
1. Bootup and Shutdown: bootup is close to 60 seconds on this device which is quite long for its purpose, it is loading a Linux OS but for a child's device it is slow. Especially compared to the 5  second bootup of the arduino based project my son is used to. Shutdown is another issue, while I did include a power switch that cuts power output from the Powerboost 1000c this is still equililant to a hard shutdown, which is not good for the OS. Properly shutting down the OS doesn't cut power to the LCD thus the need for the power switch. I suppose a script thats tied to another GPIO to control the powerboost somehow could be implemented. Not sure.
2. LCD backlight: the LCD backlight remains on even when the display "sleeps" so there is always energy draw and a glow. This can be controlled a couple of ways, neither of which are automatic. 
    * First a CLI command can be run to utilize the STMPE GPIO as documented by Adafruit https://learn.adafruit.com/adafruit-pitft-28-inch-resistive-touchscreen-display-raspberry-pi?view=all#backlight-control \
    To turn off
    ```
    sudo sh -c 'echo "0" > /sys/class/backlight/soc\:backlight/brightness'
    ```
    To turn on
    ```
    sudo sh -c 'echo "1" > /sys/class/backlight/soc\:backlight/brightness'
    ```
    * Secondly GPIO 18 can be used to control various settings, this is something I will likely implement with another physical button. Again a script thats tied to GPIO 18 and the sleep state of the display could probably be implemented.
3. Low Voltage: this is a mistake of mine. The Powerboost 1000c is a great little circuit but it only outputs 1 amp, when it would be best to to have a 2.5 amp supply given the power requirements of the audio amp, raspberry pi and the display. I would like to find a similar circuit that outputs 2.5 amps or more which would hopefully require minimal rewiring. The device does fine when plugged into a 2.5 amp supply, however its a roulette game if the device is booting up not connected to power if it will complete the boot up. It runs OK once booted and just playing local music files. However if any other activity such as transferring files to the device via SFTP or running commands over SSH is occurring while on battery power the low voltage warning MAY come up. This is less of an issue when the backlight is off.
4. The touchscreen itself: its resistive and not great, its doing the job, however a capacative model would be better. Possibly using a larger 5" or 7" screen would also help. If I did that the physical buttons would either have to be smaller or eliminated completely. 

#### Final Thoughts
Overall I am moderately happy with how this turned out. My son uses it most to listen to music when he goes to sleep so addressing the backlight is the biggest concern. I will continue to work to address the issues I have with it as I have been asked if I would make similar music players for some friends and family. If anyone has suggestions for any of the issues described please let me know.

### Fritzing schematic
