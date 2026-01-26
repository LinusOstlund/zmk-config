# ZMK Config - Sofle Choc Pro BT (Swedish Layout)

Personal ZMK firmware configuration for **Keebart Sofle Choc Pro BT** split
keyboard, optimized for **Swedish keyboard layout** on macOS.

## Hardware

- **Keyboard:** Keebart Sofle Choc Pro BT
- **Switches:** Kailh Choc v1 (low-profile)
- **MCU:** nRF52840 (Bluetooth)
- **Displays:** Sharp MiP (nice!view compatible)
- **Encoders:** 2x rotary encoders (volume/media)

## Layout Overview

This is a Swedish-optimized layout. The OS **must be set to Swedish keyboard
layout** for symbols to work correctly.

### Base Layer

```text
┌─────┬─────┬─────┬─────┬─────┬─────┐         ┌─────┬─────┬─────┬─────┬─────┬─────┐
│ ESC │  1  │  2  │  3  │  4  │  5  │         │  6  │  7  │  8  │  9  │  0  │BSPC │
├─────┼─────┼─────┼─────┼─────┼─────┤         ├─────┼─────┼─────┼─────┼─────┼─────┤
│ TAB │  Q  │  W  │  E  │  R  │  T  │         │  Y  │  U  │  I  │  O  │  P  │ ^/~ │
├─────┼─────┼─────┼─────┼─────┼─────┤         ├─────┼─────┼─────┼─────┼─────┼─────┤
│CAPS │  A  │  S  │  D  │  F  │  G  │         │  H  │  J  │  K  │  L  │ +/? │  '  │
├─────┼─────┼─────┼─────┼─────┼─────┤         ├─────┼─────┼─────┼─────┼─────┼─────┤
│SHFT │  Z  │  X  │  C  │  V  │  B  │ [ENC]   │  N  │  M  │ ,;  │ .:  │ -_  │SHFT │
└─────┴─────┼─────┼─────┼─────┼─────┤         ├─────┼─────┼─────┼─────┼─────┴─────┘
            │CTRL │ ALT │ GUI │LW/NV│   SPC    RET   │RAISE│CTRL │ ALT │ GUI │
            └─────┴─────┴─────┴─────┘                └─────┴─────┴─────┴─────┘
```

**Key differences from standard Sofle:**

- ESC top-left, CAPS on home row (where TAB usually is)
- `^/~` next to P (tap-dance: tap=^, double-tap=~)
- `+/?` and `'` on home row (where ö/ä would be on full Swedish keyboard)
- Swedish symbols via combos
- Left thumb = Space, Right thumb = Enter (only Enter location)
- **LW/NV key**: hold = LOWER layer, tap = toggle NAV mode

### Combos

Press keys **simultaneously** (within 50ms) on BASE layer:

| Combo        | Output      | Description           |
| ------------ | ----------- | --------------------- |
| P + ^/~      | å           | Adjacent keys (pos 22+23) |
| L + +/?      | ö           | Roll pinky right (pos 33+34) |
| +/? + '      | ä           | Roll pinky further (pos 34+35) |
| S + P        | Spotlight   | Cmd+Space (pos 26+22) |

### LOWER Layer (Hold LW/NV)

**Hold** LW/NV for navigation and symbols:

```text
┌─────┬─────┬─────┬─────┬─────┬─────┐         ┌─────┬─────┬─────┬─────┬─────┬─────┐
│     │  !  │ "/@ │  #  │  $  │  %  │         │  &  │  |  │ [/{ │ ]/} │  ?  │ DEL │
├─────┼─────┼─────┼─────┼─────┼─────┤         ├─────┼─────┼─────┼─────┼─────┼─────┤
│     │     │     │  ↑  │     │     │         │PGUP │ ←W  │  ↑  │  W→ │     │     │
├─────┼─────┼─────┼─────┼─────┼─────┤         ├─────┼─────┼─────┼─────┼─────┼─────┤
│     │     │  ←  │  ↓  │  →  │     │         │PGDN │  ←  │  ↓  │  →  │  ´  │  *  │
├─────┼─────┼─────┼─────┼─────┼─────┼ [ENC]   ├─────┼─────┼─────┼─────┼─────┼─────┤
│     │  <  │  >  │     │     │     │         │     │     │     │     │  \  │     │
└─────┴─────┴─────┴─────┴─────┴─────┘         └─────┴─────┴─────┴─────┴─────┴─────┘
```

### NAV Layer (Tap LW/NV)

**Tap** LW/NV to toggle navigation lock mode. Tap again or press ESC to exit.

