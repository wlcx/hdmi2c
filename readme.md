# HDMI2C Monitor Controller

HDMI2C allows network control (via WiFi) of monitors connected to it via HDMI (via
[DDC]). This allows you to build your own tooling and control systems for your monitors,
rather than relying on awkward inconvient buttons and OSDs. Think of it as an API for
your monitors.

This repository contains the hardware design, made with [KiCAD]. You can see the
generated BOM and schematic [here][pages].

## What could you build with this

- A physical brightness knob
- Switch inputs of both monitors simultaneously when you wake up your desktop PC or
  connect your laptop to your dock
- IDK probably some other weird shit

## Features

- ESP32 WiFi MCU
- USB-C power and MCU serial connection
  - With blinkenlights
- Two HDMI ports with:
  - Level shifters to bring 5v DDC signals to 3.3v for the MCU.
  - 5v HDMI presence detection, switchable from the MCU. This allows us to fake being
    unplugged and replugged from HDMI, if we need to.
- Two forward facing buttons

## Firmware

It's floating around somewhere, I'll tidy it up and upload it at some point.

## A word on monitor compatibility

Not all monitors implement DDC that well. Particularly of annoyance, some models I
tested would not listen to DDC commands on inputs that were not active, which, given
this project relies on you having a spare HDMI input which never carries any video, is
kind of a deal breaker.

### Known good monitors

- Dell U2515h - I personally have two of these and they work flawlessly.

## Improvements for next rev

- Just use M3 mounting holes, M2.5 was a terrible idea
- Spare ESP32 IO broken out to headers for ease of hacking
- More ambitious, HDMI passthrough to allow use of the project without taking up a whole
  spare HDMI port.

## Is it that useful tho?

You can achieve the same thing without having to build your own hardware with a
Raspberry Pi 4. Support for dual monitor I2C (DDC) was added shortly before I started
this project - guess I didn't check enough :-). This is a much more accessible means to
achieve the same goal. However, if you want a more minimal solution that doesn't require
an entire embedded linux system, this project may be for you.

[DDC]: https://en.wikipedia.org/wiki/Display_Data_Channel
[KiCAD]: https://kicad.org
[pages]: https://wlcx.github.io/hdmi2c
