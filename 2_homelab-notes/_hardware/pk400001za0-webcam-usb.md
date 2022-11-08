---
title:  "pk400001za0 Webcam To USB"
intro: "It's easy to convert some laptop camera modules to connect to USB."
description: "Converting a pk400001za0 laptop camera module to a USB webcam"
tags: "pk400001za0,usb,webcam,camera"
date: "2020-04-06"
---

The pk400001za0 webcam module is commonly found in Acer and Lenovo laptops and is detected as "Suyin Corp. Acer/Lenovo Webcam [CN0316]" in Linux Mint.

It's fairly easy to wire this module to connect to a USB port on a computer, there's a good tutorial here ([https://www.youtube.com/watch?v=g8XbDJLKKys](https://www.youtube.com/watch?v=g8XbDJLKKys)), below are my notes from when I did this.

### Pinout

Lay the module front of you with the wire harness (where all the wires come out) facing away from you.

Since the wire colours aren't consistent from one machine to another, I've gone ahead and numbered the pins in the diagram below to make this easier: 


```
| | | | |
| | | | |  <-- wires
1-2-3-4-5  <-- pins
|       |
|       |
|       |
|       |
| ( o ) <----- camera 
|       |
|       |
|       |
|       |
---------
```


### Wiring to USB

_Note that the Power is at around 3.9 volts, since USB delivers 5 volts we'll have to drop the voltage slightly. I used a couple Rectifier Diodes as was suggested in the video I linked above._

|pk400001za0 Pin|Description|USB Wire Colour|
|-|-|-|
|1|not used|not used|
|2|Ground|Black|
|3|Data +|Green|
|4|Data -|White|
|5|Power ~3.9V|Red/Pink ~5.0V  **__You _need to decrease the voltage_ using Rectifier Diodes or similar, failure to do so may damage the camera module__ **|

### Try it out

If you're using Linux, plug it in then hit the terminal and type `lsusb`, if successful you should see something like:

```bash
~ lsusb   
Bus 001 Device 031: ID 064e:a102 Suyin Corp. Acer/Lenovo Webcam [CN0316]
```
