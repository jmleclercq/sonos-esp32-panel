# Troubleshooting

This file documents the main issues encountered while building the Sonos ESP32 touch panel and the solutions that led to the current stable version.

---

## 1. Display worked but had blue bands / wrong rendering

### Symptoms
- blue vertical band
- partial display
- mirrored or reversed text
- white screen after some display model changes

### Cause
The display driver and board preset needed to match the real Sunton board behavior.

### Stable solution
Use:

- platform: mipi_spi
- model: ESP32-2432S028

This fixed the display layout and removed the blue-band issue in the stable version.

---

## 2. Touchscreen worked in logs but buttons were triggered in the wrong place

### Symptoms
- touch events appeared in logs
- visible buttons did not match actual touch zones
- PREV / NEXT and volume buttons could be inverted

### Cause
Touchscreen calibration and axis transform did not initially match the final portrait display orientation.

### Stable solution
Use the final stable touchscreen transform:

transform:
  swap_xy: false
  mirror_x: true
  mirror_y: false

and keep the final working button coordinates from the stable YAML.

---

## 3. Buttons triggered the wrong Sonos action

### Symptoms
- touching one button triggered another action
- volume up / volume down inverted
- previous / next inverted

### Cause
Display layout and touch coordinate system were mirrored relative to each other.

### Stable solution
Keep the current stable binary_sensor coordinates exactly as frozen in the repository.

---

## 4. Home Assistant actions did not work

### Symptoms
- touch logs were visible
- no actual reaction on Sonos

### Cause
ESPHome device permissions in Home Assistant / ESPHome were not fully enabled at one stage.

### Stable solution
Allow the ESPHome device to perform Home Assistant actions and use homeassistant.action in the YAML.

---

## 5. Accent or apostrophe rendering produced squares / artifacts

### Symptoms
- little rectangles after accented characters
- apostrophes displayed incorrectly
- Unicode rendering inconsistent depending on metadata

### Cause
Sonos metadata can include typographic apostrophes and Unicode variants that do not always map cleanly to the selected ESPHome font glyphs.

### Stable solution
Keep the current stable font block and the normalization logic inside the text_sensor lambdas.

The stable version converts problematic characters into simpler equivalents before display.

---

## 6. ESPHome font errors about duplicate glyphs or missing glyphs

### Symptoms
- duplicate glyph errors
- missing glyph \n
- font compilation failures

### Cause
Using multiline glyphs blocks incorrectly can introduce hidden newline characters or duplicate symbols.

### Stable solution
Use single-line glyphs definitions exactly as in the stable YAML.

Do not reintroduce multiline glyph blocks.

---

## 7. GitHub push failed with password authentication

### Symptoms
- push rejected
- password authentication not supported

### Cause
GitHub no longer allows standard password authentication for Git over HTTPS.

### Solution
Use SSH remote or a personal access token.

Recommended:

git remote set-url origin git@github.com:USERNAME/REPO.git
git push --set-upstream origin master

---

## 8. Branch had no upstream

### Symptoms
- git push failed with:
- current branch master has no upstream branch

### Solution

git push --set-upstream origin master

After that, a simple git push works.

---

## 9. Stable baseline rule

Once display, touch mapping and Sonos actions are working:

- do not change fonts unnecessarily
- do not change display model unnecessarily
- do not change touch transforms unless testing is intentional
- improve visuals only from the frozen stable version

This repository now documents that stable baseline.
