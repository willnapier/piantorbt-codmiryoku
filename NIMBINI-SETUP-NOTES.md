# Nimbini Setup Notes

**Date Logged:** 2025-10-07
**Next Nimbini Access:** ~4 weeks from now

---

## Application Launcher Installation & Configuration

### Primary: anyrun (Rust-based) 🦀

**Why anyrun:**
- ✅ Written in Rust (matches your toolchain preference)
- ✅ Window switching via niri-focus plugin
- ✅ Actively maintained (271+ commits)
- ✅ Fuzzy search with native Wayland support
- ✅ Niri-specific integration

**Installation:**
```bash
# On Arch Linux (AUR)
yay -S anyrun-git

# Or using Nix (if you have Nix installed)
nix profile install nixpkgs#anyrun
```

**Configure anyrun plugins:**
```bash
# Create config directory
mkdir -p ~/.config/anyrun

# Edit config to enable niri-focus plugin
# ~/.config/anyrun/config.ron should include:
# Config(
#     plugins: [
#         "libapplications.so",
#         "libniri_focus.so",  // Window switching plugin
#         "libsymbols.so",
#         "librink.so",        // Calculator
#     ],
# )
```

### Fallback: rofi (if anyrun has issues)

**Installation:**
```bash
# On Arch Linux
sudo pacman -S rofi-wayland
```

**Note:** Rofi is C-based but mature and well-documented. Keep as backup if anyrun setup proves complex.

### Configure Niri: Navigation & Application Management

**Status:** ✅ Already configured in `~/dotfiles/niri/config.kdl`

**Navigation Pattern (Consistent System):**

```kdl
binds {
    // Application launcher with window switching (like macOS Cmd+Space)
    // Primary: anyrun (Rust, with niri-focus plugin)
    Super+Space { spawn "anyrun"; }

    // Fallback: rofi (if anyrun not working)
    // Super+Space { spawn "rofi" "-show" "window"; }

    // Focus navigation (Mod+Shift = read operations)
    Super+Shift+Left  { focus-column-left; }
    Super+Shift+Right { focus-column-right; }
    Super+Shift+Down  { focus-window-down-or-top; }      // Cycles down, wraps to top
    Super+Shift+Up    { focus-window-up-or-bottom; }     // Cycles up, wraps to bottom

    // Window cycling (keyboard compatibility - triggered by S+` on keyboard)
    Super+Grave       { focus-window-down-or-top; }
    Super+Shift+Grave { focus-window-up-or-bottom; }

    // Move operations (Mod+Alt+Shift = write operations)
    Super+Alt+Shift+Left  { move-column-left; }
    Super+Alt+Shift+Right { move-column-right; }
    Super+Alt+Shift+Down  { move-window-down; }
    Super+Alt+Shift+Up    { move-window-up; }
}
```

**Design Principles:**
- **Consistent modifiers:** Same modifiers for same operation type
- **Focus (Mod+Shift):** Navigate/read operations - arrows or NEIO keys
- **Move (Mod+Alt+Shift):** Reposition/write operations - requires extra modifier
- **Keyboard compatibility:** Grave bindings match macOS muscle memory via S+`
- **Cycling variants:** Window stack navigation wraps around for seamless navigation

---

## Verification Steps

### Test anyrun (Primary)

1. **Test Super+Space binding:**
   - Press Super+Space
   - Should show anyrun with fuzzy search
   - Start typing app name or window title
   - Select window → should focus that window

2. **Test window switching (niri-focus plugin):**
   - Open multiple windows (Firefox, terminal, editor)
   - Press Super+Space
   - Type partial window title (fuzzy search)
   - Select → should focus existing window

3. **Test app launching:**
   - Close Firefox
   - Super+Space → type "firefox"
   - Should launch new instance

4. **anyrun Advantages:**
   - Fuzzy search (more forgiving than exact match)
   - GTK4 native styling
   - Rust-based performance
   - Niri-specific integration

### Fallback to rofi (if needed)

**If anyrun has issues:**
1. Edit `~/dotfiles/niri/config.kdl`
2. Comment out anyrun line
3. Uncomment rofi line:
   ```kdl
   // Super+Space { spawn "anyrun"; }
   Super+Space { spawn "rofi" "-show" "window"; }
   ```
4. Reload Niri config

**Rofi features:**
- Lists all open windows across all columns
- Selecting one focuses existing window
- If app not running, can still launch it
- More mature/documented than anyrun

---

## Troubleshooting anyrun

### Common Issues

**anyrun won't close (NVIDIA GPU):**
```bash
# Set environment variable before launching
GSK_RENDERER=ngl anyrun

# Or add to Niri config:
spawn-at-startup "sh" "-c" "export GSK_RENDERER=ngl"
```

**niri-focus plugin not working:**
1. Check plugin is enabled in `~/.config/anyrun/config.ron`
2. Verify `libniri_focus.so` exists in plugin directory
3. Check anyrun logs: `journalctl --user -u anyrun` (if running as service)

**anyrun not showing windows:**
- Ensure you're using anyrun's window list, not just app launcher
- niri-focus plugin provides window switching
- May need to configure plugin priority in config.ron

**Fuzzy search too sensitive/not sensitive enough:**
- Adjust fuzzy search threshold in anyrun config
- Check `~/.config/anyrun/config.ron` for search settings

---

## Notes

- **anyrun (Rust)** chosen as primary launcher for Rust toolchain consistency
- **rofi** available as mature fallback if anyrun has issues
- Super+Space is available (default keyboard layout switch is commented out)
- No conflict with SA (Super+Alt) prefix window management system
- This is OS-level binding, not keyboard firmware combo
- Frees up L+N combo for other uses in keyboard firmware
- Same muscle memory as macOS Cmd+Space

---

## Design Decision Log

**Why anyrun over rofi?**
- **Rust-based**: Matches your toolchain philosophy (`fd`, `rg`, `sd`, `bat`)
- **niri-focus plugin**: Native niri integration for window switching
- **Actively maintained**: 271+ commits, not in maintenance mode
- **Fuzzy search**: Potentially better UX than rofi's exact matching
- **rofi as fallback**: Keep both installed for reliability

**Why Super+Space instead of L+N combo?**
- Better architecture: OS-level shortcut for OS-level function
- Same physical gesture as macOS (Cmd/Super + Space)
- Saves keyboard combo real estate for things without good OS shortcuts
- Simpler: No conditional macros needed in firmware
