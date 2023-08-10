# Direwolf on a rapsberry pi

 Will try these instructions first. 
 * Main Article:
 ** https://www.vnutz.com/articles/direwolf_on_a_raspberry_pi_for_mobile_aprs
 ** https://www.trinityos.com/HAM/CentosDigitalModes/RPi/rpi4-setup.html
 * some build notes: https://www.marrold.co.uk/2019/04/installing-direwolf-15-on-raspberry-pi.html
 * gps libs: https://lindevs.com/install-build-essential-on-raspberry-pi
 * avahi: https://groups.google.com/g/aprsfi/c/Libx5hd_r_U?pli=1
 * hamlib:  https://groups.io/g/direwolf/topic/you_must_rebuild_direwolf/79501429

 Installing a minimalist headless pi raspberry pi os

 apt install git cmake

 sudo apt install libasound2-dev libudev-dev
 apt-get install  alsa-utils gpsd libgps-dev
 sudo apt install libavahi-client-dev
 
sudo apt install -y build-essential - already there

## Install and build Direwolf
*  git clone https://github.com/wb2osz/direwolf.git/
*  cd direwolf
*  mkdir build && cd build
*  cmake ..
   ** rerun cmake utit happy.  Skip hamlib dependancy    
*  make -j4
*  sudo make install
*  make install-conf

## thismuch done 8/9/2023
