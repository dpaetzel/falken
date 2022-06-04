# falken


Records the stream that can be found at [this
URL](https://start.video-stream-hosting.de/player.html?serverip=116.202.235.106&serverapp=wsgs-live&streamname=Falken.smil).


Meant to be put on a lightweight machine (I use a Raspberry Pi).


Note that this has all been setup rather quick'n'dirty and best-effort only.


# Setup on a Raspberry Pi 3


More like “How *I* set this up” (and not “How you *should* set this up”).


## Flash OS, then boot


Use `rpi-imager` to flash *Raspberry Pi OS Lite*. Booting this image makes you
set your username and password.


## On the Raspberry Pi 3: Enable SSH


```bash
sudo raspi-config
```

Within that tool, navigate to *Interfacing options*, then activate *SSH*.


Optional: On your local machine, copy SSH key using

```bash
ssh-copy-id -F /dev/null -i .ssh/id_rsa.raspberrypi.david david@raspberrypi
```


## On the Raspberry Pi 3: Install mosh


```bash
sudo apt-get update
sudo apt-get install mosh
```


## From now on: Login via SSH


```bash
mosh david@raspberrypi
```


## Clone this Git repository


```bash
git clone https://github.com/dpaetzel/falken
```