```text
┌─────┬─────┬─────┬─────┬─────┬─────┐         ┌─────┬─────┬─────┬─────┬─────┬─────┐
│     │     │     │     │     │     │         │     │     │     │     │     │     │
├─────┼─────┼─────┼─────┼─────┼─────┤         ├─────┼─────┼─────┼─────┼─────┼─────┤
│EXIT │     │     │     │     │     │         │     │     │  ↑  │     │     │     │
├─────┼─────┼─────┼─────┼─────┼─────┤         ├─────┼─────┼─────┼─────┼─────┼─────┤
│     │     │     │     │     │     │         │     │  ←  │  ↓  │  →  │     │     │
├─────┼─────┼─────┼─────┼─────┼─────┼ [ENC]   ├─────┼─────┼─────┼─────┼─────┼─────┤
│     │     │     │     │     │     │         │     │     │     │     │     │     │
└─────┴─────┼─────┼─────┼─────┼─────┤         ├─────┼─────┼─────┼─────┼─────┴─────┘
            │     │     │     │EXIT │                │     │     │     │     │
            └─────┴─────┴─────┴─────┘                └─────┴─────┴─────┴─────┘
```

Only IJKL arrows are active; everything else passes through to BASE layer.

**Special behaviors:**

| Keys       | Output   | Notes                            |
| ---------- | -------- | -------------------------------- |
| LOWER + 7  | `\|`     | Pipe (single tap)                |
| LOWER + 8  | `[`      | Tap-dance: tap = [               |
| LOWER + 88 | `{`      | Tap-dance: double-tap = {        |
| LOWER + 9  | `]`      | Tap-dance: tap = ]               |
| LOWER + 99 | `}`      | Tap-dance: double-tap = }        |
| LOWER + +/?| `´`      | Acute accent                     |
| LOWER + '  | `*`      | Asterisk                         |
| LOWER + Z  | `<`      | Less than                        |
| LOWER + X  | `>`      | Greater than                     |
| LOWER + -_ | `\`      | Backslash                        |
| LOWER + U  | Word ←   | Option+Left (jump word left)     |
| LOWER + O  | Word →   | Option+Right (jump word right)   |

### RAISE Layer (Right Thumb)

Hold RAISE for BT controls, tilde, and DEL:

```text
┌─────┬─────┬─────┬─────┬─────┬─────┐         ┌─────┬─────┬─────┬─────┬─────┬─────┐
│BTCLR│ BT1 │ BT2 │ BT3 │ BT4 │ BT5 │         │     │     │     │     │     │     │
├─────┼─────┼─────┼─────┼─────┼─────┤         ├─────┼─────┼─────┼─────┼─────┼─────┤
│     │     │     │     │     │     │         │     │     │     │     │     │     │
├─────┼─────┼─────┼─────┼─────┼─────┤         ├─────┼─────┼─────┼─────┼─────┼─────┤
│     │     │     │     │     │     │         │     │     │     │     │ DEL │  ~  │
├─────┼─────┼─────┼─────┼─────┼─────┼ [ENC]   ├─────┼─────┼─────┼─────┼─────┼─────┤
│     │     │ CUT │COPY │PASTE│UNLK │         │     │     │     │     │     │     │
└─────┴─────┴─────┴─────┴─────┴─────┘         └─────┴─────┴─────┴─────┴─────┴─────┘
```

**Special behaviors:**

| Keys         | Output | Notes                           |
| ------------ | ------ | ------------------------------- |
| RAISE + +/?  | DEL    | Delete key                      |
| RAISE + '    | `~`    | Tilde (macro: dead key + space) |
| RAISE + X    | Cut    | K_CUT                           |
| RAISE + C    | Copy   | K_COPY                          |
| RAISE + V    | Paste  | K_PASTE                         |
| RAISE + B    | Unlock | ZMK Studio unlock               |

### ADJUST Layer (LOWER + RAISE)

Hold **both layer keys** together:

```text
┌─────┬─────┬─────┬─────┬─────┬─────┐         ┌─────┬─────┬─────┬─────┬─────┬─────┐
│BTCLR│ BT1 │ BT2 │ BT3 │ BT4 │ BT5 │         │     │     │     │     │     │     │
├─────┼─────┼─────┼─────┼─────┼─────┤         ├─────┼─────┼─────┼─────┼─────┼─────┤
│EPWR │HUE- │HUE+ │SAT- │SAT+ │ EFF │         │     │     │     │     │     │     │
├─────┼─────┼─────┼─────┼─────┼─────┤         ├─────┼─────┼─────┼─────┼─────┼─────┤
│     │BRI- │BRI+ │     │     │     │         │     │     │     │     │     │     │
├─────┼─────┼─────┼─────┼─────┼─────┼RGB_TOG  ├─────┼─────┼─────┼─────┼─────┼─────┤
│     │ TOG │ EFF │HUE+ │SAT+ │BRI+ │         │     │     │     │     │     │     │
└─────┴─────┴─────┴─────┴─────┴─────┘         └─────┴─────┴─────┴─────┴─────┴─────┘
```

- **Row 0:** Bluetooth device selection (1-5), BT Clear (§)
- **Row 1:** External power toggle, RGB hue/saturation/effects
- **Row 2:** RGB brightness adjustment
- **Row 3 (Z,X,C,V,B):** RGB Toggle, Effects, Hue+, Sat+, Brightness+
- **Left Encoder:** RGB toggle

## Swedish OS Symbol Reference

Since the OS is Swedish, these HID codes produce:

| ZMK Keycode | Swedish Output | With Shift |
| ----------- | -------------- | ---------- |
| `N1`-`N0`   | 1-0            | !"#¤%&/()= |
| `COMMA`     | ,              | ;          |
| `DOT`       | .              | :          |
| `FSLH`      | -              | _          |
| `MINUS`     | +              | ?          |
| `BSLH`      | '              | *          |
| `LBKT`      | å              | Å          |
| `SEMI`      | ö              | Ö          |
| `SQT`       | ä              | Ä          |

**Common symbols via AltGr:**

- `@` = AltGr + 2
- `$` = AltGr + 4
- `{` = AltGr + 7
- `[` = AltGr + 8
- `]` = AltGr + 9
- `}` = AltGr + 0
- `\` = AltGr + +
- `~` = AltGr + ¨ (then space)

## Build & Flash

### Prerequisites

- GitHub account with this repo forked
- `gh` CLI installed and authenticated
- macOS with Swedish keyboard layout

### Build Firmware

```bash
# 1. Make changes to keymap
cd ~/dotfiles/zmk-config
$EDITOR config/sofle_choc_pro.keymap

