# How to flash raspbian on a Rasperry Pi

**First you need some tools**

1. balenaEtcher

2. raspbian iso

3. a pc

4. 15-20 minutes

**The image in this [repository](https://drive.google.com/file/d/1wLuyTCQxGp63mAIFYXXDNSh0i43EToBi/view?usp=sharing) is preconfigured: it have ssh enabled and wpa_supplicant configured**

## Let's install etcher

got do balena [download page](https://www.balena.io/etcher/) and download the version suitable for you.

![](/home/rdfilippo/Desktop/Scuola/howToFlashARaspberry/Screenshot_20211005_092258.png)
<img title="image" src="https://github.com/filippo-ferrando/howToFlashARaspberry/blob/master/Screenshot_20211005_092258.png" alt="" width="377" data-align="center">

## Download the raspbian ISO

for this guide we will use the lite version because we don't need a GUI

![](/home/rdfilippo/Desktop/Scuola/howToFlashARaspberry/Screenshot_20211005_092632.png)
<img title="image" src="https://github.com/filippo-ferrando/howToFlashARaspberry/blob/master/Screenshot_20211005_092632.png" alt="" width="377" data-align="center">

## Now we have all we need!!

go and take you micro sd and insert it in to the pc.

Then open balenaEtcher and select your iso image.

![](/home/rdfilippo/Desktop/Scuola/howToFlashARaspberry/Screenshot_20211006_080927.png)
<img title="image" src="https://github.com/filippo-ferrando/howToFlashARaspberry/blob/master/Screenshot_20211006_080927.png" alt="" width="377" data-align="center">

##### Then select the media you want to flash and click "Flash!"

## Create ssh folder in boot partition

Because we want to use the Pi in headless mode (without keyboard and monitor) we have to activate ssh from the first boot.

To do that mount the sd card just flashed in your pc and open the **boot** partition.

create a folder named "ssh" and job done!

## Configure wpa_supplicant for wifi connection

The Pi will connect to the lan via WiFi, so you need to setup the connection before the Pi boots.

To do that mount again the sd in your pc but this time go in the root partition.

We gonna modify the file */etc/wpa_supplicant/wpa_supplicant.conf* and add the ssid and the password of the wifi network designed.

**The file requires root permissions to modify**

Once you opened that the file have to look like these:

```bash
country=it
update_config=1
ctrl_interface=/var/run/wpa_supplicant

network={
 ssid="YOURSSID"
 psk="YOURPASSWORD"
}
```

After that you can finally put the sd in the Pi and power it up!

### First boot and basic config
