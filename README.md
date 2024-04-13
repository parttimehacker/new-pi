# new-pi
Basic startup installation instructions for a raspberry pi
## Description

This repository contains instructions and bash scripts I use to configure new Raspberry Pi devices as Raspbian OS servers. I use the Raspberry Pi Image Installer to copy the latest Raspberry Foundation image to a SD card. I enable SSH and set up Wi-Fi on the SD card. I strongly recommend creating a **NEW USER** account and delete the **PI** account, which can be automatic if you use the new Imager.

## Raspberry Pi Imager v1.8.4

The new Imaging app allows you to configure many important first steps like Wi-Fi SSID and password, user name, host name, etc. The link to the
new imager is https://www.raspberrypi.com/software/

## Remote Access and Development Configuration

Remote login to the new device from your development host. I like to update .bashrc with ll command.

```
vi .bashrc
```
- Followed by
```
source .bashrc
ll
```
### Configuring Your Raspberry Pi

A default configuration dialog will start on the first boot of your new SD card. Run raspi-config, the Raspberry Pi
Configation dialog. Update the following based on your plan for the server:

* Enable interfaces: Camera, SSH, VNC, SPI and I2C

```
sudo raspi-config
```
- Install i2cdetect if your are planning I2C
```
sudo apt-get -y install i2c-tools
```
- Add lint for good practice
```
sudo pip3 install pylint --break-system-packages
```
- If the terminal font is too small then you can change it from the command line
```
sudo vi /etc/default/console-setup 
```
- Enter the following, save and exit
```
FONTFACE="Terminus
FONTSIZE="16x32"
```

### Update packages
```
sudo apt -y update
sudo apt-get -y update
sudo apt-get -y upgrade
sudo apt-get -y dist-upgrade
```

### Install Firewall 
- Install the raspian firewall with restrictions unless specifically allowed.
```
sudo apt-get -y install ufw
sudo ufw allow 22
sudo ufw allow 548
sudo ufw allow 80
sudo ufw allow 443
sudo ufw allow 5000
sudo ufw allow 5900
sudo ufw enable
sudo ufw status
```
## This is optional but a good idea to test the I2C bus for future IOT devices.
```
sudo i2cdetect -y 1
```
* Operating information
```
uname -a
```
* Hardware information
```
cat /proc/device-tree/model
```
* Network Information
```
hostname -I
```
* Raspberry Pi OS version
```
cat /etc/os-release
```
All done.
## Sync and Reboot
- Test the basic install and firewall
```
sudo sync
sudo reboot
```
## Licence
-------

MIT

## Authors
-------

`new-pi` was written by `Dave Wilson <parttimehacker@gmail.com>`_.
