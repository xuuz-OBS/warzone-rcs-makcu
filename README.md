# Warzone RCS

A recoil control system for Black Ops 7 / Warzone using MAKCU hardware.

> **For educational purposes only. Use at your own risk.**

---

## Requirements

- MAKCU device
- Dual-PC setup (Bot-PC runs the tool, Main-PC plays the game)
- Python 3.10+

---

## Setup

```
setup.bat
```

Then launch with:

```
run_gui.bat   ← with console
```

---

## Features

### Pattern Editor
- Freehand curve drawing on a canvas
- Load a bullet-hole screenshot as background with adjustable transparency
- Arc-length sampling: draw any curve, enter bullet count → exactly N evenly spaced points are generated
- **Averaging Mode (⊕ Avg):** draw 3 curves over 3 separate spray groups, system averages them into one stable pattern
- Scale X / Scale Y sliders for fine-tuning
- Right-click to clear

### Recoil Control
- Smooth movement via `makcu` Python package (software ease-out interpolation)
- Single worker thread with queue – no move overlap, no MAKCU buffer overload
- Fractional accumulator – sub-integer counts are never lost between shots
- ADS detection: automatically applies zoom multiplier when RMB is held
- Activation button: LMB or RMB
- Toggle bind: assign MB4, MB5 or MMB to toggle RCS on/off from ingame

### Weapon Profiles
- Per-weapon JSON profiles stored in `patterns/`
- Fields: name, category, RPM, magazine size, bullet velocity, DPI, sensitivity, zoom factor, notes
- Magazine auto-syncs to pattern length on save
- Favorites, search, categories
- Duplicate / export weapons

### Sensitivity & FOV
- DPI + in-game sensitivity input → auto-calculates sens factor
- Hipfire FOV input
- ADS zoom factor per weapon (1.0 = iron sights / 1x red dot, 2.0 = 2x, etc.)
- Zoom multiplier calculated via trigonometric FOV formula

### Screenshot Upload Server
- Flask server on port 5000 (start/stop via GUI button)
- Upload bullet-hole screenshots from Main-PC browser to Bot-PC
- Accessible at `http://<bot-pc-ip>:5000`

### GUI
- Dark theme inspired by Black Ops 7
- Sidebar: RCS toggle, toggle bind, strength, delay, ADS multiplier, live shot counter, stats
- Pattern Editor tab + Weapon Stats tab per weapon
- Toast notifications
- No console window when launched via `run_gui.vbs`

---

## Configuration

All settings are saved in `rcs_config.json`. Sensitivity is always calculated live from DPI + in-game sens and never stored directly.

---

## Credits

Developed by xuuz
