# ESP32 Sonos Touch Panel

<p align="center">
<img src="https://img.shields.io/badge/ESP32-Sunton%202.8%22-blue?logo=espressif" />
<img src="https://img.shields.io/badge/ESPHome-supported-000000?logo=esphome" />
<img src="https://img.shields.io/badge/Home%20Assistant-integrated-41BDF5?logo=homeassistant" />
<img src="https://img.shields.io/badge/Sonos-controller-black?logo=sonos" />
<img src="https://img.shields.io/badge/License-MIT-green" />

</p>

<p align="center">
Dedicated Sonos touchscreen controller using an ESP32 Sunton display and ESPHome.
</p>


# ESP32 Sonos Touch Panel

![ESPHome](https://img.shields.io/badge/ESPHome-supported-blue)
![Home Assistant](https://img.shields.io/badge/Home%20Assistant-compatible-41BDF5)
![ESP32](https://img.shields.io/badge/ESP32-supported-orange)
![License](https://img.shields.io/badge/license-MIT-green)

A standalone **ESP32 touchscreen controller for Sonos**, powered by **ESPHome** and integrated with **Home Assistant**.

![Sonos Touch Panel](images/sonos-touch-panel.jpg)

--------------------------------------------------

OVERVIEW

This project implements a dedicated Sonos controller using a Sunton ESP32-2432S028 2.8" touchscreen display with ESPHome integrated into Home Assistant.

The panel displays:

- Sonos playback state
- Track title
- Artist name

Touch controls:

- Previous track
- Play / Pause
- Next track
- Volume down
- Volume up

This repository documents the first stable version of the project.

--------------------------------------------------

HARDWARE

Tested with:

Sunton ESP32-2432S028

Features:

- ESP32 microcontroller
- 2.8" TFT display
- XPT2046 touchscreen controller
- SPI display interface

--------------------------------------------------

SOFTWARE STACK

- ESPHome
- Home Assistant
- ESP-IDF framework

--------------------------------------------------

PROJECT STRUCTURE

.
├── README.md
├── TROUBLESHOOTING.md
└── esphome
    ├── sunton-2432s028r-sonos.yaml
    └── secrets.example.yaml

--------------------------------------------------

ESPHOME CONFIGURATION

Main configuration file:

esphome/sunton-2432s028r-sonos.yaml

This file includes:

- display configuration
- touchscreen calibration
- Sonos Home Assistant integration
- Unicode text normalization
- touch button mapping

--------------------------------------------------

HOME ASSISTANT ENTITY

The configuration uses the Sonos entity:

media_player.arc

If your entity has a different name, replace every occurrence of media_player.arc inside the YAML file.

--------------------------------------------------

CONFIGURATION

Copy the example secrets file:

cp esphome/secrets.example.yaml esphome/secrets.yaml

Edit the file with your WiFi credentials:

wifi_ssid: "YOUR_WIFI"
wifi_password: "YOUR_PASSWORD"

--------------------------------------------------

INTERFACE LAYOUT

Top section

- SONOS ARC header
- playback state
- track title
- artist

Bottom section

- PREV | PLAY | NEXT
- volume - | volume +

Touching these areas sends commands to Home Assistant.

--------------------------------------------------

NOTES

Stable reference version

This repository represents a stable working baseline:

- display works correctly
- touchscreen mapping works
- Sonos commands work
- text normalization handles most metadata issues

Future improvements should build from this version.

--------------------------------------------------

UNICODE HANDLING

Sonos metadata sometimes contains typographic characters such as apostrophes or accents.

The YAML includes a normalization function to reduce display artifacts.

--------------------------------------------------

GPIO WARNINGS

ESPHome may warn about strapping pins (GPIO12).

This is expected on this board and does not affect normal operation.

--------------------------------------------------

FLASHING

1. Copy the YAML file to your ESPHome configuration folder:

/config/esphome/sunton-2432s028r-sonos.yaml

2. Ensure secrets are configured.

3. Install the device from ESPHome Builder in Home Assistant.

--------------------------------------------------

GIT WORKFLOW

Typical workflow:

git add .
git commit -m "Update configuration"
git push

--------------------------------------------------

ROADMAP

Planned improvements:

- improved UI
- better handling of long titles
- volume slider
- album artwork
- LVGL interface
- screen sleep mode
- automatic brightness

--------------------------------------------------

LICENSE

MIT

