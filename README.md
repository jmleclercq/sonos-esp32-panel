# ESP32 Sonos Touch Panel for Home Assistant

This project creates a simple Sonos control panel using the Sunton ESP32-2432S028R touchscreen display and ESPHome.

The panel connects to Home Assistant and displays live information from a Sonos speaker while providing basic touch controls.

Current features:

- Display current Sonos state
- Display current track title
- Display current artist
- Touch controls for:
  - Volume down
  - Pause
  - Volume up

The project was tested with a Sonos Arc entity:

media_player.arc


--------------------------------------------------

Hardware

- Sunton ESP32-2432S028R
- 2.8 inch touchscreen (ILI9341)
- XPT2046 resistive touchscreen controller
- 5V power supply
- USB data cable


--------------------------------------------------

Software stack

- ESPHome
- Home Assistant
- Sonos Home Assistant integration


--------------------------------------------------

Current status

Working:

- display initialization
- touchscreen input
- Home Assistant API connection
- Sonos metadata display
- working touchscreen controls

Known limitations:

- a vertical blue strip appears on the right side of the display depending on the driver configuration


--------------------------------------------------

Project structure

Example structure:

.
├── README.md
└── esphome
    └── sunton-28-sonos-panel.yaml


--------------------------------------------------

Secrets example

Example secrets.yaml:

wifi_ssid: "YOUR_WIFI"
wifi_password: "YOUR_PASSWORD"
fallback_password: "CHANGE_ME"


--------------------------------------------------

Installing ESPHome on Linux

Create a Python virtual environment:

python3 -m venv .venv
source .venv/bin/activate

Install ESPHome:

pip install esphome


--------------------------------------------------

Compile firmware

esphome compile esphome/sunton-28-sonos-panel.yaml


--------------------------------------------------

Flash firmware

USB device example:

esphome run esphome/sunton-28-sonos-panel.yaml --device /dev/ttyUSB0

or

esphome run esphome/sunton-28-sonos-panel.yaml --device /dev/ttyACM0


--------------------------------------------------

What has been validated

During testing the following was confirmed:

- the screen initializes correctly
- the touchscreen coordinates are detected
- Home Assistant connects successfully
- Sonos metadata is received
- Home Assistant actions triggered from ESPHome work correctly


--------------------------------------------------

Next improvements

Planned improvements:

- improve UI layout
- better handling of long text
- play/resume button
- Sonos favorites
- improved graphics
- possible migration to LVGL interface


--------------------------------------------------

License

Add your preferred license (MIT recommended).
