# Cross-Platform Keymap Guide - Piantor Pro BT

**Date Created:** 2025-10-07
**Status:** ✅ Implemented and Working

---

## Overview

The Piantor Pro BT keyboard now supports **true cross-platform operation** with separate keymap files optimized for macOS and Linux.

### Hardware Setup
- **macOS keyboard**: Dedicated Piantor connected only to macOS machine
- **Linux keyboard**: Dedicated Piantor connected only to Nimbini (Linux)
- Both keyboards use **identical firmware** except for edit command modifiers

---

## Architecture Decision

### Why Separate Keymaps?

**Problem:** ZMK edit commands like `LC(C)` (Ctrl+C) work on Linux but not macOS, which expects `LG(C)` (Cmd+C).

**Solution:** Two keymap files that differ only in the NAV and MOUSE layers:
- `piantor_pro_bt.keymap` - Linux version (uses Ctrl)
- `piantor_pro_bt_macos.keymap` - macOS version (uses Cmd)

**Why not conditional compilation?**
- Keyboards are permanently assigned to specific platforms
- Simpler to maintain than Kconfig conditionals
- No need to remember build flags
- Easier to diverge keymaps in the future if needed

---

## Technical Implementation

### NAV Layer Differences

#### Linux Version (`piantor_pro_bt.keymap`)
```c
// Behavior definition
td_ctrlz: tap_dance {
    bindings = <&none>, <&kp LC(Z)>;  // Ctrl+Z
};

// NAV layer top row
&kp LC(Y)  &kp LC(V)  &kp LC(C)  &kp LC(X)  &td_ctrlz
```

#### macOS Version (`piantor_pro_bt_macos.keymap`)
```c
// Behavior definition
td_cmdz: tap_dance {
    bindings = <&none>, <&kp LG(Z)>;  // Cmd+Z
};

// NAV layer top row
&kp LG(Y)  &kp LG(V)  &kp LG(C)  &kp LG(X)  &td_cmdz
```

### Edit Command Mappings

| Action | Base Key | macOS Keymap | Linux Keymap |
|--------|----------|-------------|-------------|
| **Redo** | J (pos 6) | `&kp LG(Y)` → Cmd+Y | `&kp LC(Y)` → Ctrl+Y |
| **Paste** | L (pos 7) | `&kp LG(V)` → Cmd+V | `&kp LC(V)` → Ctrl+V |
| **Copy** | U (pos 8) | `&kp LG(C)` → Cmd+C | `&kp LC(C)` → Ctrl+C |
| **Cut** | Y (pos 9) | `&kp LG(X)` → Cmd+X | `&kp LC(X)` → Ctrl+X |
| **Undo** | ' (pos 10) | `&td_cmdz` → Cmd+Z (double-tap) | `&td_ctrlz` → Ctrl+Z (double-tap) |

### MOUSE Layer

The MOUSE layer has **identical changes** to NAV layer - edit commands work the same way while using mouse emulation.

### All Other Layers

**Completely identical** between both keymaps:
- BASE (Colemak-DH, HRMs, symbol combos)
- SYM (symbols)
- NUM (numbers, numpad)
- MEDIA (media controls, Bluetooth)
- FUN (function keys)

---

## Building Firmware

### Linux Build (Automated)

GitHub Actions automatically builds Linux firmware on every push:

```bash
# Default build uses piantor_pro_bt.keymap
west build -s zmk/app -b piantor_pro_bt_left -- -DSHIELD=nice_view
west build --pristine -s zmk/app -b piantor_pro_bt_right -- -DSHIELD=nice_view
```

**Output:** Firmware files in GitHub Actions artifacts

### macOS Build (Manual)

Build locally on macOS machine:

```bash
cd ~/piantor-zmk

# Build left half
west build -s zmk/app -b piantor_pro_bt_left -- \
  -DZMK_CONFIG="$(pwd)/config" \
  -DKEYMAP_FILE="$(pwd)/config/piantor_pro_bt_macos.keymap" \
  -DSHIELD=nice_view

# Copy firmware
cp build/zephyr/zmk.uf2 ~/Desktop/left_macos.uf2

# Build right half
west build --pristine -s zmk/app -b piantor_pro_bt_right -- \
  -DZMK_CONFIG="$(pwd)/config" \
  -DKEYMAP_FILE="$(pwd)/config/piantor_pro_bt_macos.keymap" \
  -DSHIELD=nice_view

# Copy firmware
cp build/zephyr/zmk.uf2 ~/Desktop/right_macos.uf2
```

### Flashing Firmware

1. **Enter bootloader mode:**
   - Hold Q+W+F (left half) or U+Y+' (right half)
   - Or double-press reset button on keyboard

2. **Flash firmware:**
   - Keyboard appears as USB drive
   - Copy `.uf2` file to the drive
   - Keyboard automatically restarts with new firmware

---

## Maintenance Procedures

### Making Changes to Shared Layers

When modifying BASE, SYM, NUM, MEDIA, or FUN layers:

1. **Edit one keymap file** (either Linux or macOS version)
2. **Copy changes to other keymap file:**
   ```bash
   # Use a diff tool to compare
   diff config/piantor_pro_bt.keymap config/piantor_pro_bt_macos.keymap

   # Manually copy the changed layer(s)
   # Ensure NAV/MOUSE layers remain different!
   ```
