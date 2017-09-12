# Freifunk Monitor

# What to do if Freifunk appears to be down

## Log on

1. Connect the C.H.I.P. via USB to a Mac and execute `screen /dev/tty.usbmodem*`. It will bring up a serial console (via USB).
1. Log on (you may have to press Enter before that, so that the login prompt appears). Default username and password are `chip`.
1. When done, exit `screen` with `Control-a`, `Control-d` (where `Control-a` is `screen`'s prefix).

## Check the WiFi connection

The C.H.I.P. is connected to the Freifunk network via WiFi. Use `nmcli` to check and, if necessary restart, the networking on the chip:

* `nmcli n connectivity` should report `full`.
* If it is `none`, restart the network with `sudo sh -c "nmcli n off; nmcli n on"`

Optionally, check the IP address assigned with `ip address show wlan0`.

1. `sudo TERM=linux nmtui`
1. Select "Activate a connection" adnd then "Freifunk".
1. If that doesn't help, unplug the Freifunk router's power cable to make it reboot.
