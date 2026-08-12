# RubberDucky Installation

## Flashing CircuitPython

So how do we set this thing up?

First, we need to flash a firmware to the chip — in our case [CircuitPython](https://circuitpython.org/).

1. Download the `.uf2` file [here](https://circuitpython.org/board/waveshare_rp2040_zero/).
2. Hold the BOOT button on the RP2040 while plugging it into your PC. This will mount the board as a drive.
3. Drop the downloaded image into that drive and you're done!

## Installing the Code

Our code is hosted on [Gitea here](https://git.magnusku.de/Magnus/ruber-ducky).

Start by creating a local copy anywhere on your computer:

```bash
$ git clone https://git.magnusku.de/Magnus/ruber-ducky
```

Then plug in your microcontroller.

If you're on Linux, execute `flash.sh` from the project directory. It will detect the mount point and copy the project files over automatically.

On Windows, you'll need to do this manually.

That should be all!

## How to Debug

Now that the RubberDucky is armed, we need another way to update the code without triggering it.

For this purpose, there is a check on boot (in `boot.py`) that enables debug mode when GPIO pin 0 is pulled to ground. This stops keystroke injection and enables drive mounting for code access.

Simply connect the two pins with a jumper before plugging the board into your PC.

The board's LED will blink blue when debug mode is enabled.
