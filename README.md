# Logitech Webcam Light

This script automatically turns a [Logitech Litra Glow](https://www.logitech.com/en-us/shop/p/litra-glow) light on and off when a webcam is in use

## Quick Start

* Install dependencies

```
sudo apt install python3-usb
```

* Give access to the device by creating `/etc/udev/rules.d/99-litra.rules`

```
SUBSYSTEM=="usb", ATTR{idVendor}=="046d", ATTR{idProduct}=="c900",MODE="0666"
SUBSYSTEM=="usb", ATTR{idVendor}=="046d", ATTR{idProduct}=="c901",MODE="0666"
```

* Download and run the [logitech_webcam_light](logitech_webcam_light) script with the name of your webcam e.g.

```
./logitech_webcam_light /dev/video0
```

* Open an app that uses your webcam, the light should turn on. Close the app and the light should turn off.

## Usage

```
usage: logitech_webcam_light [-h] webcam

Logitech Webcam Light

positional arguments:
  webcam      The webcam to watch for activity e.g. /dev/video0

options:
  -h, --help  show this help message and exit
```

## Run in systemd

Create a systemd service at `~/.config/systemd/user/logitech-webcam-light.service`

```
[Unit]
Description=Logitech Webcam Light

[Service]
ExecStart=/path/to/logitech_webcam_light
Restart=always
RestartSec=60

[Install]
WantedBy=default.target
```

Enable and start the service

```
systemctl --user enable logitech-webcam-light.service
systemctl --user start logitech-webcam-light.service
```

## License

Distributed under the GNU General Public License v3.0. See `LICENSE` for more information.

## Author

Written by [Kieren Beckett](http://kierenb.net).
