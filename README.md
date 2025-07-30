# Colemak w/CapsLock
This is just a set of patches to Add the Colemak layout but with
active Caps Lock key instead of remmaping it to backspase/delete key.

It's not a ton of work but I coudn't find anyone that did this, so
I created this mini repo.

The X11 version is added as a variant for the US keyboard.

The VT(tty) version is just the Colemak layout modified in 1 line,
pressing `<S-Caps_Lock>` (or any modifier for that matter) will input backspace
## Install the VT layout
`# cp colemak-capsVT.acc.kbd /usr/share/vt/keymaps/`  
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

this exact location may vary from system to system. Not sure. It is there in FreeBSD
### activate it
then to activate it just:
`$ kbdmap`
and select it from the menu

alternatively change the `keymap` variable from the /etc/rc.conf to:
`keymap="colemak-capsVT.acc.kbd`

## To install the X11 layout
first find where the directory X11/xkb is in your system.
as per the nature of X11 configurations, it could be in various places.
it **WILL** vary from system to system.
In my case I moved all my X11 configuration
to */usr/local/share/X11*.
### Find the X11/xkb folder that your system uses
To do this just do a dry startx run
`$ startx > test 2>&1` with no .xinitrc file and look throug the "test" file
*alternatively read the manpage with `man xorg.conf`*

### Install the patches
> I moved all my X11 configuration to *usr/local/share/X11*
so, to install the patches I would have to:
```
# patch /usr/local/share/X11/xkb/rules/evdev.lst X11/xkb-rules-evdev.lst.patch
# patch /usr/local/share/X11/xkb/rules/evdev.xml X11/xkb-rules-evdev.xml.patch
# patch /usr/local/share/X11/xkb/symbols/us      X11/xkb-symbols-us.patch`  
```
### Activate it
```
$ setxkbmap -layout us -variant colemak_caps
```
Should work like a charm. To make it definitive,
you may modify the
`11/xorg.conf.d/00-keyboard.conf` or `11/xorg.conf` file (it is recommended to use the directory but
fell free to do whatever).

Here at 5.4.5 there's an example 00-keyboard.conf
[FreeBSD Handbook - Configuring Xorg](https://docs.freebsd.org/en/books/handbook/x11/#x-config)
