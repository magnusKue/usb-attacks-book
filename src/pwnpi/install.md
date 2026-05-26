# Installation

## 1. Flash the Image

First, download the latest release of the custom image from [RoganDawes/P4wnP1_aloa](https://github.com/RoganDawes/P4wnP1_aloa/releases/tag/v0.1.1-beta).

This guide was created with `v0.1.1-beta`. The image is provided in `.img.xz` format, so it needs to be decompressed first:

```bash
$ xz -d ~/Downloads/kali-linux-v0.1.1-beta-rpi0w-nexmon-p4wnp1-aloa.img.xz
```

Once decompressed, the image can be written to the MicroSD card. Insert the card and identify its device name:

```bash
$ lsblk
```

The device will likely appear as something like `/dev/sdX`.

> ⚠️ **Double-check the device name before proceeding — writing to the wrong device will corrupt that drive!**

Now write the image:

```bash
$ dd if=<path-to-img> of=<name-of-drive> bs=4M status=progress conv=fsync
```

Once the process is complete, unmount and remove the SD card, insert it into the Pi, and power it on.
