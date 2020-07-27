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
1. Put the file `files/README.md` into the top-level folder of the SD cards `MEDIA` partition.

### Adding the autoplay script
The script `files/autoexec.py` needs to be copied to the SD cards `STORAGE` partition.

#### Linux & other OS supporting ext4 file systems
1. Copy the file `files/autoexec.py` into the `.kodi/userdata/` folder of the `STORAGE` partition.

#### Any OS supporting Samba network shares
1. Put the micro SD card into the Raspberry Pi and boot it.
1. Follow the on-screen instruction to initialize LibreELEC:
    1. Configure WiFi, if the Raspberry Pi isn't connected via Ethernet.
    1. Enable Samba (SMB).
1. From another system with network access to the Raspberry Pi via network, connect to the `LIBREELEC` Samba share.
1. Place the file `files/autoexec.py` into the `Userdata` folder.

### Adding media files
1. Access the `MEDIA` partition directly through a file manager on a system with a micro SD card reader or connect to the `LIBREELEC` Samba network share and switch to the `MEDIA` folder.
1. Follow the [instructions for creating the autoplay list](files/README.md).

### Finishing
1. (Re-)Boot the Raspberry Pi with the `pi-player` SD card inserted.
1. Complete the LibreELEC setup wizard if you haven't already.
1. If you created a playlist beforehand, your videos should already play in the background.

## Notes

1. The Raspberry Pi 4 has two HDMI ports. LibreELEC will output to port `HDMI0`.
1. If your display doesn't support HDMI audio or you need to connect external speakers to the Pi for any other reason, it is recommended to connect them through a separate USB sound card since the built-in Raspberry Pi auto port only provides rather low quality. This also requires to adjust the audio routing in LibreELEC.
1. Use the `h.264` video codec for best performance on the Raspberry Pi 4.
1. For enabling 4K@60Hz output, add `hdmi_enable_4kp60=1` to your `config.txt`.
1. The above setup steps are intended for copying the media and playlist files to the SD card from a MS Windows or macOS system that don't support the `ext4` file system used by LibreELEC for the `STORAGE` partition. If accessing the `ext4` `STORAGE` partition directly or via network is feasible, the separate `MEDIA` partition is not necessary. The `autoplay.m3u` path needs to be adjusted accordingly in `autoexec.py`.
