# Platform-Specific Keymaps - Quick Reference

**Date:** 2025-10-07
**Status:** ✅ Implemented

---

## Quick Facts

- **Two keyboards, two platforms:** One Piantor for macOS, one for Linux (Nimbini)
- **Two keymap files:** Nearly identical except for edit command modifiers
- **Same muscle memory:** NAV+U copies on both platforms (via Cmd on macOS, Ctrl on Linux)

---

## Which Keymap For Which Platform?

| Keymap File | Platform | Modifier | Build Method |
|------------|----------|----------|--------------|
| `piantor_pro_bt.keymap` | **Linux (Nimbini)** | Ctrl (`LC()`) | GitHub Actions (automatic) |
| `piantor_pro_bt_macos.keymap` | **macOS** | Cmd (`LG()`) | Local build (manual) |

---

## Edit Commands Quick Reference

**Hold NAV (left thumb on SPACE) + right hand key:**

| Key | Action | macOS | Linux |
|-----|--------|-------|-------|
| **J** | Redo | Cmd+Y | Ctrl+Y |
| **L** | Paste | Cmd+V | Ctrl+V |
| **U** | Copy | Cmd+C | Ctrl+C |
| **Y** | Cut | Cmd+X | Ctrl+X |
| **'** | Undo (double-tap) | Cmd+Z | Ctrl+Z |

**Same commands available on MOUSE layer**

---

## When To Use Each Build Command

### Building for macOS (Local)

```bash
# Use when updating macOS keyboard
west build -s zmk/app -b piantor_pro_bt_left -- \
  -DZMK_CONFIG="$(pwd)/config" \
  -DKEYMAP_FILE="$(pwd)/config/piantor_pro_bt_macos.keymap" \
  -DSHIELD=nice_view
```

### Building for Linux (Push to GitHub)

```bash
# Just push to GitHub - Actions builds automatically with default keymap
git add config/piantor_pro_bt.keymap
git commit -m "Update Linux keymap"
git push
```

---

## What's Different Between Keymaps?

**Only NAV and MOUSE layers differ:**
- Behavior: `td_ctrlz` (Linux) vs `td_cmdz` (macOS)
- Edit commands: `LC()` (Linux) vs `LG()` (macOS)

**Everything else identical:**
- BASE layer (Colemak-DH, HRMs, combos)
- SYM, NUM, MEDIA, FUN layers
- All behaviors except undo tap-dance

---

## Keeping Keymaps in Sync

**When changing non-NAV/MOUSE layers:**
1. Edit one keymap file
2. Copy changes to other keymap file
3. Verify NAV/MOUSE layers remain different
4. Build and test both platforms

---

## Complete Documentation

See [CROSS-PLATFORM-KEYMAP-GUIDE.md](./CROSS-PLATFORM-KEYMAP-GUIDE.md) for:
- Full technical implementation details
- Build procedures and troubleshooting
- Maintenance workflows
- Testing checklists
- Design rationale

---

## Why This Approach?

**Simplicity:** Keyboards are permanently assigned to platforms - no need for complex conditional compilation

**Maintainability:** Only 2 layers differ between 60+ layer definitions

**Correctness:** Each platform gets native shortcuts that actually work

**Muscle Memory:** Same physical gestures produce same logical outcomes across platforms
