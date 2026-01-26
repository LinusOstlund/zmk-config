# ZMK Config - Claude Instructions

You are assisting with a **ZMK firmware configuration** for a **Keebart Sofle Choc Pro BT** split keyboard running on **macOS with Swedish keyboard layout**.

## Critical Context

1. **Swedish OS Layout**: The keyboard sends US HID keycodes, but macOS interprets them as Swedish. This means:
   - `LBKT` → å, `SEMI` → ö, `SQT` → ä
   - `COMMA` → ,; `DOT` → .: `FSLH` → -_
   - `MINUS` → +? `BSLH` → '*
   - Brackets require AltGr: `RA(N8)` = [, `RA(N9)` = ], `RA(N7)` = {, `RA(N0)` = }

2. **Layer Philosophy**:
   - **LOWER** (left thumb): Navigation, symbols, arrows, brackets
   - **RAISE** (right thumb): Bluetooth, media, tilde, clipboard
   - **ADJUST** (both): RGB, BT clear, power

3. **Key Positions**: Sofle has 58 keys (0-57). Reference `config/sofle_choc_pro.keymap` for position mapping.

## Rules

1. **Never guess Swedish keycodes** - always reference the keycode table in README.md or ask.

2. **Test changes mentally** before suggesting - walk through what happens when the key is pressed on Swedish OS.

3. **Preserve combos** - Swedish character combos (å ä ö) are critical. Don't break them.

4. **Use behaviors correctly**:
   - `&kp` for simple keys
   - `&mt` for mod-tap (hold=mod, tap=key)
   - `&lt` for layer-tap (hold=layer, tap=key)
   - `&td_*` for tap-dance (defined in behaviors section)
   - `&tilde` for the tilde macro

5. **Comment non-obvious bindings** - especially Swedish symbol mappings.

6. **Build workflow**: Changes require GitHub Actions build:
   ```bash
   git add -A && git commit -m "feat: description" && git push
   gh workflow run "Build ZMK firmware" --repo LinusOstlund/zmk-config
   ```

## File Structure

```text
zmk-config/
├── config/
│   └── sofle_choc_pro.keymap   # ← THE keymap - EDIT THIS
├── boards/arm/sofle_choc_pro/
│   └── sofle_choc_pro.keymap   # Board default (overridden by config/)
├── .github/workflows/
│   └── build.yml               # GitHub Actions build
└── README.md                   # User documentation
```

**IMPORTANT:** The `config/sofle_choc_pro.keymap` overrides the board keymap. Build logs confirm:
`-- Using keymap file: /tmp/zmk-config/config/sofle_choc_pro.keymap`

## ZMK Studio Warning

This keyboard has ZMK Studio enabled with persistent keymap storage. If keymap changes don't appear after flashing:

1. **ZMK Studio may have stored old keymap settings** that persist across firmware updates
2. **Solution:** Flash `settings_reset` firmware first to clear stored settings, then flash regular firmware

```bash
# Flash settings reset (clears stored keymap)
cp settings_reset-sofle_choc_pro_left.uf2 /Volumes/KEEBART/
cp settings_reset-sofle_choc_pro_right.uf2 /Volumes/KEEBART\ 1/

# Then flash regular firmware
cp nice_view_disp-sofle_choc_pro_left-zmk.uf2 /Volumes/KEEBART/
cp nice_view_disp-sofle_choc_pro_right-zmk.uf2 /Volumes/KEEBART\ 1/
```

## When Making Changes

1. Read the current keymap first
2. Identify the layer and position
3. Use correct Swedish-aware keycodes
4. Update README.md if behavior changes
5. Update `wtfzmk` alias in dotfiles if layout changes significantly

## Quick Reference

| What | ZMK Code | Swedish Output |
|------|----------|----------------|
| å | `&kp LBKT` | å |
| ä | `&kp SQT` | ä |
| ö | `&kp SEMI` | ö |
| [ | `&kp RA(N8)` | [ |
| ] | `&kp RA(N9)` | ] |
| { | `&kp RA(N7)` | { |
| } | `&kp RA(N0)` | } |
| < | `&kp NUBS` | < |
| > | `&kp LS(NUBS)` | > |
| ~ | `&tilde` | ~ (macro) |
| \ | `&kp RA(MINUS)` | \ |
| @ | `&kp RA(N2)` | @ |
| $ | `&kp RA(N4)` | $ |

## Related Files (in dotfiles repo)

- `zsh/.config/zsh/aliases.zsh` - Contains `wtfzmk` function
- `.claude/plans/zmk/` - Planning documents
- `.claude/plans/iterations/` - Iteration feedback
