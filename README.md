# Corne 4.1 QMK Firmware (6-Column Colemak)

This repository contains the QMK configuration for my **Corne (CRKBD) 4.1** split keyboard, running custom firmware built using [QMK](https://qmk.fm/). The layout is based on **Colemak**, inspired by the principles of [Miryoku](https://github.com/manna-harbour/miryoku) — minimal finger travel, home-row mods, and layered functionality. The outer columns are disabled for a cleaner 5-column effective layout.

## Hardware

- **Keyboard**: Corne 4.1 (6-column with outer columns disabled)
- **Firmware**: [QMK Firmware](https://qmk.fm/)
- **Layout Style**: Colemak, Miryoku-inspired
- **MCU**: RP2040 (Raspberry Pi Pico)
- **Connection**: USB-C wired

---

## Features

- ✅ **Home row modifiers** with per-key optimized timing
- 🎯 **Tap dance** for bracket pairs: `()`, `[]`, `{}`
- 🔢 **Five dedicated layers**: Base, Numpad, Navigation, Media, Function
- 🖥️ **OLED displays** with WPM counter and bongo cat animation
- 🎛️ **Encoder support** for volume/media control
- 🧠 Ergonomic thumb cluster layer access

---

## Layer Overview

### 🅱 Base Layer (Colemak)

- **Home-row mods**: `A`=Ctrl, `R`=Alt, `S`=Cmd, `T`=Shift | `N`=Shift, `E`=Cmd, `I`=Alt, `O`=Ctrl
- **Thumb cluster**: NAV/Tab, Backspace, NUMPAD/Enter, Space, FUNCTION/Quote, MEDIA/Grave

### 🔢 Numpad Layer
- **Left**: Traditional numpad with operators (`*`, `/`, `+`, `-`, `=`)
- **Right**: Symbols and tap dance brackets
  - `TD(BRKT1)`: `(` / `)`
  - `TD(BRKT2)`: `[` / `]`  
  - `TD(BRKT3)`: `{` / `}`

### 🧭 Navigation | 🔧 Function | 🎵 Media
- **NAV**: Arrow keys + Escape
- **FUNCTION**: F1-F12 + tap dance controls
- **MEDIA**: Volume and playback controls

---

## Custom Behaviors

### 🏠 Home Row Modifiers
```c
// Optimized per-key tapping terms
HOME_A/O (Ctrl): TAPPING_TERM + 40ms
HOME_R/I (Alt):  TAPPING_TERM + 30ms  
HOME_S/E (Cmd):  TAPPING_TERM - 10ms
HOME_T/N (Shift): TAPPING_TERM - 20ms
```

### 🎯 Tap Dance Brackets
```c
[BRKT1] = ACTION_TAP_DANCE_DOUBLE(LSFT(KC_9), LSFT(KC_0)),    // ( )
[BRKT2] = ACTION_TAP_DANCE_DOUBLE((KC_LBRC), (KC_RBRC)),      // [ ]
[BRKT3] = ACTION_TAP_DANCE_DOUBLE(LSFT(KC_LBRC), LSFT(KC_RBRC)), // { }
```

### 🖥️ OLED Features
- **Master (Left)**: WPM Counter + Bongo Cat Animation
  - **Idle (0-10 WPM)**: Cat sits peacefully, slowly breathing
  - **Prep (10-30 WPM)**: Cat gets ready, paws positioned over drums
  - **Active (30+ WPM)**: Cat energetically plays the bongos!

![Bongo Cat Animation](images/bongo_cat.png)

*Bongo cat responds to your typing speed - the faster you type, the faster he drums!*

- **Slave (Right)**: Current layer indicator (BASE, NUM, NAV, MEDIA, FUN)

---

## Building and Configuration

### Build Commands
```bash
# Build and flash
qmk compile -kb crkbd/rev1 -km your_keymap_name
qmk flash -kb crkbd/rev1 -km your_keymap_name
```

### Key Features Enabled
```c
// rules.mk
OLED_ENABLE = yes          # OLED displays
WPM_ENABLE = yes           # WPM calculation  
TAP_DANCE_ENABLE = yes     # Tap dance functionality
ENCODER_ENABLE = yes       # Rotary encoder support
SPLIT_KEYBOARD = yes       # Split keyboard support
```

### Recommended Settings
```c
// config.h
#define TAPPING_TERM 200              # Base tapping term
#define PERMISSIVE_HOLD              # Aggressive mod-tap
#define IGNORE_MOD_TAP_INTERRUPT     # Prevent accidental triggers
```

---

## Customization

### Add New Layer
```c
enum layers { _BASE, _NUMPAD, _NAV, _MEDIA, _FUNCTION, _CUSTOM };

[_CUSTOM] = LAYOUT_split_3x6_3(
    XXXXXXX, _______, _______, _______, _______, _______,    _______, _______, _______, _______, _______, XXXXXXX,
    // ... your layout
),
```

### Adjust Timing
```c
// In get_tapping_term()
case HOME_A: return TAPPING_TERM + 50;  // Slower/faster
```

---

## Troubleshooting

**Split sync issues**: Check TRRS cable  
**OLED not working**: Verify `OLED_ENABLE = yes`  
**Accidental mod triggers**: Adjust tapping terms  
**USB-C detection**: Try different cable/port

---

## Keymap Visualization

Generate diagrams using [`keymap-drawer`](https://github.com/caksoylar/keymap-drawer):
```bash
keymap parse -c 10 -z keymap.c > keymap.yaml
keymap draw keymap.yaml > keymap.svg
```

---

## License

MIT License – see `LICENSE`.  
Built on the excellent work of the QMK and Miryoku communities.

## Credits

- **QMK Firmware**: [QMK Contributors](https://github.com/qmk/qmk_firmware)
- **Miryoku Layout**: [Manna Harbour](https://github.com/manna-harbour/miryoku)
- **Corne Keyboard**: [foostan](https://github.com/foostan/crkbd)

## Author

Custom layout and configuration by [undergroundpost].
