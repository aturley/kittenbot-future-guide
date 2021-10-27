# Kittenbot Future Guide

An unofficial guide to the [KittenBot Future board](https://www.kittenbot.cc/products/future-board-esp32-aiot-python-education-kit)

## Overview

The KittenBot Future board is an ESP32-based IoT development board. It has:
* wifi
* an LCD screen
* two physical buttons
* an accelerometer
* a compass
* a thermometer
* a humidity sensor
* a light sensor
* three built-in NeoPixel lights

The board can be programmed using the [KittenBlock](https://www.kittenbot.cc/pages/software) development environment, using either a [Scratch](https://scratch.mit.edu/)-based visual language or directly in [MicroPython](https://docs.micropython.org/en/latest/esp32/quickref.html).

Most of the documentation is in Chinese. This documention is unoffical and is an attempt to help share information about the system with English-speakers.

## KittenBlock

The folks at Kittenbot seem to want you to use KittenBlock to program the device. In theory you should be able to connect over a serial port, but I haven't gotten that to work yet.

### Getting Started

Once you fire KittenBlock up you're presented with a Scratch-like IDE. There's a top bar where you can select a device and connect to it. Find the board selection menu and select "Future". Then plug in your device and connect to it by clicking on the section that says "Not Connected", selecting "Serial" and then selecting your device. Then click on the switch that says "Coding" so that it now says "Stage". You are now ready to begin programming your Kittenbot Future board.

## Python Examples

### Read a Button Using a Callback

```python
#/bin/python
from future import *

def on_btn_a():
  screen.fill((255, 255, 255))
  screen.text("button a pressed",5,10,1,(0, 119, 255))

def on_btn_b():
  screen.fill((255, 255, 255))
  screen.text("button b pressed",5,10,1,(0, 119, 255))

sensor.btnTrig['a']=on_btn_a
sensor.btnTrig['b']=on_btn_b
sensor.startSchedule()

screen.fill((255, 255, 255))
```

### Use the Radio to Send and Receive Messages

```python
#/bin/python
from future import *

from radio import *
x = 0

def on_btn_a():
  global r
  r.send('a')

def on_btn_b():
  global r
  r.send('b')

def on_recv(m, x):
  screen.fill((255, 255, 255))
  screen.text("got: " + m.decode('utf8'),5,10,1,(0, 119, 255))

sensor.btnTrig['a']=on_btn_a
sensor.btnTrig['b']=on_btn_b
sensor.startSchedule()

r = Radio()

r.channel = 12

r.onRecv = on_recv

screen.fill((255, 255, 255))
```
