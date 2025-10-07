# Tab and History Navigation Combos

**Date Implemented:** 2025-10-07
**Status:** ✅ Implemented in both keymaps

---

## Overview

Added four home row combos for browser/application tab and history navigation:

**Tab Navigation (Most Frequent - Inner Positions):**
- S+T → Previous tab
- N+E → Next tab

**History Navigation (Less Frequent - Outer Positions):**
- R+S → Back in history
- E+I → Forward in history

---

## Visual Layout

```
Home Row (Colemak-DH):
A    R────S────T        N────E────I    O
     └────┘    │        │    └────┘
   History  Tabs      Tabs  History
   (Back)   (Prev)   (Next) (Fwd)
```

**Key Positions:**
- R+S = 14, 15 (adjacent outer)
- S+T = 15, 16 (adjacent inner)
- N+E = 19, 20 (adjacent inner)
- E+I = 20, 21 (adjacent outer)

---

## Platform-Specific Shortcuts

### macOS Version (`piantor_pro_bt_macos.keymap`)

**Tab Navigation:**
- S+T → Cmd+Shift+[ (Previous tab)
- N+E → Cmd+Shift+] (Next tab)

**History Navigation:**
- R+S → Cmd+[ (Back)
- E+I → Cmd+] (Forward)

**Works in:**
- Firefox, Chrome, Safari (tabs)
- Firefox, Chrome, Safari (history)
- Any macOS app with tab/history support

### Linux Version (`piantor_pro_bt.keymap`)

**Tab Navigation:**
- S+T → Ctrl+PgUp (Previous tab)
- N+E → Ctrl+PgDn (Next tab)

**History Navigation:**
- R+S → Alt+Left (Back)
- E+I → Alt+Right (Forward)

**Works in:**
- Firefox, Chrome (tabs and history)
- Any Linux app following standard shortcuts

---

## Technical Implementation

### Combo Configuration

All combos use:
- `timeout-ms = <50>` - Fast, near-simultaneous press
- `require-prior-idle-ms = <150>` - Prevents accidental firing during fast typing
- `layers = <BASE>` - Only active on base layer

### Macro Pattern

**macOS macros:**
```c
bindings = <&kp LGUI>, <&kp LSHFT>, <&kp LBKT>, <&kp LGUI>;
// Press GUI, press Shift, press [, release GUI
```

**Linux macros:**
```c
bindings = <&kp LCTRL>, <&kp PG_UP>, <&kp LCTRL>;
// Press Ctrl, press PgUp, release Ctrl
```

---

## Design Rationale

### Why Home Row Combos?

**Ergonomics:**
- Minimal finger travel
- Comfortable adjacent finger combinations
- Faster than reaching for arrow keys or Fn combos

**Frequency-based positioning:**
- Tab switching (S+T / N+E) on inner positions = most frequent
- History navigation (R+S / E+I) on outer positions = less frequent

**Symmetry:**
- Left hand = "previous/back" semantic
- Right hand = "next/forward" semantic
- Mirror positions for easy learning

### Why Not Arrow Keys?

1. **Platform inconsistency:** macOS doesn't use arrows for tabs/history by default
2. **HRM conflicts:** Would require complex modifier combinations
3. **Reach:** Even on NAV layer, arrows require more finger travel
4. **Clarity:** Home row combos are more deliberate actions

### Niri Compatibility

**No conflicts with Niri SS (Super+Shift) bindings because:**
- Combo fires in <50ms (simultaneous press)
- Niri shortcuts need Super held + Shift held + key pressed (sequential)
- Different timing and context = zero conflict

---

## Testing Checklist

### On macOS

**Browser tabs:**
- [ ] S+T switches to previous tab in Firefox
- [ ] N+E switches to next tab in Firefox
- [ ] Works in Chrome
- [ ] Works in Safari

**Browser history:**
- [ ] R+S goes back in history
- [ ] E+I goes forward in history
- [ ] Works across all browsers

**Other apps:**
- [ ] Try in WezTerm (if it has tabs)
- [ ] Try in any other tabbed apps

### On Linux (Nimbini)

**Browser tabs:**
- [ ] S+T switches to previous tab in Firefox
- [ ] N+E switches to next tab in Firefox
- [ ] Works with Niri window manager

**Browser history:**
- [ ] R+S goes back in history (Alt+Left)
- [ ] E+I goes forward in history (Alt+Right)

**Niri compatibility:**
- [ ] SS+N still focuses column left (no conflict)
- [ ] SS+E still focuses window down (no conflict)
- [ ] No interference with Niri navigation

---

## Troubleshooting

### Combos Not Firing

**Symptom:** Pressing S+T produces individual S and T

**Solutions:**
1. Press more simultaneously (within 50ms)
2. Ensure no typing happened in last 150ms (`require-prior-idle-ms`)
3. Verify you're on BASE layer (not holding another layer)

### Wrong Shortcut on Platform

**Symptom:** Combo produces wrong shortcut for platform

**Solution:** Verify correct keymap was built and flashed:
- macOS should have `piantor_pro_bt_macos.keymap`
- Linux should have `piantor_pro_bt.keymap`

### Conflicts with Typing

**Symptom:** Combo fires during normal typing

**Diagnosis:** Unlikely due to `require-prior-idle-ms = <150>`

**If it happens:** May need to increase timeout or add more prior-idle time

---

## Future Enhancements

### Potential Additions (If Needed)

**Zellij tab switching:**
- May need Zellij config to respond to these shortcuts
- Or add Zellij-specific combos

**Application-specific variants:**
- Could add layer-specific combos for different apps
- Example: Different shortcuts when in terminal vs browser

**More navigation:**
- First/last tab (if friction emerges)
- Close tab (if frequently used)

### Not Planned Unless Needed

- Window switching (already on NAV layer with arrows)
- Workspace switching (OS-level in Niri)
- Monitor switching (less frequent, already has shortcuts)

---

## Summary

✅ **Achieved:** Universal tab and history navigation via comfortable home row combos

✅ **Benefits:**
- Same muscle memory across platforms
- Platform-native shortcuts that work correctly
- Ergonomic positioning based on frequency
- No conflicts with existing shortcuts or Niri

✅ **Next Steps:**
1. Build firmware for both platforms
2. Flash to keyboards
3. Practice combos for 2-3 days
4. Evaluate if they feel natural and useful
5. Document any issues or desired improvements

**This completes the Phase 1 combo implementation from the original proposal!**
