# PiLittleRadio
A Raspberry Pi internet radio controlled from web page

## What it does
Turn an old Raspberry Pi and some amplified speakers into an internet radio you can control from your phone, tablet, Kindle or and computer on your WiFi network. It uses a simple webserver on the Pi to dish up a web page you can use to change channel, adjust the volume and see some 'now playing' track info via Twitter.

## What you'll need
- Some kind of Raspberry Pi with an audio jack and an SD card
- A way of connecting it to the internet, either ethernet or wifi
- Amplified speakers or headphones

## How to install it
- Download a fresh copy of Raspberry Pi OS Lite, I used the current Buster image: https://www.raspberrypi.org/software/operating-systems/#raspberry-pi-os-32-bit 
- Flashed it to the SD card - I uses the 16GB microSD card that was in my old Pi using RaspberryPi imager app (Mac) but you could use a much smaller card.
- Plugged the Pi into a TV or monitor via HDMI socket, ethernet internet and a USB keyboard
- Wait for it to expand filesystem and run apt upgrade 
- log in as pi / raspberry
- configure a few things with sudo raspi-config:
-- set Wifi credentials
-- set audio to 3.5mm jack
-- change default Pi user password
-- Interface - enable SSH so you can administer from laptop
-- Change hostname: I used 'PiLittleRadio' to make it easier to find on your local network
- reboot Pi, sudo shutdown now
- unplug, replug
- Looked at your router admin page (e.g. BT Home Hub is http://192.168.1.254/) to see if it had successfully joined wifi, and get its IP address: soemthing like 192.168.1.199
- Log in by SSH from Terminal on your laptop: ssh pi@192.168.1.199 in my case, enter password
- Hooray! You're now logged in remotely!
- Run `sudo apt-get update` on Pi
- Install Music Player Client and Daemon. These will stream internet radio for you.	Use `sudo apt-get install mpd mpc`
