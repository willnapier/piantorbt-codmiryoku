# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a ZMK (Zephyr-based Mechanical Keyboard) firmware configuration for the Piantor Pro BT keyboard (42-key split) running a Miryoku-inspired layout with Colemak-DH base layer. This configuration is based on the official Keebart repository structure with a custom Miryoku keymap.

**NEW (2025-10-07):** This project now maintains **two platform-specific keymaps** for true cross-platform support:
- `piantor_pro_bt.keymap` - Linux version (Ctrl-based edit commands)
- `piantor_pro_bt_macos.keymap` - macOS version (Cmd-based edit commands)

See [PLATFORM-SPECIFIC-KEYMAPS.md](./PLATFORM-SPECIFIC-KEYMAPS.md) for quick reference or [CROSS-PLATFORM-KEYMAP-GUIDE.md](./CROSS-PLATFORM-KEYMAP-GUIDE.md) for complete details.

## Key Commands

### Building Firmware

**Two keymaps available:**
- `piantor_pro_bt.keymap` - **Linux version** (uses Ctrl for edit commands)
- `piantor_pro_bt_macos.keymap` - **macOS version** (uses Cmd for edit commands)

#### Linux Build (Default - for Nimbini)
```bash
# Build left half with nice!view display
west build -s zmk/app -b piantor_pro_bt_left -- -DSHIELD=nice_view

# Build right half with nice!view display (use --pristine to clean build)
west build --pristine -s zmk/app -b piantor_pro_bt_right -- -DSHIELD=nice_view
```

#### macOS Build (for macOS keyboard)
```bash
# Build left half with macOS keymap
west build -s zmk/app -b piantor_pro_bt_left -- \
  -DZMK_CONFIG="$(pwd)/config" \
  -DKEYMAP_FILE="$(pwd)/config/piantor_pro_bt_macos.keymap" \
  -DSHIELD=nice_view

# Build right half with macOS keymap
west build --pristine -s zmk/app -b piantor_pro_bt_right -- \
  -DZMK_CONFIG="$(pwd)/config" \
  -DKEYMAP_FILE="$(pwd)/config/piantor_pro_bt_macos.keymap" \
  -DSHIELD=nice_view
```

### Initial Setup (if needed)
```bash
west init -l config
west update
west zephyr-export
```

## Architecture

### Configuration Structure
- **`piantor_pro_bt.conf`**: Main keyboard configuration (display, pointing, Bluetooth)
- **`piantor_pro_bt.keymap`**: Linux version - 7-layer Miryoku keymap with Ctrl-based edit commands
- **`piantor_pro_bt_macos.keymap`**: macOS version - identical to Linux version but uses Cmd for edit commands
- **`west.yml`**: Points to upstream ZMK repository
- **`build.yaml`**: Defines boards for GitHub Actions builds
- **`boards/arm/piantor_pro_bt/`**: Complete board definition files from Keebart
- **`zephyr/module.yml`**: Module configuration for board discovery

### Platform-Specific Edit Commands

**NAV and MOUSE layers have cross-platform edit commands:**

| Action | macOS Keymap | Linux Keymap | Base Layer Key |
|--------|-------------|-------------|----------------|
| Redo   | NAV+J → Cmd+Y | NAV+J → Ctrl+Y | J (pos 6) |
| Paste  | NAV+L → Cmd+V | NAV+L → Ctrl+V | L (pos 7) |
| Copy   | NAV+U → Cmd+C | NAV+U → Ctrl+C | U (pos 8) |
| Cut    | NAV+Y → Cmd+X | NAV+Y → Ctrl+X | Y (pos 9) |
| Undo   | NAV+' → Cmd+Z (double-tap) | NAV+' → Ctrl+Z (double-tap) | ' (pos 10) |

**Implementation details:**
- macOS keymap uses `LG()` (Left GUI/Cmd) via `td_cmdz` behavior
- Linux keymap uses `LC()` (Left Ctrl) via `td_ctrlz` behavior
- Both keymaps are otherwise identical
- Edit commands also available on MOUSE layer

### Important Details
- Uses Piantor Pro BT board definition files (not shields)
- 42-key layout (6 columns x 3 rows + 3 thumb keys per side)
- Based on official Keebart repository structure
- Left half configured as central (connects to computer)
- Right half configured as peripheral (connects to left half)
- GitHub Actions automatically builds firmware on push using a custom workflow (.github/workflows/build.yml) with the build matrix from build.yaml
- Built-in features: deep sleep, RGB underglow, battery monitoring via MAX17048
- nice!view displays enabled on both halves
- Mouse pointing support enabled

### Layers
0. BASE - Colemak-DH with home row mods
1. SYM - Symbols
2. NUM - Numbers/numpad + sticky modifier on right outer middle for tab switching (Alt on Linux, Cmd on macOS)
3. NAV - Navigation + edit commands (Copy/Paste/Cut/Undo/Redo)
4. MEDIA - Media controls and Bluetooth profiles
5. MOUSE - Mouse emulation + edit commands (same as NAV)
6. FUN - Function keys

### Extra Keys (vs 36-key layout)
- **Left side**: Pipe (top-left), Smart Shift (middle-left), none (bottom-left)
- **Right side**: Question/Exclaim (top-right), Smart Shift (middle-right), Colon/Semi (bottom-right)
- **Transparent** on most non-base layers for fallthrough behavior

