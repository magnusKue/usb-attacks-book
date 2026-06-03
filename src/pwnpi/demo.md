{{#title P4wnP1 Demo}}

# Demo
To show the capabilities of this setup we've decided to create a small demo, with the P4wnP1 loading a rom (Super Mario Land) and gameboy emulator via MSC and starting to play it. 

## Sorage preparation
Start of by preparing the needed files:
```bash
root@kali:/usr/local/P4wnP1/helper# ls *
genimg

payload:
MGBA.appimage  SML.gb
```
the payload consists of a legally aquired copy of `Super Mario Land (Rev 1)` and an appimage of the mgba emulater downloaded [here](https://github.com/mgba-emu/mgba/releases/download/0.10.5/mGBA-0.10.5-appimage-x64.appimage)

then create the payload as done before:
```bash
$ ./genimg -i ./payload -o mario -l WORKFILES -s 2048
```
Next enable mass storage emulation and continue with the HID payload.
