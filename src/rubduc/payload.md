# The Payload

## Structure

As seen on the last page, the payload is defined in `src/inputs.py` and selected by setting the `payload` variable in `code.py`.

Let's look at an example:

```python
# src/inputs.py
hello_world = [
    ("SLEEP", 0.2),
    ("LED", (0,255,0)),
    ("SLEEP", 0.2),
    ("WRITE", "Hello World"),
    ("SLEEP", 0.1),
]

# code.py
payload = inputs.hello_world
```

This script first sets the color of the on-board LED to an RGB value, then types out `Hello World`.

There are multiple actions used here — let's look at all of them:  

| Key     | Value                                                              |
|---------|--------------------------------------------------------------------|
| `SLEEP`   | Sleep for `v` seconds                                              |
| `PRESS`   | Press and hold key `v` (Adafruit HID keycode: `Keycode.<key>`)    |
| `SEND`    | Press and release key `v` (Adafruit HID keycode: `Keycode.<key>`) |
| `WRITE`   | Type out the string `v`                                            |
| `RELEASE` | Release all keys. No value needed, so set to `None`               |
| `LED`     | Change the LED color to RGB tuple `v`                              |
