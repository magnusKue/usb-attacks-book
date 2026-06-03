# Keylogger Installation & Setup

This guide is written for an Arch Linux setup. If you are using Windows, this guide does not cover that environment.

## Arduino IDE Installation

Install the Arduino IDE using:

```bash
yay -S arduino-ide-bin
```

## Clone the Repository

Clone the project repository and open it in the Arduino IDE:

```bash
git clone https://git.magnusku.de/David_Heunisch/Keylogger.git
```

## Initial Setup

After cloning, connect your controller to the computer.

### Board Installation

In the Arduino IDE:

- Go to `Tools -> Board -> Boards Manager`
- Search for:  
  `Raspberry Pi Pico/RP2040/RP2350 by Earle F. Philhower`
- Install the package

### Library Installation

Go to `Tools -> Manage Libraries` and install the following:

- Neopixel (1.15.5)
- Adafruit SPI Flash (5.1.1)
- Adafruit TinyUSB Library (3.7.7)
- MIDI Library (3.7.7)
- PICO PIO USB (0.7.2)
- SdFAT (Adafruit Fork) (2.3.103)

### IDE Configuration

Configure the following settings:

- **Port**  
  Select the UF2 device for the first setup. After flashing, switch to the normal serial port.

- **CPU Speed**  
  Must be divisible by 12. Recommended: 240 MHz.

- **Flash Size**  
  Allocate space for LittleFS logging. Recommended: 3–4 MB.

- **USB Stack**  
  Set to: Adafruit TinyUSB

## Flashing the Firmware

Click the **Upload** button in the bottom-left corner of the Arduino IDE and wait for the compilation and flashing process to complete.