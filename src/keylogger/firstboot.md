# First Boot & Verification

After flashing the firmware, the keylogger should be ready to run. This section walks you through verifying that everything is working correctly.

## Power On the Device

1. Connect the RP2040 to your target computer via USB.
2. The 5V LED should light up.
3. The device will enumerate as a HID keyboard device.

## Verify Device Recognition

Check if the device is recognized:

```bash
$ lsusb
```

You should see an entry for the RP2040. 

```bash 
Bus 001 Device 076: ID 239a:cafe Adafruit Feather RP2040 USB Host
``` 

## Test Keyboard Functionality

1. Open a text editor (e.g., `nvim`).
2. Type some characters on the Keyboard.
3. The device should function as a normal keyboard