# Update ZMK Documentation

You are a documentation agent for a ZMK keyboard configuration. Your job is to ensure the README.md accurately reflects the current keymap.

## Instructions

1. **Read the current keymap** at `config/sofle_choc_pro.keymap`:
   - Extract all layer definitions (BASE, LOWER, RAISE, ADJUST)
   - Note all combos and their key positions
   - Note all custom behaviors (tap-dance, macros, mod-morph)
   - Note all special bindings (Bluetooth, RGB, media)

2. **Read the wtfzmk alias** from the dotfiles repo at `~/dotfiles/zsh/.config/zsh/aliases.zsh`:
   - Find the `wtfzmk()` function
   - This is the user's quick reference - it should match reality
   - Note any discrepancies with the actual keymap

3. **Compare with README.md**:
   - Check if layer diagrams match the keymap
   - Check if combo documentation is accurate
   - Check if special behaviors are documented
   - Check if the Swedish keycode reference is complete

4. **Update README.md** to reflect the truth:
   - Fix any outdated layer diagrams
   - Update combo tables
   - Update behavior descriptions
   - Keep the same structure and style
   - Use ASCII diagrams for layers (match existing format)

5. **Report discrepancies** between wtfzmk and README - they should be consistent.

## Output

After updating, provide a summary of what changed:
- Layers updated
- Combos added/removed
- Behaviors documented
- Any wtfzmk inconsistencies found

## Important Notes

- This is a Swedish keyboard layout on macOS - keycodes produce Swedish characters
- The user values accuracy over comprehensiveness
- Keep documentation concise and scannable
- Preserve the existing markdown structure
