# Troubleshooting

This document lists common issues encountered with the ESP32 Sonos Touch Panel and how to fix them.

## Screen stays white

Possible causes:
- wrong display model
- SPI misconfiguration
- incorrect wiring if not using the original board

Solutions:
- ensure model is set to:
      ESP32-2432S028
- verify SPI pins:
      CLK  = GPIO14
      MOSI = GPIO13
      MISO = GPIO12
- check power supply with stable 5V

## Touchscreen not working

Possible causes:
- incorrect SPI config for touch
- bad calibration values
- wrong transform

Solutions:
- verify touch SPI:
      CLK  = GPIO25
      MOSI = GPIO32
      MISO = GPIO39
- adjust calibration:
      x_min / x_max
      y_min / y_max
- check transform:
      mirror_x / mirror_y

## Touch works but buttons are not aligned

Cause:
- calibration mismatch

Fix:
- adjust these values:
      x_min
      x_max
      y_min
      y_max

Tip:
- use logs to read raw touch values
- press corners of the screen to calibrate

## Buttons trigger wrong actions

Cause:
- touch zones do not match display layout

Fix:
- adjust:
      x_min / x_max / y_min / y_max
  inside binary_sensor blocks

Important:
- do not change display layout if everything works
- only adjust touch zones

## Screen does not wake properly

Cause:
- missing wake logic or touch handling

Fix:
- ensure:
      on_touch:
        - script.execute: wake_screen_only

- ensure debounce logic with:
      just_woke flag

## Screen goes black instead of showing clock

Cause:
- backlight too low

Fix:
- increase standby brightness:
      brightness: 30%

Typical working range:
- 25% to 40%

## Clock appears briefly then disappears

Cause:
- backlight too low or transition delay

Fix:
- set:
      default_transition_length: 0s

- increase brightness

## Screen never sleeps

Cause:
- Sonos state is still:
      playing

Explanation:
- this is expected behavior in the current stable version
- the panel is designed to stay awake while music is playing

## Screen sleeps too soon after pause

Cause:
- no touch activity since playback stopped

Explanation:
- the current logic sleeps after 30 seconds when Sonos is not playing
- this is intended behavior

## Weird characters or accent issues

Cause:
- unsupported glyphs in font
- Sonos metadata contains special characters

Fix:
- use normalized text already implemented in YAML
- ensure glyph list includes apostrophes:
      '
      ’

Note:
- Sonos sometimes sends typographic apostrophes

## Text display glitches

Cause:
- long strings or encoding issues

Fix:
- text is split into 2 lines automatically
- current limits are:
      title: 18 chars
      artist: 20 chars

## Display is slow warnings in logs

Message:
      display took a long time

Cause:
- complex drawing

Status:
- normal behavior
- no action required

## GPIO12 warning

Message:
      GPIO12 is a strapping pin

Explanation:
- normal on ESP32
- safe if not externally pulled

Action:
- ignore warning

## Sonos not responding

Check:
- Home Assistant entity name

Default:
      media_player.arc

Fix:
- replace with your own entity if needed

## WiFi issues

Check:
- credentials in secrets.yaml

Verify:
      wifi_ssid
      wifi_password

## Power issues

Symptoms:
- reboot
- white screen
- unstable behavior

Fix:
- use stable 5V power supply
- or USB power bank

Note:
- using a power bank is the simplest and recommended solution for portable use
- a dedicated battery circuit is not part of this project

## General advice

- if everything works, do not modify working parts
- change only one thing at a time
- always keep a backup of your stable YAML
