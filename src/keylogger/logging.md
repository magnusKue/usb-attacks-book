# Logging & Data Retrieval

The keylogger stores captured keystrokes in a file on the LittleFS filesystem of the RP2040s flash. This section explains how to access and retrieve the logged data.

## Where Logs Are Stored

- **File path**: `/keylog.txt`
- **Filesystem**: LittleFS (internal flash storage)
- **Buffer**: Keystrokes are first buffered in RAM and flushed to flash every 2 seconds or when the buffer is nearly full.

## Method 1: via Arduino IDE

The easiest way to view logs is via the Arduino Serial Monitor.

### View the Log (DUMP)

1. Open Arduino IDE
2. Go to `Tools -> Port` and select the Pico's serial port
3. Open the **Serial Monitor** (`Tools -> Serial Monitor`)
4. Set baud rate to `115200`
5. Type `DUMP` and press Enter

The entire log file will be printed to the serial output.


6. Type `CLEAR` to clear delete logs


## Method 2: via Python Log Reader

For a more convenient experience with automatic device detection and log cleaning, use the included `reader.py` script.

### Setup

Install the required dependency:

```bash
pip install pyserial
```

### Running the Reader

```bash
python3 reader.py
```

### Features

- **Auto-detection**: Automatically finds RP2040 devices
- **Interactive menu** with four options:
  1. **Read Log (RAW)**: Displays raw log output exactly as sent from the device
  2. **Read Log (Cleaned)**: Processes the log to produce readable text
  3. **Clear Log**: Erases the stored log file
  4. **Exit**: Closes the serial connection and exits