3. **Verify NAV/MOUSE layers** remain platform-specific
4. **Build and test** on both platforms

### Making Changes to NAV/MOUSE Layers

**Keep these layers platform-specific!**

When changing navigation or mouse functionality:
1. Update both keymap files independently
2. Remember: macOS uses `LG()`, Linux uses `LC()` for edit commands
3. Keep the pattern consistent between both versions

### Adding New Behaviors

If adding behaviors that need platform-specific implementation:

**Option 1: Add to both files separately**
```c
// In piantor_pro_bt.keymap
my_behavior: behavior {
    // Linux-specific implementation
};

// In piantor_pro_bt_macos.keymap
my_behavior: behavior {
    // macOS-specific implementation
};
```

**Option 2: Keep behavior identical**
```c
// Same behavior code in both files
// Platform differences handled by layer bindings
```

---

## Testing Checklist

### After Building New Firmware

**On macOS:**
- [ ] Hold NAV (left thumb space) + U → Cmd+C copies text
- [ ] Hold NAV + L → Cmd+V pastes text
- [ ] Hold NAV + Y → Cmd+X cuts text
- [ ] Hold NAV + ' (double-tap) → Cmd+Z undoes
- [ ] Hold NAV + J → Cmd+Y redoes
- [ ] All other layers function identically to Linux version
- [ ] Symbol combos work (L+U = colon, U+Y = minus, comma+dot = question)

**On Linux:**
- [ ] Hold NAV + U → Ctrl+C copies text
- [ ] Hold NAV + L → Ctrl+V pastes text
- [ ] Hold NAV + Y → Ctrl+X cuts text
- [ ] Hold NAV + ' (double-tap) → Ctrl+Z undoes
- [ ] Hold NAV + J → Ctrl+Y redoes
- [ ] All other layers function identically to macOS version
- [ ] Symbol combos work identically

**Both Platforms:**
- [ ] HRM behaviors work correctly (A=Ctrl, R=Alt, S=Gui, T=Shift)
- [ ] Bluetooth pairing and switching works
- [ ] Mouse layer functions (if tested)
- [ ] Media controls work
- [ ] Function keys accessible

---

## Troubleshooting

### Edit Commands Not Working on macOS

**Symptom:** Copy/paste/cut/undo don't work or use wrong modifier

**Diagnosis:**
```bash
# Check which keymap was used in build
grep "td_cmdz\|td_ctrlz" build/zephyr/.config

# If it shows td_ctrlz, you built with wrong keymap
```

**Solution:** Rebuild with correct `-DKEYMAP_FILE` flag pointing to `piantor_pro_bt_macos.keymap`

### Edit Commands Not Working on Linux

**Symptom:** Edit commands use Cmd (Super) instead of Ctrl

**Solution:** Ensure GitHub Actions is building default keymap (no KEYMAP_FILE override in build.yaml)

### Keymaps Out of Sync

**Symptom:** One platform has features the other doesn't

**Diagnosis:**
```bash
# Compare keymaps excluding NAV/MOUSE layers
diff config/piantor_pro_bt.keymap config/piantor_pro_bt_macos.keymap
```

**Solution:** Manually sync the differing layers (except NAV/MOUSE)

### Build Fails with macOS Keymap

**Check:**
1. Correct path in `-DKEYMAP_FILE` argument
2. File exists: `config/piantor_pro_bt_macos.keymap`
3. No syntax errors in keymap file

---

## Design Rationale

### Why Tap Dance for Undo?

**Prevents accidental undo triggers** when brushing A key while pressing Z:
- Safety combo `A+Z → none` prevents Ctrl/Cmd+Z
- Double-tap requirement adds deliberate action
- Redo (single key) is easier since less destructive

### Why Hold NAV + Right Hand Keys?

**Ergonomics:**
- Left thumb naturally holds layer
- Right hand free to execute commands
- No finger stretching or awkward combinations
- Same pattern as traditional Ctrl/Cmd+key shortcuts

### Why J/L/U/Y/' Positions?

**Mnemonic and positional logic:**
- J = first key (Redo/redo is forward action)
- L/U/Y = middle keys (primary edit commands)
- ' = last key (Undo is backward action)
- Top row = easy to reach, no HRM interference
- Mirrors QWERTY positions used by most apps

---

## Future Enhancements

### Potential Additions

**If friction emerges from real usage:**
- Save/Find combos (F+S for Save, P+T for Find)
- Additional platform-specific shortcuts
- Per-application layer customization

**Not planned unless needed:**
- Conditional compilation (adds complexity)
- Runtime platform detection (not possible in ZMK)
- Single keymap for both platforms (modifiers don't map correctly)

### Keeping Platforms Consistent

**Philosophy:** The goal is **functional consistency** (same outcome), not **implementation identity** (same code).

- macOS users press NAV+U and get copy behavior (via Cmd+C)
- Linux users press NAV+U and get copy behavior (via Ctrl+C)
- **Same muscle memory, different implementation**

---

## Summary

✅ **Achieved:** True cross-platform keyboard support with minimal maintenance overhead

✅ **Benefits:**
- Each platform gets native shortcuts that work correctly
- Muscle memory transfers perfectly between machines
- Simple maintenance (only NAV/MOUSE layers differ)
- No complex build system changes required

✅ **Trade-off:** Two keymap files to maintain, but differences are minimal and clearly documented

**This is the optimal solution for dedicated keyboards on dedicated platforms.**
