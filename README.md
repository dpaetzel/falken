# falken


Systemd service and shell script to record the stream that can be found at [this
URL](https://start.video-stream-hosting.de/player.html?serverip=116.202.235.106&serverapp=wsgs-live&streamname=Falken.smil)
to `$HOME/recordings/` in segments of 30 min.


Meant to be put on a lightweight machine (I use a Raspberry Pi).


**Important: Make sure that you have enough space left on the partition the
recordings are stored on.** They're around 2.5 GB/h in size. I'm using the
`fetch-falken` script to move finished recordings to some other location with
more storage.


Note that this has all been setup rather quick'n'dirty and best-effort only. In
the longterm I might create a [NixOS image](https://nixos.org/) for this (and
this is of course what I would recommend for you to do as well).


# Setup on a Raspberry Pi 3


More like “How *I* set this up” (and not “How you *should* set this up”).


## Flash OS, then boot


Use `rpi-imager` to flash *Raspberry Pi OS Lite*. Booting this image makes you
set your username and password.


## On the Raspberry Pi 3


Enable SSH using

```bash
sudo raspi-config
```

Within that tool, navigate to *Interfacing options*, then activate *SSH*.


Optional: On your local machine, copy SSH key using

```bash
ssh-copy-id -F /dev/null -i .ssh/id_rsa.raspberrypi.david david@raspberrypi
```


Optional: Install mosh.

```bash
sudo apt-get update
sudo apt-get install mosh
```


From now on: Just login via SSH.

```bash
mosh david@raspberrypi
```


## Install stuff


Install required software:

```bash
sudo apt-get update
sudo apt-get install git ffmpeg fish
```


Clone this Git repository:

```bash
git clone https://github.com/dpaetzel/falken
cd falken
```


**Important: Make sure to adjust the paths and username in the service file
(they're hardcoded to my username right now).**


Activate and check the service:

```bash
sudo cp falken.service /etc/systemd/system/
sudo chmod 640 /etc/systemd/system/falken.service
sudo systemctl status falken
sudo systemctl daemon-reload
sudo systemctl start falken
sudo systemctl status falken
sudo systemctl enable falken
sudo systemctl status falken
sleep 10
ls $HOME/recordings
```
