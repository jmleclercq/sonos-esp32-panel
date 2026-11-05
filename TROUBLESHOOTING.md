# Troubleshooting

Common issues with the ESP32 Sonos Touch Panel and how to fix them.

## Screen stays white

Possible causes:
- wrong display model
- SPI misconfiguration
- unstable power

Fixes:
- keep the display model set to `ESP32-2432S028`
- verify the display SPI pins: CLK = GPIO14, MOSI = GPIO13, MISO = GPIO12
- use a stable 5V supply

## Colors look wrong (inverted, blue tint)

The `mipi_spi` driver uses the `ESP32-2432S028` preset. If colors look inverted or red and blue are swapped on your board revision, try adding `invert_colors: true` (or `false`) and `color_order: bgr` (or `rgb`) to the `display` block, one change at a time.

## Touchscreen not working or misaligned

- verify the touch SPI pins: CLK = GPIO25, MOSI = GPIO32, MISO = GPIO39
- adjust `calibration` (`x_min`, `x_max`, `y_min`, `y_max`) and `transform` (`mirror_x`, `mirror_y`, `swap_xy`) in the `touchscreen` block
- touch coordinates are visible in the logs at `DEBUG` level: press the corners of the screen to calibrate

Buttons and the slider are LVGL widgets, so no separate touch zones need to be configured.

## Screen does not wake

Touching the clock page runs the `wake_up` script. If it does not wake, check that the touchscreen works (see above) and that the `clock_page` still has its `on_press` action.

## Clock too dark or screen goes black in sleep

Sleep brightness is set in the `go_to_sleep` script (`brightness: 55%`). Increase it if the clock is hard to read. Keep `default_transition_length: 0s` on the backlight light to avoid a delayed or flashing clock.

## Screen never sleeps

Expected while Sonos is `playing`: the panel stays awake during playback. It sleeps 30 seconds after the last touch when Sonos is paused or idle.

## No album art

Check the logs for `online_image` lines.

- `ha_url` must be in `secrets.yaml`, reachable from the panel, without trailing slash (for example `http://192.168.1.100:8123`)
- the Sonos entity must expose `entity_picture` (not the case on the TV source)
- the format must stay `PNG`: Home Assistant serves PNG, and JPEG decoding would need the whole file in one memory block (`allocation of ... bytes failed`)
- a fallback icon is shown whenever the download fails

## Old artist or cover remains on the TV source

Home Assistant removes artist and picture attributes on the TV input, and the panel clears them by checking the `source` attribute. If your TV input is not named `TV`, update the check in the `refresh_media` script. The logs print the value as `Sonos source: '...'`.

## Weird characters

Fonts use the Google `GF_Latin_Core` glyph set, which covers French accents and typographic apostrophes. If a character is missing, add the glyphs it needs to the `font` blocks.

## Display is slow warnings in logs

`online_image ... took a long time for an operation` appears while a cover is decoded. It is normal and short.

## GPIO12 warning

`GPIO12 is a strapping pin` is normal on this board and safe to ignore.

## Sonos not responding

Check the Home Assistant entity name (`player` in the `substitutions` block, default `media_player.arc`).

## WiFi issues

Check `wifi_ssid` and `wifi_password` in `secrets.yaml`.

## Power issues

Symptoms: reboots, white screen, unstable behavior. Use a stable 5V supply or a USB power bank.

## General advice

- change one thing at a time
- keep a backup of a working YAML
