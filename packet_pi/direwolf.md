# Direwolf on a rapsberry pi

 Will try these instructions first. 
 * Main Article:
 ** https://www.vnutz.com/articles/direwolf_on_a_raspberry_pi_for_mobile_aprs
 ** https://www.trinityos.com/HAM/CentosDigitalModes/RPi/rpi4-setup.html
 * some build notes: https://www.marrold.co.uk/2019/04/installing-direwolf-15-on-raspberry-pi.html
 * gps libs: https://lindevs.com/install-build-essential-on-raspberry-pi
 * avahi: https://groups.google.com/g/aprsfi/c/Libx5hd_r_U?pli=1
 * hamlib:  https://groups.io/g/direwolf/topic/you_must_rebuild_direwolf/79501429

 
# Updates
https://www.trinityos.com/HAM/CentosDigitalModes/RPi/rpi4-setup.html

`1,$s/Debiam/Debian/g`

EOL Debian 10 “Buster”  August 1st, 2022 to June 30th, 2024
Maybe only document Bullseye? Remove references to othr EOL versions.

64 bit is not beta anymore.  Raspberry PI v 3 & 4 uppport 64bit

If using the Raspberry Pi Imager, PI account is not created, unless you specify that as your account.
Issue with v1.7.5 of the imager is that it does not set your wireless interface.  So hook it to a ethernet cable then use raspi-config to setup wifi access.

SSH Port: Port scanner will figure out that another port servicing SSH.  Just make sure you are using SSH key 2048bit or better to use ed25519 if you can or rsa 4098 bit.  Best practive, rotate you ssh key evefry 90 days, but never use a key for more than a year.   Usig a pass phrase is even better.


# 1.a Choose a quality SD card and how to put a Raspbian image on it
404: Elinux SD card compatibility
  http://elinux.org/RPi_SD_cards%20for%20a%20lot%20more%20details%20on%20what%20cards%20are

# 1.b Download the newest Raspbian OS release and install it
Change references from buster to Bullseye
p, instead of image-rpi-sdcard-multiformat.sh , use the 
If using a UI  build  the image using the Raspbery Pi Imager.  As of 8/21/2023 v1.7.5 ia the latest. https://www.raspberrypi.com/software/.  Once you make storeage or OS selection on the raspberry pi imager, the setting gear will become selectable. From ther you can set:
* hostname
* enable ssh
* set initial user and password
* configure lan - wifi does not take, use ethrnet cable initially.
* Set locale settings - does not set correctly.

Can run `sudo raspi-config` once your ssh in to complete settings.



# 3. Boot up the new image and prepare to do initial security on it
## 3.a Create a new user and disable the Pi user
### 1.a. Add this new user into the following UNIX groups:
using the imager, already a member of the following group
```
mpechner@packet:~ $ cat /etc/group | grep mpechner | sort
adm:x:4:mpechner
audio:x:29:pulse,mpechner
cdrom:x:24:mpechner
dialout:x:20:mpechner
games:x:60:mpechner
gpio:x:997:mpechner
i2c:x:998:mpechner
input:x:104:mpechner
lpadmin:x:117:root,mpechner
mpechner:x:1000:
netdev:x:108:mpechner
plugdev:x:46:mpechner
render:x:106:mpechner
spi:x:999:mpechner
sudo:x:27:mpechner
users:x:100:mpechner
video:x:44:mpechner
```

## .c IPTABLES: Install and configure a simple but effective firewall
Not sure IPtables is needed

```
mpechner@packet:~ $ netstat -lntu
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN
tcp        0      0 127.0.0.1:631           0.0.0.0:*               LISTEN
tcp6       0      0 :::22                   :::*                    LISTEN
tcp6       0      0 ::1:631                 :::*                    LISTEN
udp        0      0 0.0.0.0:68              0.0.0.0:*
udp        0      0 0.0.0.0:631             0.0.0.0:*
```
68 is DHCP so do not block

631 is print printing, disable  `sudo systemctl disable cups`
