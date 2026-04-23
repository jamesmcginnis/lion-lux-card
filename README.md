# Lion Lux Card

A compact pill card for Home Assistant that shows current lux / illuminance levels at a glance. Tap to open a full overview popup — see each sensor's current reading and tap any sensor to view its 24-hour history timeline.

![Home Assistant](https://img.shields.io/badge/Home%20Assistant-2024.1+-blue)
![HACS](https://img.shields.io/badge/HACS-Custom-orange)
![License](https://img.shields.io/badge/license-MIT-green)

[![Open your Home Assistant instance and add this repository to HACS.](https://my.home-assistant.io/badges/hacs_repository.svg)](https://my.home-assistant.io/redirect/hacs_repository/?owner=jamesmcginnis&repository=lion-lux-card&category=plugin)

---

## ✨ Features

### Pill Card
- **Compact pill design** — a slim 56px card shows the average lux level and how many sensors are currently bright (e.g. *Avg 320 lx · 2 Bright*, *Avg 45 lx · All Low*, *Avg 2.4k lx · All Bright*)
- **Pill fill bar** — a proportional tinted fill behind the card grows from left to right as the peak lux level rises; configurable fill colour and fill-max ceiling
- **Optional title** — show a label on the pill, or leave it blank to show just the readings
- **Frosted-glass popups** — smooth slide-up and scale animations, fully customisable colours
- **Mobile optimised** — touch-friendly tap targets designed for iPhone dashboards

### Sensor Overview Popup
- **Stats bar** — shows Bright count, live average, and current peak across all configured sensors; tap the Bright pill to highlight matching sensors in the grid
- **Sensor pills** — each sensor is shown as its own tappable pill with its current lux reading; bright sensors display in your configured high colour, dim sensors are muted
- **Live sun icons** — each sensor pill shows a full or dimmed sun icon reflecting the real-time brightness state
- **Group by Area** — optionally group sensors by their Home Assistant area, with a labelled section per area
- **Tap to open detail** — tap any sensor pill to open its individual detail popup

### Individual Sensor Detail Popup
- **State circle** — large indicator reflecting the sensor's current brightness; filled and glowing when bright, dimmed when low
- **Live lux value** — prominent lux reading that updates in real time as Home Assistant reports state changes
- **Type row** — shows the sensor's Home Assistant device class (Illuminance, etc.)
- **Unit row** — shows the unit of measurement reported by the sensor (lx, etc.)
- **Bright threshold row** — shows the configured threshold at which a sensor is classed as Bright
- **Last updated row** — shows how long ago the sensor last reported a value; tap it to open a 24-hour history timeline
- **Live updates** — the popup reflects state changes from Home Assistant in real time without needing to be reopened

### Sensor History
- Tap the *Last updated* row in the detail popup to open a 24-hour history timeline
- History is fetched live from the Home Assistant history API
- Each entry shows the lux value, date and time, and how long the sensor stayed at that reading
- Entries are shown most recent first
- Readings at or above the bright threshold are highlighted in your accent colour

### Visual Editor
- **Auto-detected sensors** — all `sensor` entities with device class `illuminance` or unit of measurement `lx` are shown automatically with a type badge
- **Search and filter** — type to instantly filter the sensor list
- **Toggle to select** — tap the toggle next to any sensor to add or remove it
- **Drag-to-reorder** — drag selected sensors using the grip handle to set the order they appear in the popup
- **Friendly names** — expand any selected sensor to set a custom display name
- **Threshold settings** — configure the Bright threshold and the fill bar maximum directly in the editor
- **Colour control** — eight colour pickers: Pill Background, Text, Accent, Pill Fill, High, Low, Popup Background and Sensor Icon

---

## 🚀 Installation

### HACS (Recommended)

[![Open your Home Assistant instance and add this repository to HACS.](https://my.home-assistant.io/badges/hacs_repository.svg)](https://my.home-assistant.io/redirect/hacs_repository/?owner=jamesmcginnis&repository=lion-lux-card&category=plugin)

1. Open **HACS** in your Home Assistant instance
2. Click **Frontend**
3. Click the ⋮ menu → **Custom repositories**
4. Paste `https://github.com/jamesmcginnis/lion-lux-card` and set the category to **Dashboard**
5. Click **Download**
6. Restart Home Assistant

### Manual Installation

1. Download `lion-lux-card.js`
2. Copy it into your `config/www/` folder
3. Add the resource in your Lovelace configuration:

```yaml
lovelace:
  resources:
    - url: /local/lion-lux-card.js
      type: module
```

4. Restart Home Assistant

---

## ⚙️ Configuration

### Quick Start

1. Edit your dashboard and click **Add Card**
2. Search for **Lion Lux**
3. Use the **visual editor** to select your sensors and configure colours
4. Hit **Save** — done!

### YAML Example

```yaml
type: custom:lion-lux-card
entities:
  - sensor.living_room_illuminance
  - sensor.garden_lux
  - sensor.bedroom_illuminance
  - sensor.office_light_level
title: Light Levels
high_threshold: 1000
fill_max: 10000
accent_color: '#FFD60A'
fill_color: '#FFD60A'
high_color: '#FF9F0A'
low_color: '#48484A'
icon_color: '#FFD60A'
pill_bg: '#1c1c1e'
text_color: '#ffffff'
popup_bg: '#1c1c1e'
friendly_names:
  sensor.living_room_illuminance: Living Room
  sensor.garden_lux: Garden
```

### Configuration Options

| Option | Type | Default | Description |
|--------|------|---------|-------------|
| `entities` | list | `[]` | List of sensor entity IDs to display, in display order |
| `title` | string | _(blank)_ | Label shown on the pill card. Leave blank to hide |
| `group_by_area` | boolean | `false` | Group sensors by their Home Assistant area in the overview popup |
| `high_threshold` | number | `1000` | Lux value at or above which a sensor is classed as Bright |
| `fill_max` | number | `10000` | Lux value at which the pill fill bar reaches 100% |
| `accent_color` | string | `#FFD60A` | Highlight colour for active states and controls |
| `fill_color` | string | `#FFD60A` | Colour of the proportional fill bar |
| `high_color` | string | `#FF9F0A` | Colour used to indicate a sensor is above the bright threshold |
| `low_color` | string | `#48484A` | Colour used to indicate a sensor is below the bright threshold |
| `icon_color` | string | `#FFD60A` | Colour of the sun icon on the pill card |
| `pill_bg` | string | `#1c1c1e` | Background colour of the main pill card |
| `text_color` | string | `#ffffff` | Primary text colour |
| `popup_bg` | string | `#1c1c1e` | Background colour of all popup dialogs |
| `friendly_names` | map | `{}` | Custom display names keyed by entity ID |

---

## 🎨 Colour System

| Field | Default | What it affects |
|-------|---------|----------------|
| **Pill Background** | `#1c1c1e` | The background of the main pill card |
| **Text** | `#ffffff` | Labels and lux text |
| **Accent** | `#FFD60A` | Stat pill highlight, active filters, history entries above threshold |
| **Pill Fill** | `#FFD60A` | The proportional tinted fill bar that grows with lux levels |
| **High** | `#FF9F0A` | Pill icon and state text when a sensor is above the bright threshold |
| **Low** | `#48484A` | State circle border when a sensor is below the bright threshold |
| **Popup Background** | `#1c1c1e` | The background of the overview and detail popups |
| **Sensor Icon** | `#FFD60A` | The sun icon on the pill card |

---

## 💡 How It Works

### Pill Fill
A tinted bar sits behind the pill card content and grows proportionally as the peak lux reading rises — empty when the highest reading is 0 lx, full when it reaches the configured `fill_max`. The fill colour is set independently via `fill_color`.

### Pill Summary
The pill shows the average lux value across all configured sensors alongside a count of how many are currently Bright. The average uses smart formatting — readings above 1000 lx are displayed in compact form (e.g. `2.4k lx`).

### Sensor Overview
Tap the pill card to open the full overview popup. Each sensor is displayed as a pill showing its current lux reading with a live sun icon. Tap the **Bright** stat pill at the top to filter and highlight sensors in the grid. Average and peak readings are shown at a glance. Tap any sensor pill to open its detail popup.

### Sensor Detail
The detail popup shows the sensor's current lux value with a large indicator circle, its device class, unit, the configured bright threshold, and when it last updated. The popup updates live as Home Assistant reports state changes — no need to reopen it.

### Sensor History
Tap the *Last updated* row in any sensor's detail popup to fetch and display the last 24 hours of lux readings directly from the Home Assistant history API. Entries are shown most recent first with timestamps and duration. Readings at or above the bright threshold are highlighted.

### Group by Area
Enable the **Group by Area** toggle in the editor to group sensors by their Home Assistant area in the overview popup. Sensors not assigned to an area appear under a *No Area* section.

### Auto-Detection
The visual editor automatically discovers all `sensor` entities from your Home Assistant instance with a device class of `illuminance` or a unit of measurement of `lx`. These are sorted to the top of the list and shown with a type badge.

---

## 🔍 Supported Sensor Types

The card works with any numeric sensor entity, but is best suited to sensors with:

- `illuminance` device class — standard light level sensors
- `lx` unit of measurement — generic lux reporters

Common compatible devices include Zigbee light sensors (Aqara, IKEA, Sonoff), Z-Wave multi-sensors, and any custom integration reporting lux values.

---

## 🔧 Troubleshooting

**Card doesn't appear after installation**
- Add the resource to Lovelace (see Installation above) and hard-refresh: `Ctrl+Shift+R` / `Cmd+Shift+R`

**No sensors appear in the editor**
- Ensure your entities are in the `sensor` domain with device class `illuminance` or unit of measurement `lx`

**The fill bar is always at 100%**
- Increase the `fill_max` value to better match the typical peak lux readings in your environment

**Popup doesn't open when tapping the pill**
- Ensure at least one entity is configured and that the entity exists in your Home Assistant instance

**History popup shows "No history in the last 24 hours"**
- Ensure the HA history integration is enabled and configured to record the entity. Check **Settings → System → Storage** for recorder configuration

**Keyboard closes while typing on iPhone**
- All text fields save on blur rather than on every keystroke, which prevents HA from rebuilding the editor mid-input. Tap the field, type, then tap elsewhere to save

---

## 📄 License

MIT License — free to use, modify and distribute.

---

## ⭐ Support

If this card is useful to you, please **star the repository** and share it with the community!

For bugs or feature requests, use the [GitHub Issues](../../issues) page.