# 2. Commit and push
git add -A
git commit -m "feat: description of changes"
git push

# 3. Trigger GitHub Actions build
gh workflow run "Build ZMK firmware" --repo LinusOstlund/zmk-config

# 4. Watch build progress
gh run list --repo LinusOstlund/zmk-config --limit 1
gh run watch <run-id> --repo LinusOstlund/zmk-config --exit-status

# 5. Download firmware artifacts
gh run download <run-id> --repo LinusOstlund/zmk-config --dir firmware
```

### Flash Firmware

1. **Enter bootloader mode:** Double-tap reset button on each half quickly
2. **Verify mount:** `ls /Volumes/ | grep -i keebart`
   - Should show `KEEBART` and `KEEBART 1`
3. **Copy firmware:**

   ```bash
   cp firmware/firmware/nice_view_disp-sofle_choc_pro_left-zmk.uf2 /Volumes/KEEBART/
   cp firmware/firmware/nice_view_disp-sofle_choc_pro_right-zmk.uf2 /Volumes/KEEBART\ 1/
   ```

4. **Keyboards reboot automatically** after flashing

### Troubleshooting

**Keymap changes not appearing after flash:**

ZMK Studio is enabled with persistent storage. If you've ever modified the keymap through ZMK Studio, those changes persist across firmware updates.

1. Flash `settings_reset-sofle_choc_pro_left.uf2` to left half
2. Flash `settings_reset-sofle_choc_pro_right.uf2` to right half
3. Re-flash regular firmware to both halves

**Halves won't pair after flash:**

1. Flash `settings_reset-sofle_choc_pro_*.uf2` to both halves
2. Re-flash regular firmware

**Bootloader not mounting:**

- Try holding boot button while plugging in USB
- Double-tap reset faster (within 500ms)

## File Structure

```text
zmk-config/
├── config/
│   ├── sofle_choc_pro.keymap    # ← EDIT THIS (overrides board default)
│   └── west.yml                  # West manifest
├── boards/arm/sofle_choc_pro/
│   └── sofle_choc_pro.keymap    # Board default keymap
├── .github/workflows/
│   └── build.yml                 # GitHub Actions build
└── README.md
```

**Note:** The `config/sofle_choc_pro.keymap` overrides the board keymap when present.

## Custom Behaviors

### Tap-Dance (Brackets)

| Key (LOWER) | Tap   | Double-Tap |
| ----------- | ----- | ---------- |
| 8 position  | `[`   | `{`        |
| 9 position  | `]`   | `}`        |

Tapping term: 125ms (175ms for td_n2)

### Macros

| Name   | Output | Implementation              |
| ------ | ------ | --------------------------- |
| tilde  | `~`    | AltGr+RBKT then Space (dead key sequence) |

## Backlog / Future Ideas

- [ ] Add `@` combo (Q + W or similar)
- [ ] Caps Word (double-tap shift)
- [ ] Home row mods (hold for modifier)
- [ ] Mouse keys layer
- [ ] Macro for common phrases
- [ ] Sticky/one-shot modifiers
- [ ] Mod-tap: hold Space = Shift, hold Enter = Ctrl
- [ ] Word selection tap-dance (tap = word jump, hold = select line)

## Resources

- [ZMK Documentation](https://zmk.dev/docs)
- [ZMK Combos](https://zmk.dev/docs/keymaps/combos)
- [ZMK Mod-Morph](https://zmk.dev/docs/keymaps/behaviors/mod-morph)
- [Keebart Website](https://www.keebart.com/products/sofle-wireless)
- [Keebart Discord](https://discord.gg/keebart)

## Quick Reference

Run `wtfzmk` in terminal for a quick cheat sheet (requires alias in dotfiles).

---

_Forked from [Keebart/zmk-config](https://github.com/Keebart/zmk-config)_
