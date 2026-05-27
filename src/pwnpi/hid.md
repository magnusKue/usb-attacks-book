# HID Injection

Next we want to set up HID injection. In this chapter you will learn how to write custom scripts and deploy them using trigger actions.

HID is enabled by default so there is no need to configure anything. If you have turned it off, just re-enable `keyboard` and `mouse` in the `USB SETTINGS` tab.

## 1. Writing a First Script

Scripts are located at `/usr/local/P4wnP1/HIDScripts`, but you can also use the Web UI for editing.

Scripts are written in JavaScript using custom functions provided by P4wnP1 ALOA. We won't go in-depth on everything that's possible as that would blow the scope of this tutorial, but here are some basics to get started.

### Useful Functions

#### Keyboard Actions

| Function | Action | Parameters |
| --------------------------------- | ------------------------------------ | --------------------------------------------------------------- |
| `layout("US");`                   | Set keyboard layout                  | Country code (`us`, `de`, `gb`, `fr`, `es`, `it`, `br`, `ru`)  |
| `typingSpeed(delay, jitter);`     | Set typing speed                     | Base delay in ms; additional random jitter in ms                |
| `delay(ms);`                      | Wait for a short time                | Duration in ms                                                  |
| `type("text\n");`                 | Type out a string                    | Text; `\n` is interpreted as RETURN, uppercase triggers SHIFT   |
| `press("KEY1 KEY2");`             | Press multiple keys at once          | Space-separated key names; full list [here](https://github.com/RoganDawes/P4wnP1_aloa/blob/master/README.md) |
| `waitLED(NUM);`                   | Wait for a keyboard LED state change | `NUM`, `CAPS`, `SCROLL`, `ANY`, `ANY_OR_NONE`, or combined with `\|` |
| `waitLEDRepeat(ANY);`             | Wait for repeated LED toggling       | Same filters as `waitLED`; useful to trigger on intentional human input |

#### Mouse Actions

| Function | Action |
| ---------------------------- | ----------------------------------------- |
| `move(dx, dy);`              | Fast, imprecise relative movement         |
| `moveStepped(dx, dy);`       | Slow, precise relative movement (1 DPI steps) |
| `moveTo(x, y);`              | Absolute positioning (Windows only)       |
| `click(BT1\|BT2);`           | Click a button                            |
| `doubleClick(BT1\|BT2);`     | Double-click a button                     |
| `button(BT1\|BT2\|BTNONE);`  | Press and hold or release a button        |


For more advanced scripting, take a look at `/usr/local/P4wnP1/HIDScripts/helper.js` which contains a bunch of useful utility functions.
