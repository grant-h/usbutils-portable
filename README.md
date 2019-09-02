<!---
SPDX-License-Identifier: GPL-2.0+
Copyright (c) 2018 Greg Kroah-Hartman <gregkh@linuxfoundation.org>
-->
# usbutils

This is a collection of USB tools for use on Linux and BSD systems to
query what type of USB devices are connected to the system.  This is to
be run on a USB host (i.e. a machine you plug USB devices into), not on
a USB device (i.e. a device you plug into a USB host.)

## Portability (by @grant-h)
Upstream usbutils has a hard dependency on udev, which makes it incompatible with anything except Linux.
Removing the dependency on udev and restoring the USB IDs database parsing makes `lsusb` only depend on `libusb`.
Some `sysfs` files are used for extra info such as which kernel driver is loaded for a USB interface, but otherwise,
only libusb descriptors are needed.

A list of changes made to make usbutils portable is visible here: https://github.com/grant-h/usbutils-portable/compare/upstream...master
Build instructions remain the same.

### What's working

* Tested on macOS 10.14 with libusb installed via Homebrew
* Not currently tested on Windows / WSL / Ubuntu on Windows (coming soon)
* `lsusb` plain works well on Mac
* `lsusb -v` works well, minus any `sysfs` reads
* `usbhid-dump` default mode works

### What's not
* `lsusb -t` does NOT work due to a hard dependency on `sysfs`
* `usbreset` does NOT work as it depends on `sysfs`

## Building and installing

Note, usbutils depends on libusb, be sure that library is properly
installed first.

To work with the "raw" repo, after cloning it just do:

	./autogen.sh

Or if you like doing things "by hand" you can try the following:

Get the usbhid-dump git submodule:

	git submodule init
	git submodule update

Initialize autobuild with:

	autoreconf --install --symlink

Configure the project with:

	./configure

Build everything with:

	make

Install it, if you really want to, with:

	make install
