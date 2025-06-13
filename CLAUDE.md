# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a ZMK (Zephyr-based Mechanical Keyboard) firmware configuration for the Piantor Pro BT keyboard (42-key split) running a Miryoku-inspired layout with Colemak-DH base layer. This configuration is based on the official Keebart repository structure with a custom Miryoku keymap.

## Key Commands

### Building Firmware
```bash
# Build left half with nice!view display
west build -s zmk/app -b piantor_pro_bt_left -- -DSHIELD=nice_view

# Build right half with nice!view display (use --pristine to clean build)
west build --pristine -s zmk/app -b piantor_pro_bt_right -- -DSHIELD=nice_view
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
- **`piantor_pro_bt.keymap`**: 8-layer Miryoku keymap definition with home row mods for 42-key layout
- **`west.yml`**: Points to upstream ZMK repository
- **`build.yaml`**: Defines boards for GitHub Actions builds
- **`boards/arm/piantor_pro_bt/`**: Complete board definition files from Keebart
- **`zephyr/module.yml`**: Module configuration for board discovery

### Important Details
- Uses Piantor Pro BT board definition files (not shields)
- 42-key layout (6 columns x 3 rows + 3 thumb keys per side)
- Based on official Keebart repository structure
- Left half configured as central (connects to computer)
- Right half configured as peripheral (connects to left half)
- GitHub Actions automatically builds firmware on push using build.yaml
- Built-in features: deep sleep, RGB underglow, battery monitoring via MAX17048
- nice!view displays enabled on both halves
- Mouse pointing support enabled

### Layers
0. BASE - Colemak-DH with home row mods
1. SYM - Symbols
2. NUM - Numbers/numpad
3. NAV - Navigation
4. MEDIA - Media controls and Bluetooth profiles
5. MOUSE - Mouse emulation
6. FUN - Function keys
7. BUTTON - Additional mouse buttons

### Extra Keys (vs 36-key layout)
- **Left side**: Tab (top-left), Esc (middle-left), Shift (bottom-left)
- **Right side**: Backspace (top-right), Semicolon (middle-right), Shift (bottom-right)
- **Transparent** on all non-base layers to avoid conflicts

## Common Tasks

### Modifying Keymap
Edit `config/piantor_pro_bt.keymap`. The file uses ZMK's keymap format with bindings for each layer adapted for the 42-key layout.

### Changing Keyboard Settings
Edit `config/piantor_pro_bt.conf` for features like display settings, pointing configuration, or Bluetooth power settings.

### Testing Changes
Push to GitHub to trigger automated builds, or build locally using the commands above.