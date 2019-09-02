# SPDX-License-Identifier: GPL-2.0+
# Copyright (c) 2004 Thomas Sailer <sailer@ife.ee.ethz.ch>
# Copyright (c) 2005-2006 David Brownell <dbrownell@users.sourceforge.net>
# Copyright (c) 2009 Kay Sievers <kay.sievers@vrfy.org>
# Copyright (c) 2009 Greg Kroah-Hartman <gregkh@suse.de>

SUBDIRS = \
	usbhid-dump

AM_LDFLAGS = \
	-Wl,--as-needed

data_DATA =

bin_PROGRAMS = \
	lsusb

sbin_SCRIPTS =

bin_SCRIPTS = \
	usb-devices \
	lsusb.py

noinst_PROGRAMS = \
	usbreset

lsusb_SOURCES = \
	lsusb.c lsusb.h \
	lsusb-t.c \
	list.h \
	desc-defs.c desc-defs.h \
	desc-dump.c desc-dump.h \
	names.c names.h \
	usbmisc.c usbmisc.h

lsusb_CPPFLAGS = \
	$(AM_CPPFLAGS) $(LIBUSB_CFLAGS) \
	-DDATADIR=\"$(datadir)\"

lsusb_LDADD = \
	$(LIBUSB_LIBS)

usbreset_SOURCES = \
	usbreset.c

if HAVE_ZLIB
lsusb_CPPFLAGS += -DHAVE_LIBZ
lsusb_LDADD += -lz
endif

man_MANS = \
	lsusb.8	\
	usbhid-dump.8 \
	usb-devices.1

EXTRA_DIST = \
	usb.ids \
	update-usbids.sh.in \
	lsusb.8.in \
	usbhid-dump.8.in \
	usb-devices.1.in \
	usb-devices \
	lsusb.py.in \
	usbreset.c \
	LICENSES/GPL-2.0.txt \
	LICENSES/GPL-3.0.txt

lsusb.py: $(srcdir)/lsusb.py.in
	sed 's|VERSION|$(VERSION)|g;s|@usbids@|$(datadir)/usb.ids|g' $< >$@
	chmod 755 $@

if INSTALL_USBIDS
data_DATA += usb.ids

if HAVE_ZLIB
data_DATA += usb.ids.gz
endif

sbin_SCRIPTS += update-usbids.sh

usb.ids.gz: $(srcdir)/usb.ids
	gzip -c -9 $< > $@

update-usbids.sh: $(srcdir)/update-usbids.sh.in
	sed 's|@usbids@|$(datadir)/usb.ids|g' $< >$@
	chmod 755 $@
endif

lsusb.8: $(srcdir)/lsusb.8.in
	sed 's|VERSION|$(VERSION)|g;s|@usbids@|$(datadir)/usb.ids|g' $< >$@

usbhid-dump.8: $(srcdir)/usbhid-dump.8.in
	sed 's|VERSION|$(VERSION)|g' $< >$@

usb-devices.1: $(srcdir)/usb-devices.1.in
	sed 's|VERSION|$(VERSION)|g' $< >$@

DISTCLEANFILES = \
	usb.ids.gz \
	lsusb.py \
	lsusb.8 \
	usb-devices.1 \
	usbhid-dump.8 \
	update-usbids.sh \
	usbutils.pc

distclean-local:
	rm -rf autom4te.cache
