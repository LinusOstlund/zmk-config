# ZMK Keymap Changes - Requested 2026-01-25

## Overview

Changes requested for Sofle Choc Pro BT with Swedish keyboard layout on macOS.

## Key Findings (Investigation 2026-01-25)

### Keymap Resolution - CORRECTED

**Previous assumption (WRONG):** The board keymap overrides the config keymap.

**Actual behavior (CORRECT):** The `config/sofle_choc_pro.keymap` IS being used.

**Evidence from build log:**
```
-- Using keymap file: /tmp/zmk-config/config/sofle_choc_pro.keymap
-- Found devicetree overlay: /tmp/zmk-config/config/sofle_choc_pro.keymap
```

### Why Changes Weren't Appearing

ZMK Studio is enabled with persistent keymap storage:
```
CONFIG_ZMK_KEYMAP_SETTINGS_STORAGE=y
CONFIG_ZMK_STUDIO=y
```

If you ever modified the keymap through ZMK Studio, those changes are saved to flash storage and **persist across firmware updates**.

### Solution: Flash Settings Reset First

1. Flash `settings_reset-sofle_choc_pro_left.uf2` to left half
2. Flash `settings_reset-sofle_choc_pro_right.uf2` to right half
3. Then flash regular firmware to both halves

This clears any stored keymap overrides and forces the keyboard to use the compiled keymap.

---

## File Structure

```text
zmk-config/
├── config/
│   └── sofle_choc_pro.keymap    # ← THIS IS USED (user config)
├── boards/arm/sofle_choc_pro/
│   └── sofle_choc_pro.keymap    # Default/backup (NOT used when config exists)
└── build.yaml                    # Build matrix
```

The `config/` keymap is an overlay that overrides the board default. This is standard ZMK behavior.

---

## Requested Changes

All changes should be made to `config/sofle_choc_pro.keymap`.

### 1. Replace Enter with ^/~ next to P (BASE layer, position 23)

**Goal:** Free up Enter from pinky, move it to thumb only.

**Status:** ✅ Already implemented in config keymap
```c
td_caret_tilde: tap_dance_caret_tilde {
  compatible = "zmk,behavior-tap-dance";
  #binding-cells = <0>;
  tapping-term-ms = <125>;
  bindings = <&kp LS(RBKT)>, <&tilde>;  // ^ then ~
};
```

### 2. Swap ' and +/? on home row (BASE layer, positions 34/35)

**Goal:** Put apostrophe on outer pinky position.

**Status:** ✅ Already implemented in config keymap
- Position 34: `&kp MINUS` (+/? on Swedish)
- Position 35: `&kp BSLH` (' on Swedish)

### 3. Single-tap | on LOWER layer (position 7)

**Goal:** Remove double-tap for pipe, make it single tap.

**Status:** ✅ Already implemented in config keymap
```c
m_pipe: macro_pipe {
  compatible = "zmk,behavior-macro";
  #binding-cells = <0>;
  bindings = <&kp RA(N7)>;  // | = Option+7 on macOS Swedish
};
```

### 4. Add ´ (acute accent) to LOWER layer (position 34)

**Status:** ✅ Already implemented - `&kp EQUAL` at LOWER position 34

### 5. Add * to LOWER layer (position 35)

**Status:** ✅ Already implemented - `&kp LS(BSLH)` at LOWER position 35

### 6. Tap-dance timing adjustments

**Status:** ✅ Already implemented
- All tap-dance behaviors: 125ms
- Exception: `td_n2` (left hand "/@) = 175ms

### 7. Combos for Swedish characters

**Status:** ✅ Already implemented
| Combo | Positions | Keys | Output |
|-------|-----------|------|--------|
| å | 22+23 | P + ^/~ | LBKT |
| ö | 33+34 | L + +/? | SEMI |
| ä | 34+35 | +/? + ' | SQT |
| Spotlight | 26+22 | S + P | LG(SPACE) |

---

## Next Steps

All changes are already in the config keymap. To apply them:

1. **Clear stored settings** (required because ZMK Studio may have persisted old keymap):
   ```bash
   # Put both halves in bootloader mode
   # Flash settings reset to both:
   cp firmware/settings_reset-sofle_choc_pro_left.uf2 /Volumes/KEEBART/
   cp firmware/settings_reset-sofle_choc_pro_right.uf2 /Volumes/KEEBART\ 1/
   ```

2. **Re-flash regular firmware:**
   ```bash
   # Put both halves in bootloader mode again
   cp firmware/nice_view_disp-sofle_choc_pro_left-zmk.uf2 /Volumes/KEEBART/
   cp firmware/nice_view_disp-sofle_choc_pro_right-zmk.uf2 /Volumes/KEEBART\ 1/
   ```

3. **Test all changes** per the checklist below.

---

## Testing Checklist

- [ ] Flash settings_reset to both halves
- [ ] Flash regular firmware to both halves
- [ ] Both keyboard halves work
- [ ] Key next to P outputs ^ (tap) and ~ (double-tap)
- [ ] LOWER + 7 outputs |
- [ ] LOWER + position34 outputs ´
- [ ] LOWER + position35 outputs *
- [ ] Combos work: å, ö, ä, Spotlight
- [ ] Tap-dance timing feels responsive (125ms/175ms)

---

## Documentation To Update (after testing)

1. **README.md** - Add settings_reset workflow to troubleshooting
2. **CLAUDE.md** - Update with correct file to edit
3. **wtfzmk alias** - ✅ Already updated

---

## Lessons Learned

1. **Config keymap DOES override board keymap** - Build logs prove this
2. **ZMK Studio persistent storage can override flashed keymap** - Must flash settings_reset to clear
3. **Two keymap files exist but config takes precedence** - Edit `config/sofle_choc_pro.keymap`
4. **Build logs show keymap resolution** - Check `-- Using keymap file:` line
