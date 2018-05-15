# Write Img Rasberry Pi use OSX
 
1. Download img: http://www.raspberrypi.org/downloads
2. Extract image:
	unzip ~/Downloads/2018-04-18-raspbian-stretch.zip

3. Connect the SD Card 
	df -h 
	diskutil list
	diskutil list disk2
	diskutil info dusk2s1
	ls /dev/disk2
	...
	check disk is sdcard on osx
4. Unmount the partition so that you will be allowed to overwrite the disk
	sudo diskutil unmount /dev/disk2s1
5. Using the device name of the partition work out the raw device name for the entire disk
	/dev/disk2s1 => /dev/rdisk2
6. sudo dd if=`PATH of IMG` of=/dev/rdisk2 bs=1m
7. sudo diskutil eject /dev/rdisk2
8. Insert it in the RasPi

# Connect Wifi RasPi when do not monitor

1. Open Terminal BOOT : cd /Volumes/boot
	touch wpa_supplicant.conf
	ngang hang with config
2. write wpa_supplicant.conf

for Raspbian Jessie:

	network={
    ssid="YOUR_NETWORK_NAME"
    psk="YOUR_PASSWORD"
    key_mgmt=WPA-PSK
}

for Raspbian Stretch:

ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
network={
    ssid="YOUR_NETWORK_NAME"
    psk="YOUR_PASSWORD"
    key_mgmt=WPA-PSK
}

3. IP Scan search ip RasPi
4. User: pi
	Password: raspberry

# use SSH

1. cd /Volumes/boot
2. touch ssh

# Change Password Pi & Root

1. passwd pi
2. passwd root

# Enable VNC Server

1. sudo apt-get update
2. sudo apt-get install realvnc-vnc-server realvnc-vnc-viewer
3. Enabling VNC server Graphically

Menu -> Preferences -> Raspberry Pi Configuration ->  Interfaces
VNC is Enabled

4. Enabling VNC SERVER AT the command Line

sudo raspi-config

- Navigate to Interfacing Options.

- Scroll down and select VNC > Yes.

# Install NodeJS new version on RasPi

- https://nodejs.org/en/download/
- copy node for Linux Binaries (ARM): https://nodejs.org/dist/v8.11.1/node-v8.11.1-linux-armv7l.tar.xz
- wget https://nodejs.org/dist/v8.11.1/node-v8.11.1-linux-armv7l.tar.xz
- tar -xvf node-v8.11.1-linux-armv7l.tar.xz
- cd node-v8.11.1-linux-armv7l.tar.xz
- sudo cp -R * /usr/local/
- sudo reboot
- node -v
- npm -v

