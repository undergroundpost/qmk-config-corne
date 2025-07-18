# Corne 4.1 QMK Firmware (6-Column Colemak)

This repository contains the QMK configuration for my **Corne (CRKBD) 4.1** split keyboard, running custom firmware built using [QMK](https://qmk.fm/). The layout is based on **Colemak**, inspired by the principles of [Miryoku](https://github.com/manna-harbour/miryoku) — minimal finger travel, home-row mods, and layered functionality. The outer columns are disabled for a cleaner 5-column effective layout.

## Hardware

- **Keyboard**: Corne 4.1 (5-column variant)
- **Firmware**: [QMK Firmware](https://qmk.fm/)
- **Layout Style**: Colemak, Miryoku-inspired
- **Transport**: USB-C wired connection
- **MCU**: RP2040 (Raspberry Pi Pico)

---

## Features

- ✅ **Home row modifiers** (mod-tap) on Colemak base with fine-tuned timing
- 🎯 **Tap dance** for bracket pairs: `()`, `[]`, `{}`
- 🔢 **Five dedicated layers**: Base, Numpad, Navigation, Media, Function
- 🧠 Thoughtful layer design for ergonomic workflows
- 🔐 All modifiers and layer access within thumb reach
- 🖥️ **OLED displays** with WPM counter and animated character
- 🎛️ **Encoder support** for volume/media control
- ⚡ **Per-key tapping terms** optimized for each home row modifier

---

## Layer Overview

### 🅱 Base Layer (Colemak)

- Miryoku-style home-row mods:
  - Left: `A`=Ctrl, `R`=Alt, `S`=Cmd, `T`=Shift
  - Right: `N`=Shift, `E`=Cmd, `I`=Alt, `O`=Ctrl
- Thumb keys: NAV/Tab, Backspace, NUMPAD/Enter, Space, FUNCTION/Quote, MEDIA/Grave
- Outer columns disabled for clean 5-column layout

### 🔢 Numpad Layer

- Left side: Numpad layout with operators (`*`, `/`, `+`, `-`, `=`)
- Right side: Symbols and brackets with tap dance
  - `TD(BRKT1)`: Single tap `(`, double tap `)`
  - `TD(BRKT2)`: Single tap `[`, double tap `]`
  - `TD(BRKT3)`: Single tap `{`, double tap `}`
- Additional symbols: `!`, `@`, `#`, `# Corne 4.1 QMK Firmware (6-Column Colemak)

This repository contains the QMK configuration for my **Corne (CRKBD) 4.1** split keyboard, running custom firmware built using [QMK](https://qmk.fm/). The layout is based on **Colemak**, inspired by the principles of [Miryoku](https://github.com/manna-harbour/miryoku) — minimal finger travel, home-row mods, and layered functionality. The outer columns are disabled for a cleaner 5-column effective layout.

## Hardware

- **Keyboard**: Corne 4.1 (5-column variant)
- **Firmware**: [QMK Firmware](https://qmk.fm/)
- **Layout Style**: Colemak, Miryoku-inspired
- **Transport**: USB-C wired connection
- **MCU**: RP2040 (Raspberry Pi Pico)

---

## Features

- ✅ **Home row modifiers** (mod-tap) on Colemak base with fine-tuned timing
- 🎯 **Tap dance** for bracket pairs: `()`, `[]`, `{}`
- 🔢 **Five dedicated layers**: Base, Numpad, Navigation, Media, Function
- 🧠 Thoughtful layer design for ergonomic workflows
- 🔐 All modifiers and layer access within thumb reach
- 🖥️ **OLED displays** with WPM counter and animated character
- 🎛️ **Encoder support** for volume/media control
- ⚡ **Per-key tapping terms** optimized for each home row modifier

---

## Layer Overview

, `%`, `^`, `&`

### 🧭 Navigation Layer

- Arrow keys in vim-style layout (left side)
- Escape key for quick access
- Clean and minimal navigation focus

### 🔧 Function Layer

- F-keys arranged in logical grid (F1-F12)
- Tap dance controls:
  - `DT_UP`/`DT_DOWN`: Adjust tap dance timing
  - `DT_PRNT`: Print tap dance settings

### 🎵 Media Layer

- Volume controls: Vol Down, Mute, Vol Up
- Media playback: Previous, Play/Pause, Next
- Positioned on right side for easy thumb access

---

## Custom Behaviors

### 🏠 Home Row Modifiers

```c
// Left-hand mods
#define HOME_A LCTL_T(KC_A)
#define HOME_R LALT_T(KC_R)
#define HOME_S LGUI_T(KC_S)
#define HOME_T LSFT_T(KC_T)

// Right-hand mods  
#define HOME_N RSFT_T(KC_N)
#define HOME_E RGUI_T(KC_E)
#define HOME_I LALT_T(KC_I)
#define HOME_O RCTL_T(KC_O)
```

- Per-key optimized tapping terms:
  - `A`/`O` (Ctrl): `TAPPING_TERM + 40ms` (slower)
  - `R`/`I` (Alt): `TAPPING_TERM + 30ms`
  - `S`/`E` (Cmd): `TAPPING_TERM - 10ms`
  - `T`/`N` (Shift): `TAPPING_TERM - 20ms` (faster)

### 🎯 Tap Dance Actions

```c
tap_dance_action_t tap_dance_actions[] = {
    [BRKT1] = ACTION_TAP_DANCE_DOUBLE(LSFT(KC_9), LSFT(KC_0)),    // ( )
    [BRKT2] = ACTION_TAP_DANCE_DOUBLE((KC_LBRC), (KC_RBRC)),      // [ ]
    [BRKT3] = ACTION_TAP_DANCE_DOUBLE(LSFT(KC_LBRC), LSFT(KC_RBRC)), // { }
};
```

- Single tap: Opening bracket
- Double tap: Closing bracket
- Enables rapid bracket entry without holding shift

### 🖥️ OLED Features

- **Master side**: WPM counter with animated character
- **Slave side**: Current layer indicator
- **WPM-responsive animation**: Character changes based on typing speed
  - Idle: Below 10 WPM
  - Prep: 10-30 WPM  
  - Active: Above 30 WPM

### 🎛️ Encoder Support

```c
// Volume/media controls on all layers
ENCODER_CCW_CW(KC_VOLD, KC_VOLU)
ENCODER_CCW_CW(KC_MPRV, KC_MNXT)
```

---

## Building and Flashing

> ⚠️ Ensure your environment is configured per [QMK documentation](https://docs.qmk.fm/).

### Prerequisites

```bash
# Install QMK CLI
pip3 install qmk
qmk setup
```

### Build and Flash

```bash
# Build the firmware
qmk compile -kb crkbd/rev1 -km your_keymap_name

# Flash to keyboard (enter bootloader mode first)
qmk flash -kb crkbd/rev1 -km your_keymap_name
```

### Bootloader Mode

- **Physical**: Hold BOOT button while plugging in USB-C
- **Keycode**: Use `QK_BOOT` key combination (if configured)
- **Command**: `qmk flash` will wait for bootloader automatically

---

## Configuration

## Configuration

### Features Enabled

```c
// In rules.mk
OLED_ENABLE = yes          # Enable OLED displays
WPM_ENABLE = yes           # Enable WPM calculation
TAP_DANCE_ENABLE = yes     # Enable tap dance functionality
ENCODER_ENABLE = yes       # Enable rotary encoder support
SPLIT_KEYBOARD = yes       # Split keyboard support
EXTRAKEY_ENABLE = yes      # Audio control and system control
MOUSEKEY_ENABLE = no       # Mouse keys disabled
CONSOLE_ENABLE = no        # Console for debug
COMMAND_ENABLE = no        # Commands for debug and configuration
NKRO_ENABLE = yes          # N-Key Rollover
RGBLIGHT_ENABLE = no       # RGB underlight disabled
AUDIO_ENABLE = no          # Audio output disabled
```

### Keymap-Specific Settings

```c
// In config.h (recommended)
#define TAPPING_TERM 200              // Base tapping term
#define PERMISSIVE_HOLD              // Aggressive mod-tap behavior
#define TAPPING_FORCE_HOLD           // Force hold on repeated taps
#define IGNORE_MOD_TAP_INTERRUPT     // Prevent accidental mod triggers
```

---

## Keymap Visualization

> 💡 **Tip**: Generate visual keymap diagrams using [`keymap-drawer`](https://github.com/caksoylar/keymap-drawer) or the [Corne Layout Editor](https://config.qmk.fm/#/crkbd/rev1/LAYOUT_split_3x6_3).

```bash
# Generate keymap diagram with keymap-drawer
keymap parse -c 10 -z keymap.c > keymap.yaml
keymap draw keymap.yaml > keymap.svg
```

The 6-column layout with disabled outer columns provides the clean aesthetics of a 5-column board while maintaining the standard Corne PCB compatibility.

## Customization

### Adding a New Layer

```c
// In keymap.c - add to enum
enum layers {
    _BASE,
    _NUMPAD,
    _NAV,
    _MEDIA,
    _FUNCTION,
    _CUSTOM     // Your new layer
};

// Add layer in keymaps array
[_CUSTOM] = LAYOUT_split_3x6_3(
    XXXXXXX, _______, _______, _______, _______, _______,                    _______, _______, _______, _______, _______, XXXXXXX,
    XXXXXXX, _______, _______, _______, _______, _______,                    _______, _______, _______, _______, _______, XXXXXXX,
    XXXXXXX, _______, _______, _______, _______, _______,                    _______, _______, _______, _______, _______, XXXXXXX,
                               _______, _______, _______,                    _______, _______, _______
),
```

### Modifying Tap Dance

```c
// Add new tap dance actions
enum tap_dance_codes {
    BRKT1,
    BRKT2,
    BRKT3,
    CUSTOM_TD  // Your custom tap dance
};

// Define behavior
[CUSTOM_TD] = ACTION_TAP_DANCE_DOUBLE(KC_COMM, KC_SCLN),
```

### Adjusting Home Row Timing

```c
// In get_tapping_term() function
case HOME_A:
    return TAPPING_TERM + 50;  // Make it slower/faster
```

### Adding Your Own Layer

```c
// In keymap.c
enum layers {
    _BASE,
    _LOWER,
    _RAISE,
    _ADJUST,
    _CUSTOM  // Your new layer
};

// Add layer in keymaps array
[_CUSTOM] = LAYOUT_split_3x5_3(
    // Your custom layout here
),
```

### Modifying Combos

```c
// In combos.def or keymap.c
COMB(combo_name, KC_OUTPUT, KC_INPUT1, KC_INPUT2)
```

---

## Troubleshooting

### Common Issues

- **Split halves not syncing**: Check TRRS cable connection and ensure both halves are flashed
- **OLED not displaying**: Verify `OLED_ENABLE = yes` in rules.mk and check wiring
- **Home row mods triggering accidentally**: Adjust `TAPPING_TERM` values in `get_tapping_term()`
- **Tap dance not working**: Ensure `TAP_DANCE_ENABLE = yes` and check tap timing
- **Encoder not responding**: Verify `ENCODER_ENABLE = yes` and encoder wiring
- **USB-C not detected**: Try different cable or port, ensure proper USB-C connection

### Debug Tips

```c
// Enable console output for debugging (in rules.mk)
CONSOLE_ENABLE = yes

// Check WPM calculation
sprintf(wpm_str, "WPM:%03d", get_current_wpm());
```

---

## License

MIT License – see `LICENSE`.  
Built on the excellent work of the QMK and Miryoku communities.

---

## Credits

- **QMK Firmware**: [QMK Contributors](https://github.com/qmk/qmk_firmware)
- **Miryoku Layout**: [Manna Harbour](https://github.com/manna-harbour/miryoku)
- **Corne Keyboard**: [foostan](https://github.com/foostan/crkbd)

---

## Author

Custom layout and configuration by [undergroundpost].
