# Raspberry PISA

Inspired by the Raspberry Pi [Virtual Floppy for ISA (PC XT/AT) project](https://www.smbaker.com/raspberry-pi-virtual-floppy-for-isa-pc-xtat-computers), __Raspberry PISA__ aims to implement a Pi-based [compatibility card](https://en.wikipedia.org/wiki/Compatibility_card) for DOS compatible sytems. This will allow vintage / retro machines to temporarily be turned into modern systems, allowing you to enjoy using older hardware for all kinds of things (among a set of other planned features).

## Motivation
Having amassed a collection of vintage computers that I love to maintain and use, I often wondered how a modern desktop environment would look and feel to use on these older systems, especially those using CGA displays, Plasma Display Panels, big thonky keyboards and esoteric input devices.

I see many people resorting to create "sleeper" builds / conversion mods of older machines to get this experience (and to have a bit of fun along the way), where they gut the original hardware and replace it with current-gen parts. I'm __not__ a fan of this, in many cases the original hardware works just fine! What if there was a way to switch between the original hardware and a Raspberry Pi?

## How it Works / What it Does

The Raspberry Pi communicates with the DOS-based host machine over the ISA bus and emulates a keyboard, mouse, additional serial port (for networking or file transfer) and DMA for the purpose of sending a low resolution framebuffer.

The project is made up of the following components:
- A Raspberry Pi Zero.
- An 8 or 16-bit ISA card capable of mounting the Raspberry Pi (along with other components).
- Driver and control software for DOS (PC-DOS / DR-DOS / MS-DOS 3.x or greater).
- A custom Raspberry Pi Zero image that contains the relevant control software for Linux.
- `.deb` packages for the Raspberry Pi Zero for installation on DIY distributions.
- _(Optional)_ A USB WiFi card for remote network access.
- _(Optional)_ A USB mouse if you don't have one that works directly on your DOS machine.


The aim is to provide the following functionality:
- Display a graphical frame-buffer of the Raspberry Pi on the DOS machine (via DMA) at a defined graphics mode and resolution. This will take over the display on the host DOS machine until a configurable escape sequence is pressed on the keyboard.
- Bi-directional input device support. Access host DOS machine's keyboard and mouse on the Raspberry Pi and vice-versa (for USB HID support). This feature will by default, automatically activate when the frame-buffer is enabled.
- Bi-directional network proxy support. Give your DOS machine WiFi capabilities via ISA, or give your Raspberry Pi access to a token ring network.
- File access / transfer. Access your DOS machine on the network via NFS/Samba via the Raspberry Pi.
- A card configuration utility to correctly set up memory / IRQ / DMA channels.

The ISA card will have the following ports for connectivity:
- One USB 2.0 port for a WiFi card, mouse, keyboard, USB drive, USB hub.
- A power LED to indicate the status of the Raspberry Pi.
- An activity LED to indicate communication between the DOS machine and the Raspberry Pi.
- A power switch to disable the ISA card when not needed.

## Requirements
Initially, the aim will be to support 286-based systems and above with a 16-bit ISA card, and at least one usable / free 16-bit ISA DMA channel. Mouse support will be via the Microsoft Mouse drivers over serial. There will need to be  Features will be built-out in order of the feature list described above.