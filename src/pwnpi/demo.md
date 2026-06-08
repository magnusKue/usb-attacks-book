{{#title P4wnP1 Demo}}
# Demo
To demonstrate the capabilities of this setup, we created a small demo where the P4wnP1 loads a ROM (Pokemon Yellow) and a Game Boy emulator via MSC and starts playing it automatically.

## Storage Preparation
Start by preparing the required files.  
Create a `payload` directory in `/usr/local/P4wnP1/helper`.

### 1. mGBA
I'm using the mGBA emulator here.  
- Download the AppImage [here](https://github.com/mgba-emu/mgba/releases/download/0.10.5/mGBA-0.10.5-appimage-x64.appimage).
- Rename it to `MGBA.appimage`
- And place it in the payload directory.

### 2. Pokemon Yellow
Make sure to legally dump your own copy of the game. Just Google "Vimm's Lair Pokemon Yellow ROM" to learn how! :)  
Then add the ROM to the payload directory, renamed to `POKY.gb`.

### 3. Key Extender
**There is one significant problem:**
The P4wnP1 does not provide an API for holding down keys. The standard `press()` and `type()` functions only hold keys for 1ms.
This is a problem for Game Boy games, which poll inputs from a hardware register rather than using input events like a terminal would.

To work around this we use a small Python script that attaches to the P4wnP1's HID device and repeats all desired key presses, holding them down for 100ms.
With the script running, the emulator sees the following:

```bash
$ wev
[       16:     wl_keyboard] key: serial: 28554; time: 4622645; key: 53; state: 1 (pressed)
                      sym: x            (120), utf8: 'x'
[        16:     wl_keyboard] key: serial: 28555; time: 4622646; key: 53; state: 0 (released)
                      sym: x            (120), utf8: ''
[        16:     wl_keyboard] key: serial: 28556; time: 4622647; key: 53; state: 1 (pressed)
                      sym: x            (120), utf8: 'x'
[        16:     wl_keyboard] key: serial: 28557; time: 4622747; key: 53; state: 0 (released)
                      sym: x            (120), utf8: ''
```

This `wev` (Wayland event viewer) output shows the P4wnP1's original key press (released after 1ms) followed immediately by the re-emitted press held for 100ms.

This works, but introduces another problem: unlike X11, Wayland does not share input events globally. Each process only receives input targeted at its own window. This means there is no way for the script to capture all HID input events.

> [!WARNING]
> Root access is required for this demo!

This is not an ideal solution, but it was the only approach that got the P4wnP1 to reliably control a Game Boy emulator. It is only necessary because the P4wnP1 is primarily designed as a text injector, not a game controller. For the purposes of this demo we will prepare the target system with a udev rule and leave it at that.

Start by adding a new udev rule on the system the demo will run on:
```text
# add this to /etc/udev/rules.d/99-input.rules
KERNEL=="uinput", GROUP="input", MODE="0660"
KERNEL=="event*", GROUP="input", MODE="0660"
```
This will add read and write permission to root and the input groupe for the input- and event- device files created by udev!  
Next add yourself to the input group and reload udev:
```bash
$ sudo usermod -aG input $USER
$ newgrp input

$ sudo udevadm control --reload && sudo udevadm trigger
```
To make sure everything is changed idealy reboot now or start a new session.
Opening a new terminal and typing:
```bash
$ groups
```
should list `input`.  

Also test if the permissions on the device files are good. It should look like this:
```bash
$ cd /dev/input
$ ll
Permissions  Size User Group Date Modified  Name         
crw-rw----  13,64 root input  5 Jun 10:57   event0
crw-rw----  13,65 root input  5 Jun 10:57   event1
...
```

So let's setup the script.  
The script is in the demo's [gitea repo](https://git.magnusku.de/Magnus/p4wnp1_gb_autoplay) in the `key_extendr` directory.

To build this we need some dependencies:
- You will need pyinstaller on your system, it will take care of the scripts dependencies though! 
- The `uinput` kernelmodule must be installed as we need to manually include it's `.so` library.

Run the following to clone the project:
```bash
$ git clone https://git.magnusku.de/Magnus/p4wnp1_gb_autoplay
$ cd p4wnp1_gb_autoplay/key_extendr 
```

The script detects the Usb stick by its name which you can set under `Product Name` in the P4wnP1's web ui. 
Edit the scripts `DEV_NAME_FRAG` variable to contain an unique fragment within the name you chose!  

Then bundle the script, python vm and dependencies into an binary using pyinstaller:
```bash
$ make all 
```
The resulting binary can be found at `build/key_extendr`. Add that to the payload!


### 4. Building the Image
Once everything is in place, the payload directory should look like this:

```bash
root@kali:/usr/local/P4wnP1/helper# ls *
genimg
payload:
key_extendr  MGBA.appimage  POKY.gb
```

If it does, create the FAT32 image as before:

```bash
$ ./genimg -i ./payload -o mario -l MARIO -s 2048
```

Next, enable mass storage.

## Payload Preparation
Now onto the payload!
