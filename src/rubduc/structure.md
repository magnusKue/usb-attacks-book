# Project structure


## Project files

Maybe this would be a good point to look at the files you just put on your board.  


| File/Directory    | Purpose |
| -------------- | --------------- |
| `boot.py` | This runs early in the boot process. We use this file to enable debug mode if needed.
| `code.py` | Entrypoint of the code |
| `src/*.py` | Modules that are imported in code.py |
| `src/inputs.py` | This is where you define your keyboard inputs. Different routines can be defined. One of them later is selected in code.py via the payload variable. |
| `lib/` | This directory contains some third party libraries for HID and the onboard LED |
| `serial.sh` | This will not be copied onto the board but it can be used to read out the serial bus! |
