# pi-player - A simple Raspberry-Pi 4 and LibreELEC based video player with built-in autoplay

# Hardware

For setting up the `pi-player`, you need:
- Raspberry Pi 4 (2GB+ RAM recommended)
- Raspberry Pi 4 power supply
- micro HDMI to HDMI adapter + HDMI cable
- HDMI-compatible Full HD display or projector 
- micro SD card (~1GB + size of your videos)

Additional head sinks and a Raspberry Pi 4 enclosure with a fan are recommended,
but not mandatory.

## Setup

1. Download the LibreELEC image for Raspberry Pi 4:
http://releases.libreelec.tv/LibreELEC-RPi4.arm-9.2.1.img.gz.
1. Flash the image to the micro SD card. Using tools like [balenaEtcher](https://www.balena.io/etcher/) is recommended, but use whatever you are familiar with.
1. Create an additional `ExFAT` partition labeled `MEDIA` covering the remaining SD card space.
1. The following step requires a system capable of writing `ext4` partitions:
    1. Put the file `files/autoexec.py` into the `.kodi/userdata/` folder of the SD cards `STORAGE` partition.
1. Put the file `files/README.md` into the top-level folder of the SD cards `MEDIA` partition.
1. Follow the [instructions for creating the autoplay list](files/REAMDE.md) (can be done later as well).
1. Eject the micro SD card, put it into the Raspberry Pi 4 and boot.
1. Follow the on-screen instruction to initialize LibreELEC. If you created a playlist beforehand, your videos should already play in the background.

## Notes

1. The playlist and video files on the SD card can also be modified via the SAMBA network share. To do so, enable SAMBA (SMB) in the LibreELEC settings, connect the `pi-player` to the network and connect to the `LIBREELEC` share. The `MEDIA` partition is located in the `MEDIA` folder.
1. The Raspberry Pi 4 has two HDMI ports. LibreELEC will output to port `HDMI0`.
1. Use the `h.264` video codec for best performance on the Raspberry Pi 4.
1. For enabling 4K@60Hz output, add `hdmi_enable_4kp60=1` to your `config.txt`.
1. The above setup steps are intended for copying the media and playlist files to the SD card from a MS Windows or macOS system that don't support the `ext4` file system used by LibreELEC for the `STORAGE` partition. If accessing the `ext4` `STORAGE` partition directly or via network is feasible, the separate `MEDIA` partition is not necessary. The `autoplay.m3u` path needs to be adjusted accordingly in `autoexec.py`.
