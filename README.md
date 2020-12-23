# PiLittleRadio
A Raspberry Pi internet radio controlled from a web page

## What it does
Turn an old Raspberry Pi and some amplified speakers into an internet radio you can control from your phone, tablet, Kindle or and computer on your WiFi network. It uses a simple webserver on the Pi to dish up a web page you can use to change channel, adjust the volume and see some 'now playing' track info via Twitter.

## What you'll need
- Some kind of Raspberry Pi with an audio jack and an SD card
- A way of connecting it to the internet, either ethernet or wifi
- Amplified speakers or headphones
- Some familiarity with command line Linux and using a text editor like nano.
- That's it. This is not an audiophile project, it does not use an external DAC. In my view the 3.5mm jack is good enough for a radio in the kitchen, garage or workshop.

## How to install it

### Bake a fresh Pi
- Download a fresh copy of Raspberry Pi OS Lite, I used the current Buster image: https://www.raspberrypi.org/software/operating-systems/#raspberry-pi-os-32-bit 
- Flash it to the SD card - I used the 16GB microSD card that was in my old Pi using RaspberryPi imager app (Mac) but you could use a much smaller card.
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
- Log in by SSH from Terminal on your laptop: `ssh pi@192.168.1.199` in my case, enter password
- Hooray! You're now logged in to your Pi remotely!

### Install MPD and MPC
- Run `sudo apt-get update` on Pi
- Install Music Player Client and Daemon. These will stream internet radio for you.	Use `sudo apt-get install mpd mpc`

### Add some radio stations
- Add a radio station, for example fip, the greatest radio station in the world:
	`mpc add http://icecast.radiofrance.fr/fip-midfi.mp3`
- Test with `mpc play 1` - it should plays FIP out of the headphone socket.
- Add some more radio stations. You need the raw streaming URL, they can be found for most radio stations. My list looks like this:
	- BBC Radio 2 `mpc add http://bbcmedia.ic.llnwd.net/stream/bbcmedia_radio2_mf_p`
	- BBC Radio 3 `mpc add http://bbcmedia.ic.llnwd.net/stream/bbcmedia_radio3_mf_p`
	- BBC Radio 4 FM `mpc add http://bbcmedia.ic.llnwd.net/stream/bbcmedia_radio4fm_mf_p`
	- BBC Radio 5Live `mpc add http://bbcmedia.ic.llnwd.net/stream/bbcmedia_radio5live_mf_p`
	- BBC 6music `mpc add http://bbcmedia.ic.llnwd.net/stream/bbcmedia_6music_mf_p`
	- BBC World Service News stream `mpc add http://bbcwssc.ic.llnwd.net/stream/bbcwssc_mp1_ws-einws`
	- RTÉ Radio 1 `mpc add http://icecast2.rte.ie/radio1`
	- RTÉ 2XM `mpc add http://icecast2.rte.ie/2xm`
	- Scala Radio `mpc add https://stream-mz.planetradio.co.uk/scalahigh.aac`
	- BBC Radio 4 Extra `mpc add http://bbcmedia.ic.llnwd.net/stream/bbcmedia_radio4extra_mf_p`
	- BBC 6music high quality `mpc add http://a.files.bbci.co.uk/media/live/manifesto/audio/simulcast/hls/uk/sbr_high/ak/bbc_6music.m3u8`
	- BBC Radio 3 high quality `mpc add	http://a.files.bbci.co.uk/media/live/manifesto/audio/simulcast/hls/uk/sbr_high/ak/bbc_radio_three.m3u8`
	- fip high quality `mpc add http://icecast.radiofrance.fr/fip-hifi.aac`
- They will play by numbers in the order you add them, e.g. `mpc play 4` plays BBC Radio 4.

### Pump up the volume
- Edit the mpd.conf file on the Pi to enable volume changes to work with `sudo nano /etc/mpd.conf` 
The audio_output section should end up looking like this:
`audio_output {
        type            "alsa"
        name            "My ALSA Device"
        mixer_type      "software"   
}`
- My audio jack audio was too quiet, so I fixed this using `alsamixer`. Press F6, select the headphones and turn the volume up. I went up to about 80%. Press ESC to escape. Test it out by playing some radio `mpc play 1` then try `mpc volume +10` or `mpc volume -10` to increase and decrease the volume.

### Install a webserver
- to come

### Add the web pages
- to come

### Test
- to come
