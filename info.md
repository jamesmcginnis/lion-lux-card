# Lion Lux Card

A compact pill card for Home Assistant that shows current lux levels at a glance. Tap to open a full overview popup — see each sensor's current reading and tap any sensor to view its 24-hour history.

## Key Features

- **Compact pill design** — a slim 56px card shows the average lux level across all configured sensors (e.g. *Avg 320 lx · 2 Bright*, *Avg 45 lx · All Low*); optional title label
- **Pill fill bar** — a proportional fill behind the pill grows as lux levels rise, with a configurable fill colour and a configurable fill-max ceiling
- **Auto-detection** — automatically finds all `sensor` domain entities with device class `illuminance` or unit of measurement `lx` in your Home Assistant instance
- **Bright threshold** — set your own lux threshold to define what counts as Bright; sensors at or above this value are highlighted in your chosen High colour
- **Sensor overview popup** — tap the pill to open a popup showing each sensor as its own pill with its current lux reading; tap the Bright stat pill to highlight matching sensors in the grid
- **Average and peak stats** — the overview shows a live average and peak reading across all sensors
- **Sensor detail popup** — tap any sensor pill in the overview to open its individual detail popup, showing current lux, sensor type, unit, threshold, and last-updated time
- **Live history** — tap the *Last updated* row in the detail popup to view a 24-hour lux timeline showing readings most recent first
- **Group by Area** — optionally group sensors into their Home Assistant areas in the overview popup
- **Friendly names** — assign a custom display name to any sensor directly in the visual editor
- **Drag-to-reorder** — drag selected sensors in the visual editor to set the order they appear in the popup
- **Full colour control** — eight colour pickers: Pill Background, Text, Accent, Pill Fill, High, Low, Popup Background and Sensor Icon

## Quick Start

```yaml
type: custom:lion-lux-card
entities:
  - sensor.living_room_illuminance
  - sensor.garden_lux
  - sensor.bedroom_illuminance
title: Light Levels
high_threshold: 1000
accent_color: '#FFD60A'
fill_color: '#FFD60A'
high_color: '#FF9F0A'
```

All settings can be configured through the built-in visual editor — no YAML editing required!
