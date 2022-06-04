# How to flash raspbian on a Rasperry Pi

**First you need some tools**

1. balenaEtcher

2. raspbian iso

3. a pc

Estimate Time: 15-20 minutes

## Let's install etcher

got do balena [download page](https://www.balena.io/etcher/) and download the
suitable version for your needs.

<img title="image" src="Screenshot_20211005_092258.png" alt="" width="377" data-align="center">

## Download the raspbian ISO

for this guide we'll use the lite version 'cause we don't need a GUI

<img title="image" src="Screenshot_20211005_092632.png" alt="" width="377" data-align="center">

## Now we have all we need!

Take you micro sd and insert it into the pc.

Then open balenaEtcher and select your iso image.

<img title="image" src="Screenshot_20211006_080927.png" alt="" width="377" data-align="center">

##### Then select the media you want to flash and click "Flash!"

## Create ssh folder in boot partition

We have to activate ssh at the first boot because we want to use the Pi in
headless mode (without keyboard and monitor).

To do that mount the sd card just flashed in your pc and open the **boot**
partition.

create a folder named "ssh" and the job is done!

## Configure wpa_supplicant for wifi connection

The Pi will connect to the lan via WiFi, so you need to setup the connection
before the Pi boots.

To do that mount again the sd in your pc, but this time go into the root
partition.

We'll modify the file _/etc/wpa_supplicant/wpa_supplicant.conf_ and add the ssid
and password of the designed wifi network.

**The file requires root permissions to be modified**

Once you opened that the file, it has to look like these:

```bash
country=it
update_config=1
ctrl_interface=/var/run/wpa_supplicant

network={
 ssid="YOURSSID"
 psk="YOURPASSWORD"
}
```

After that you can finally put the sd in your Raspberry Pi and power it up!

## First boot and basic config

When the pi ha booted up you have to find its ip address, to do it run the
command _ip-scan_ and connect your pc to the board via ssh

```bash
ssh pi@*pi ip*
```

The default password is **raspberry**

Once you're connected, launch the command:

```bash
sudo raspi-config
```

This will prompt a menu from which we can change some important settings:

<img title="image" src="raspi-config_main.png" alt="" width="377" data-align="center">

1. hostname --> the device name on the network

2. locale --> Country (language)

3. timezone

4. password --> change pi and root password

**optionally** we can enable the _"wait for network at boot"_ which won't fully
boot the operating system until a Wi-Fi or cable connection is established.

## Update and Upgrade

Another importat thing is to keep the software up-to-date, so we can run:

```bash
sudo apt update && sudo apt upgrade
```

to update the index of packages and upgrade the installed software.

Then we reboot the pi and we're ready to rock!
