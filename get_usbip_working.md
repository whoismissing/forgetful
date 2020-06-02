**first world problem:**

the game controller cable is too short to plug in to the computer and sit from the couch at the same time

**solution:**

try a usb over network solution like usbip.

**setup:**

* client - windows 10
* server - ubuntu 18.04.3 linux kernel v 4.15.0-99

using the instructions [here](https://github.com/solarkennedy/wiki.xkyle.com/wiki/USB-over-IP-On-Ubuntu), we install and bind the usb devices to the server

**instructions:**

mirroring the instructions, we have:

Install usbip on the server that is going to export the usb port (what we plug our usb's into)
```
apt-get install linux-tools-generic
modprobe usbip_host
echo 'usbip_host' >> /etc/modules
```

Bind a usb port to share it over the network
```
/usr/lib/linux-tools/`uname -r`/usbip list -l
/usr/lib/linux-tools/`uname -r`/usbip bind -b 1-1.3 # obtain the proper id via the `lsusb` command
/usr/lib/linux-tools/`uname -r`/usbipd # Run the server
```

On the client, list and attach
```
/usr/lib/linux-tools/`uname -r`/usbip list -r $remote_host
/usr/lib/linux-tools/`uname -r`/usbip attach -r $remote_host -b 1-1.3
```

**errata**

the windows client from usbip on sourceforge doesn't seem to work with a linux kernel version after 3.1.10 according to [here](https://sourceforge.net/p/usbip/discussion/418508/thread/cfd3ddb1/)

so we use the v0.1.0 binary [release](https://github.com/cezanne/usbip-win/releases/tag/v0.1.0) from https://github.com/cezanne/usbip-win instead installing via the client instructions on the README

