# ESP32 Sonos Touch Panel

A stable ESPHome project for a Sunton ESP32 2.8" touchscreen display used as a dedicated Sonos controller in Home Assistant.

This repository documents the first stable working version before visual improvements.

## Stable features

- Sonos state display
- Track title display
- Artist display
- Touch controls:
  - Previous track
  - Play / Pause
  - Next track
  - Volume down
  - Volume up
- Unicode cleanup for Sonos metadata
- Stable touchscreen mapping
- Stable portrait layout

## Hardware

Tested with:

- Sunton ESP32-2432S028
- 2.8" TFT screen
- XPT2046 touchscreen controller

## Software stack

- ESPHome
- Home Assistant
- ESP-IDF

## Project structure

.
├── README.md
├── TROUBLESHOOTING.md
└── esphome
    └── sunton-28-sonos-panel.yaml

## Main configuration file

esphome/sunton-28-sonos-panel.yaml

## Home Assistant entity used

This version is configured for:

media_player.arc

If your Sonos entity has a different name, replace every occurrence of:

media_player.arc

in the YAML.

## Stable interface layout

Top area:
- SONOS ARC header
- state
- title
- artist

Bottom area:
- PREV / PLAY / NEXT
- volume - / +

## Important notes

### 1. This is the stable reference version

This version is intentionally frozen because:

- the display works
- the touchscreen mapping works
- Sonos commands work
- text normalization is good enough for daily use

Future improvements should be built from this version.

### 2. Unicode cleanup

Some Sonos metadata may contain typographic apostrophes or accented characters that do not render perfectly on ESPHome fonts.

A normalization function is included to reduce these display issues.

### 3. GPIO warnings

ESPHome may warn that some GPIOs are strapping pins, especially GPIO12.

This is expected on this board and does not prevent the project from working with the current setup.

## Flashing from Home Assistant

1. Copy the YAML into:

/config/esphome/sunton-28-sonos-panel.yaml

2. Make sure your ESPHome secrets are available:
- wifi_ssid
- wifi_password

3. Install or update the device from ESPHome Builder.

## Git workflow used for this stable version

Typical workflow:

git add .
git commit -m "Stable version: Sonos ESP32 touch panel working"
git push

## Roadmap

Planned future improvements after this stable checkpoint:

- better UI design
- improved text handling for long titles
- volume bar
- album artwork
- LVGL interface
- sleep mode
- auto brightness

## License

MIT
