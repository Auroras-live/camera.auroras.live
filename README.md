# WeatherCam
This is alpha software, being written as part of the Auroras.live Sensor Network, an "internet of things" for aurora hunting equipment.

## About the project
The Auroras.live Sensor Network will be a range of internet-connected devices, ranging from skyward-facing webcams, through to home made magnetometers and internet connected weather stations. This system will be entirely DIY, so Auroras.live won't actually provide or set up these items, but will allow enthusiasts to add their items to the network using the Auroras.live API. Data will be provided on a map for others to explore and view.

The software will be "one-way", so the software will push TO Auroras.live, but nobody can connect to or interfere with your device.

## About this software
This software uses the `raspistill` command, node.js and GraphicsMagick to take a photo every 5 minutes, overlay weather / aurora hunting data over the top, then uploads it to the Auroras.live sensor network where it's then displayed on a map on the website and app for others to view. 

As mentioned above, this communication is presently one-way, so the sensor network has no control over the device, other than doing an update every night at midnight. 

## Installation
Eventually this will be released as a simple install script, but for now:

You will need a Raspberry Pi (2 or above), the Raspberry Pi camera module and optionally, a WiFi dongle.

1. [Download Raspian Jessie](https://www.raspberrypi.org/downloads/raspbian/)
2. Image it to your SD card. For Windows, something like [Win32DiskImager](https://sourceforge.net/projects/win32diskimager/) works perfectly
3. Plug your Raspberry Pi camera in, HDMI (if using a monitor to set it up), Ethernet (if using SSH to set it up), then power.
4. SSH in or go into the terminal on your Pi
5. Install node.js using the command `curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash`
6. Install `node`, `GraphicsMagick` and `Git` by running `sudo apt-get install nodejs git graphicsmagick`
7. Clone this repo into your home directory: `git clone https://github.com/Auroras-live/WeatherCam`
8. Install `nodemon`, `node-autostart` and `gulp` first, using `npm install -g gulp nodemon node-autostart`
9. Install the remaining node dependencies using `npm install`
10. Run `autostart enable -n "weathercam" -p "~/weathercam" -c "nodemon index"` to auto-start the camera app
10. Make a folder in /boot called `weathercam` using `sudo mkdir /boot/weathercam`
11. Email admin@auroras.live and request an API key. You'll need to provide the following:
  * Your name
  * A contact email (used so we can send you automatic and manual alert emails)
  * The town, suburb or area you live in *which will be displayed on the camera image itself and will be searchable on the website or app*. The location will be non-specific (e.g. "Inverloch", not "123 Sample Street, Inverloch")
12. Create a file in there called `config.json`. In it, put the following:

```json
{
      "apikey": "<your API key here>",
      "location": "<your location from step #11 here>"
}
```

The API key is private, and identifies you as the owner of the camera, making you responsible for any images that are uploaded to Auroras.live. **Keep this key secure!**

Finally, reboot your Pi. Check that it's working by visiting http://raspberrypi:9001/image.jpg . Point your camera at the sky, and let it go!

This software is still in alpha. For more information, email admin@auroras.live
