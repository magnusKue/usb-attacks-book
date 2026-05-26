{{#title Overview}}

# Project Overview

For our Offensive Security university module we decided to look into USB-based attacks. How USB devices can be used to attack a computer just by plugging them in. We picked three projects that each show a different way this can be done.

## Why USB Attacks?

USB attacks are surprisingly easy to pull off and hard to defend against. A device that looks like a normal flash drive or even like a cable can start typing on its own, open a shell, or log your keystrokes — all within seconds of being plugged in. We thought that was worth exploring.

## The Three Projects

- ### 1. DIY Rubber Ducky: Keystroke injection, Reverse Shell to C2

    Here we built our own Rubber Ducky, a well known USB attack tool that emulates a keyboard. Once plugged in, it types out a payload on its own and in our case opens a reverse shell back to a C2 server, giving us remote access to the target machine. We realized this project using an RP2040 with CircuitPython.

- ### 2. P4wnP1 ALOA: HID + Mass Storage emulation

    This builds on the Rubber Ducky idea but uses a Raspberry Pi Zero W running P4wnP1 ALOA, a full blown USB-hacking environment. This allows for both keystroke injection and storage emulation at the same time, making the attack harder to detect and allowing for more complex ones.

- ### 3. DIY Hardware Keylogger: Intercepting keystrokes

    This is a small custom PCB built around an RP2040 microcontroller <!-- TODO: add board name here --> that sits between a keyboard and a computer and records every keystroke. No software needed on the target — just plug it in and it works.

## What This Book Is

This book contains tutorials for setting up all three projects. It was written for our university module and is meant for educational purposes only.