### Key Features
- **Cognitive Consistency**: Punctuation in same positions across layers (MINUS, COMMA, DOT, FSLH, TILDE)
- **Smart Shift**: Shift keys that produce parentheses when double-tapped
- **Shift Behaviors**: Leverages standard keyboard shift (e.g., Shift+EQUAL = PLUS)
- **Simplified thumbs**: ESC/MEDIA on leftmost thumb (tap/hold)
- **Symbol Combos**: 11 combos for ergonomic programming (2025-10-07)
- **Shift Combos** (2026-06-30): home-row S+T / N+E fire a one-shot sticky Shift for single capitals (experimental). NB the earlier "tab/history navigation" combos (2025-10-07) are **no longer present** in either keymap.
- **Bilateral home-row mods** (2026-06-28): left letter-mods A=Ctrl, R=Alt, S=Gui use the `hml` positional hold-tap — the hold only triggers with an opposite-hand (right) key. Prevents same-hand misfires such as a→z producing Ctrl-Z (which suspends the terminal). Shift mods (`hml_shift`/`hmr_shift`) were already bilateral; this extends the guard to the remaining left letter-mods on both keymaps.
- **Ctrl+Z hard no-op** (both keymaps, 2026-06-28/29): base-layer Z is a `z_no_ctrl` mod-morph — Z alone = "z", but Z while **Left-Ctrl** is held emits nothing. Reads live modifier state, so it neutralises a *deliberately-held* A (=LCtrl) followed by Z — which the positional `hml` guard above cannot, because a sustained hold engages the mod by design. Kills terminal-suspend (SIGTSTP) at the source. Only Left-Ctrl is in the trigger mask, so **Right-Ctrl+Z and Cmd+Z are unaffected**. Applied to **both keymaps** for identical cross-platform behaviour. Undo is preserved on each platform via the NAV layer (macOS `td_cmdz`=Cmd+Z; Linux `td_ctrlz`=Ctrl+Z, a separate binding) — only the misfire-prone hold-A+Z route is removed.
- **num_word**: REMOVED due to stability issues (see NUM_WORD_IMPLEMENTATION.md)

## Common Tasks

### Modifying Keymap

**For Linux keyboard (Nimbini):**
- Edit `config/piantor_pro_bt.keymap`
- Push to GitHub to trigger automated builds via GitHub Actions

**For macOS keyboard:**
- Edit `config/piantor_pro_bt_macos.keymap`
- Build locally using macOS build commands above
- Flash manually to keyboard via bootloader mode

**Platform-specific changes:**
- NAV layer edit commands: Use `LG()` for macOS, `LC()` for Linux
- Tap dance behaviors: Use `td_cmdz` for macOS, `td_ctrlz` for Linux
- All other layers should remain identical between keymaps

### Changing Keyboard Settings
Edit `config/piantor_pro_bt.conf` for features like display settings, pointing configuration, or Bluetooth power settings. This config file is shared between both keymaps.

### Keeping Keymaps in Sync
When making changes to layers other than NAV/MOUSE:
1. Make changes in one keymap file
2. Manually copy to the other keymap file
3. Verify NAV/MOUSE layers remain platform-specific
4. Test both platforms to ensure consistency

## Quick Reference

### Symbol Combos (2025-10-07)

**Programming symbols via simultaneous keypresses:**

| Combo | Output | Common Use |
|-------|--------|------------|
| A+R | `#` | Comments, headers |
| W+F | `[` or `{` (Shift) | Arrays, dicts, JSON |
| F+P | `]` or `}` (Shift) | Closing brackets |
| I+O | `'` or `"` (Shift) | String quotes |
| C+D | `|` | Shell pipes, OR logic |
| X+C | `@` | Email, decorators |
| H+, | `+` | Addition, concat |
| .+/ | `£` | UK currency |
| L+U | `:` or `;` (Shift) | Python, CSS |
| U+Y | `-` | Minus, hyphen |
| ,+. | `?` or `!` (Shift) | Questions |

**How to use:** Press both keys simultaneously (within 50ms) after brief pause (150ms)

**See:** [SYMBOL-COMBOS-IMPLEMENTATION.md](./SYMBOL-COMBOS-IMPLEMENTATION.md) for complete documentation

### Shift Combos — one-shot capitals (2026-06-30, experimental)

**Tap both keys of a home-row pair to arm a sticky Shift for the *next* letter** (one capital, then auto-releases):

| Combo | Positions | Emits | Suggested use |
|-------|-----------|-------|---------------|
| S+T | 15 16 | sticky **LSHIFT** | left-hand combo → capitalise a right-hand letter |
| N+E | 19 20 | sticky **RSHIFT** | right-hand combo → capitalise a left-hand letter |

- **Shift only — never Cmd/Ctrl** — so there is **no conflict with Cmd+Shift (or Ctrl+Shift) application shortcuts**.
- Guarded by `require-prior-idle-ms = 200` + `timeout-ms = 40`: they will not fire during ordinary typing rolls (`st`, `ne`, `en` have no preceding pause), but *will* fire after a space — which is where capitals naturally fall.
- **Tuning:** hard to trigger → raise `timeout-ms` toward 50; misfires on `st…`/`ne…` words typed after a pause → lower `timeout-ms` (~30) or raise `require-prior-idle-ms`. Restricted to `layers = <BASE>`; defined identically in both keymaps.
- **Fallback for what this can't cover:** mid-word capitals (camelCase, acronyms) → hold-T / hold-N home-row Shift; runs of capitals → `caps_word` (NAV layer).

**History:** an earlier revision (2025-10-07) documented S+T / N+E / R+S / E+I as tab- and history-navigation combos (Cmd+Shift+[, etc.). Those combos were since removed and are **not present in either keymap** as of 2026-06-30 — only the now-unused `prev_tab`/`next_tab` mod-morph behaviours remain. `TAB-HISTORY-COMBOS-IMPLEMENTATION.md` is therefore historical.