# Piantor Pro BT Keyboard - Master Documentation Index

**Complete reference for Colemak-DH + Miryoku + Symbol Combos configuration**

**Last Updated:** 2025-10-08
**Status:** Active Development - Layer Optimization Phase

---

## 📖 Quick Start: What You Need to Know

### Current System Status
- ✅ **42-key split keyboard** (Piantor Pro BT with nRF52840 controllers)
- ✅ **Colemak-DH base layout** with home row mods (CAGS: Ctrl, Alt, Gui, Shift)
- ✅ **7 layers**: BASE, SYM, NUM, NAV, MEDIA, MOUSE, FUN
- ✅ **15 active combos**: 11 symbol combos + 4 navigation combos
- ✅ **Dual platform support**: Linux (Nimbini) and macOS (separate keymaps)
- ✅ **Bootloader access**: Layer bindings (SYM/NUM/FUN + ') work on both halves

### What Works Right Now
- **Editing**: Copy/Paste/Cut/Undo/Redo on NAV layer (cross-platform)
- **Symbols**: High-frequency programming symbols via combos (W+F for [], F+P for {}, etc.)
- **Navigation**: Tab switching (S+T, N+E) and history (R+S, E+I) via home row combos
- **Numbers**: Full numpad on NUM layer with cognitive consistency

---

## 🗂️ Documentation Structure

### 1. Essential Reference (Read First)

| File | Purpose | Status | When to Use |
|------|---------|--------|-------------|
| **[CURRENT_STATE.md](./CURRENT_STATE.md)** | **Current working configuration** | ✅ Up-to-date (2025-10-07) | **Start here** - shows what's actually implemented |
| **[CLAUDE.md](./CLAUDE.md)** | Project overview and build commands | ✅ Current | Building firmware, understanding project structure |

### 2. Layer System Documentation

| File | Purpose | Status | Focus |
|------|---------|--------|-------|
| **[LAYER-OPTIMIZATION-TRACKING.md](./LAYER-OPTIMIZATION-TRACKING.md)** | **Layer redundancy analysis and optimization** | ✅ Active (2025-10-08) | **Current work** - identifying free slots for new functions |
| [CROSS-PLATFORM-KEYMAP-GUIDE.md](./CROSS-PLATFORM-KEYMAP-GUIDE.md) | Dual keymap system (Linux vs macOS) | ✅ Current (2025-10-07) | Understanding platform-specific edit commands |
| [PLATFORM-SPECIFIC-KEYMAPS.md](./PLATFORM-SPECIFIC-KEYMAPS.md) | Quick reference for platform differences | ✅ Current (2025-10-07) | Quick lookup of Ctrl vs Cmd bindings |

### 3. Combo System Documentation

| File | Purpose | Status | Focus |
|------|---------|--------|-------|
| **[SYMBOL-COMBOS-IMPLEMENTATION.md](./SYMBOL-COMBOS-IMPLEMENTATION.md)** | **Complete symbol combo reference** | ✅ Implemented | Using symbol combos (W+F, I+O, etc.) |
| [TAB-HISTORY-COMBOS-IMPLEMENTATION.md](./TAB-HISTORY-COMBOS-IMPLEMENTATION.md) | Navigation combo reference | ✅ Implemented | Browser/editor tab and history navigation |
| [COMBO-ALLOCATION-PROPOSAL.md](./COMBO-ALLOCATION-PROPOSAL.md) | Original design philosophy and proposals | 📚 Historical (2025-10-07) | Understanding design decisions |
| [COMBO-NAMESPACE-INVENTORY.md](./COMBO-NAMESPACE-INVENTORY.md) | Available combo positions analysis | 📚 Reference (2025-10-06) | Finding available combo slots |

### 4. Specialized Topics

| File | Purpose | Status | Focus |
|------|---------|--------|-------|
| [NUM_WORD_IMPLEMENTATION.md](./NUM_WORD_IMPLEMENTATION.md) | num_word behavior documentation | ⚠️ **NOT IN USE** | **Avoided** - caused keyboard malfunctions |
| [NUM_WORD_PROBLEM_ANALYSIS.md](./NUM_WORD_PROBLEM_ANALYSIS.md) | Why num_word was removed | 📚 Historical | Understanding stability issues |
| [SCREENSHOT_PROJECT_STATUS.md](./SCREENSHOT_PROJECT_STATUS.md) | Screenshot automation project | ⏸️ Separate project | Niri screenshot hotkeys |
| [NIMBINI-SETUP-NOTES.md](./NIMBINI-SETUP-NOTES.md) | Linux machine setup notes | ✅ Reference | Setting up Linux environment |

---

## 🎯 Current Focus: Layer Optimization (2025-10-08)

### The Discovery
**SYM and NUM layers have significant overlap** - same symbols accessible via both layers (and sometimes combos too!). This creates wasted "prime real estate" that could be used for new functions.

### Active Work
See **[LAYER-OPTIMIZATION-TRACKING.md](./LAYER-OPTIMIZATION-TRACKING.md)** for:
- Complete redundancy analysis (9 symbols with double coverage)
- Identification of 9 freed prime slots (7 on SYM, 2 on NUM)
- Decision framework for what to allocate to freed slots
- Implementation strategy (conservative vs aggressive)

### Key Insights
1. **Bracket combos (W+F, F+P) so convenient** → Remove redundant layer bindings
2. **Smart Shift handles () perfectly** → Remove from layers
3. **NUM+Shift provides traditional symbols** (Shift+1 = !, Shift+2 = @, etc.) → Migrate less-frequent symbols

---

## 📋 Implementation Status Summary

### ✅ Implemented and Working

**Symbol Combos (11 total):**
- L+U → `:` / `;` (colon/semicolon)
- U+Y → `-` (minus)
- ,+. → `?` (question mark)
- A+R → `#` (hash)
- W+F → `[` / `{` (brackets)
- F+P → `]` / `}` (brackets)
- I+O → `'` / `"` (quotes)
- X+C → `@` (at)
- C+D → `|` (pipe)
- H+, → `+` (plus)
- .+/ → `!` (exclamation)

**Navigation Combos (4 total):**
- S+T → Previous tab (Cmd+Shift+[ on macOS, Ctrl+PgUp on Linux)
- N+E → Next tab (Cmd+Shift+] on macOS, Ctrl+PgDn on Linux)
- R+S → Back in history (Cmd+[ on macOS, Alt+Left on Linux)
- E+I → Forward in history (Cmd+] on macOS, Alt+Right on Linux)

**Layer Bindings:**
- NAV layer: Copy/Paste/Cut/Undo/Redo (cross-platform)
- Bootloader access: SYM/NUM/FUN + ' (works on both halves)

### ⏳ In Progress

**Layer Optimization:**
- Identifying redundant bindings
- Planning freed slot allocation
- User preference gathering

### ❌ Removed (With Good Reason)

**Bootloader Combos:**
- Q+W+F (left half) - Removed 2025-10-08
- U+Y+' (right half) - Removed 2025-10-08
- **Reason:** ZMK limitation - combos only trigger on central half, layer bindings work better

**num_word Behavior:**
- **Reason:** Caused keyboard malfunctions and stuck keys
- See: NUM_WORD_PROBLEM_ANALYSIS.md

---

## 🔧 Common Tasks Reference

### How to Access Bootloader Mode

**Both Halves (Reliable Method):**
1. Hold layer: SYM (RET), NUM (BSPC), or FUN (ESC)
2. While holding, tap `'` (top-right key)
3. Controller enters bootloader, shows as NICENANO USB drive

**To Exit Bootloader Without Flashing:**
- Power cycle (disconnect/reconnect USB or battery)
- Single reset tap (RST to GND once, not double-tap)
- Flash any .uf2 file (even CURRENT.UF2 from the drive)

### How to Use Symbol Combos

**Press both keys simultaneously** (within 50ms) **after a brief pause** (150ms):

```
For [: Press W+F together
For ": Hold Shift, press I+O together
For #: Press A+R together
```

**Full reference:** [SYMBOL-COMBOS-IMPLEMENTATION.md](./SYMBOL-COMBOS-IMPLEMENTATION.md)

### How to Switch Tabs/Navigate History

**Tab switching (same as browser/editor):**
- S+T → Previous tab
- N+E → Next tab

**History navigation:**
- R+S → Back
- E+I → Forward

**Full reference:** [TAB-HISTORY-COMBOS-IMPLEMENTATION.md](./TAB-HISTORY-COMBOS-IMPLEMENTATION.md)

### How to Build Firmware

**For Linux (Nimbini) - Default:**
```bash
# Left half
west build -s zmk/app -b piantor_pro_bt_left -- -DSHIELD=nice_view

# Right half (clean build)
west build --pristine -s zmk/app -b piantor_pro_bt_right -- -DSHIELD=nice_view
```

**For macOS - Use macOS keymap:**
```bash
# Left half
west build -s zmk/app -b piantor_pro_bt_left -- \
  -DZMK_CONFIG="$(pwd)/config" \
  -DKEYMAP_FILE="$(pwd)/config/piantor_pro_bt_macos.keymap" \
  -DSHIELD=nice_view

# Right half
west build --pristine -s zmk/app -b piantor_pro_bt_right -- \
  -DZMK_CONFIG="$(pwd)/config" \
  -DKEYMAP_FILE="$(pwd)/config/piantor_pro_bt_macos.keymap" \
  -DSHIELD=nice_view
```

**Output location:** `build/zephyr/zmk.uf2`

---

## 🗺️ Visual Layer Maps

### BASE Layer (Colemak-DH)
```
Q  W  F  P  B      J  L  U  Y  '  ?
A  R  S  T  G      M  N  E  I  O  Shift
Z  X  C  D  V      K  H  ,  .  /  :

   ESC SPC TAB    RET BSP ESC
   MED NAV MOU    SYM NUM FUN
```

**Home Row Mods (Miryoku):**
- A: Ctrl | R: Alt | S: Gui | T: Shift
- N: Shift | E: Gui | I: Alt | O: Ctrl

### Symbol Combo Positions
```
       W─F        I─O          [] and {}    Quotes
A─R                            Hash
       X─C        C─D          @ and |
       H─,        .─/          + and !
       L─U                     : and ;
```

**See full combo table:** [SYMBOL-COMBOS-IMPLEMENTATION.md](./SYMBOL-COMBOS-IMPLEMENTATION.md)

### NAV Layer (Right Hand)
```
Hold SPACE (left thumb) + right hand:
  J → Redo (Ctrl/Cmd+Y)
  L → Paste (Ctrl/Cmd+V)
  U → Copy (Ctrl/Cmd+C)
  Y → Cut (Ctrl/Cmd+X)
  ' → Undo (Ctrl/Cmd+Z, double-tap)

  ← ↓ ↑ →  Arrow keys
```

**Platform-specific:** Uses LC() on Linux, LG() on macOS
**Full details:** [CROSS-PLATFORM-KEYMAP-GUIDE.md](./CROSS-PLATFORM-KEYMAP-GUIDE.md)

---

## 📝 Design Philosophy Summary

### Core Principles

1. **Frequency × Ergonomics** - Most common operations get most comfortable positions (Colemak-DH principle)

2. **Redundancy Elimination** - If accessible 3 ways, keep the best method only

3. **Layer vs Combo Decision:**
   - **Layers** for mode-specific operations (NAV for editing, NUM for numbers)
   - **Combos** for universal symbols accessible from BASE layer
   - **OS-level** for window/app management (respect platform paradigms)

4. **Cross-Platform First** - Maintain separate keymaps for platform-specific commands, everything else identical

5. **Observation-Driven Design** - Add complexity only when real usage reveals friction

### What Makes a Good Combo vs Layer Binding

**Use Combos For:**
- High-frequency symbols needed from BASE layer ([], {}, ", #, etc.)
- Universal operations that shouldn't require mode switch
- Things you use constantly while typing prose

**Use Layer Bindings For:**
- Mode-specific operations (editing commands on NAV)
- Number entry (numpad on NUM layer)
- Function keys, media controls, system functions
- Things that benefit from holding a layer vs precise timing

**Use OS-Level For:**
- Window management (Cmd+Tab, Super+Space)
- Application launching (Alfred, rofi)
- Compositor-specific features (Niri column navigation)

---

## 🔍 Finding What You Need

### "I want to understand..."

**...the current keyboard layout**
→ [CURRENT_STATE.md](./CURRENT_STATE.md)

**...how symbol combos work**
→ [SYMBOL-COMBOS-IMPLEMENTATION.md](./SYMBOL-COMBOS-IMPLEMENTATION.md)

**...why Linux and macOS have different keymaps**
→ [CROSS-PLATFORM-KEYMAP-GUIDE.md](./CROSS-PLATFORM-KEYMAP-GUIDE.md)

**...what layer slots are available for new functions**
→ [LAYER-OPTIMIZATION-TRACKING.md](./LAYER-OPTIMIZATION-TRACKING.md) (current work)

**...why certain design decisions were made**
→ [COMBO-ALLOCATION-PROPOSAL.md](./COMBO-ALLOCATION-PROPOSAL.md) (design philosophy)

### "I want to do..."

**...add a new symbol combo**
1. Check [COMBO-NAMESPACE-INVENTORY.md](./COMBO-NAMESPACE-INVENTORY.md) for available positions
2. See [SYMBOL-COMBOS-IMPLEMENTATION.md](./SYMBOL-COMBOS-IMPLEMENTATION.md) for implementation pattern
3. Update both `piantor_pro_bt.keymap` and `piantor_pro_bt_macos.keymap`

**...optimize layer bindings**
1. Start with [LAYER-OPTIMIZATION-TRACKING.md](./LAYER-OPTIMIZATION-TRACKING.md)
2. Identify redundancies using the analysis tables
3. Propose new allocations following the decision framework

**...enter bootloader mode**
→ Hold SYM/NUM/FUN + tap ' (see "Common Tasks Reference" above)

**...build firmware**
→ See "Common Tasks Reference" above or [CLAUDE.md](./CLAUDE.md)

---

## 📊 File Relationships Diagram

```
KEYBOARD-MASTER-INDEX.md (You are here!)
    │
    ├─ CURRENT_STATE.md ⭐ START HERE
    │   └─ Shows what's actually implemented right now
    │
    ├─ Layer System Documentation
    │   ├─ LAYER-OPTIMIZATION-TRACKING.md ⭐ ACTIVE WORK
    │   │   └─ Identifies redundant bindings and freed slots
    │   ├─ CROSS-PLATFORM-KEYMAP-GUIDE.md
    │   │   └─ Explains Linux (LC) vs macOS (LG) differences
    │   └─ PLATFORM-SPECIFIC-KEYMAPS.md
    │       └─ Quick reference table
    │
    ├─ Combo System Documentation
    │   ├─ SYMBOL-COMBOS-IMPLEMENTATION.md ⭐ REFERENCE
    │   │   └─ Complete guide to all 11 symbol combos
    │   ├─ TAB-HISTORY-COMBOS-IMPLEMENTATION.md
    │   │   └─ Navigation combo guide (tab switching, history)
    │   ├─ COMBO-ALLOCATION-PROPOSAL.md
    │   │   └─ Original design philosophy and decisions
    │   └─ COMBO-NAMESPACE-INVENTORY.md
    │       └─ Available combo position analysis
    │
    └─ Specialized / Historical
        ├─ NUM_WORD_PROBLEM_ANALYSIS.md (⚠️ AVOID)
        ├─ SCREENSHOT_PROJECT_STATUS.md (separate project)
        └─ NIMBINI-SETUP-NOTES.md (Linux setup)
```

---

## 🚀 Next Steps / Active Threads

### Immediate (Layer Optimization - Started 2025-10-08)

1. **Complete redundancy analysis** in LAYER-OPTIMIZATION-TRACKING.md
2. **Get user confirmation** on which symbols to keep vs migrate
3. **Identify top 3-5 functions** for freed prime slots
4. **Implement conservative cleanup** (remove confirmed redundancies)
5. **Test for 1 week** and observe friction points

### Near Future

1. **Firmware build and flash** optimized layers
2. **Real-world usage observation** for 1-2 weeks
3. **Evaluate need for additional combos** based on friction points
4. **Consider aggressive optimization** if conservative approach works well

### Long Term

1. **Document final optimized layout** in CURRENT_STATE.md
2. **Update all relevant docs** to reflect changes
3. **Establish maintenance rhythm** for keeping docs current

---

## 📜 Document Maintenance

### When to Update This Index

- New documentation file created → Add to appropriate section
- File becomes outdated → Mark as historical or remove
- Major feature implemented → Update "Implementation Status Summary"
- Design philosophy changes → Update "Design Philosophy Summary"

### Version History

- **2025-10-08** - Initial master index created, consolidated 13 docs
- **2025-10-07** - Symbol combos and tab/history navigation implemented
- **2025-10-07** - Dual keymap system established (Linux/macOS)

---

_This master index provides a comprehensive overview and navigation system for all Piantor Pro BT keyboard documentation. Start with [CURRENT_STATE.md](./CURRENT_STATE.md) to see what's actually working right now, then dive into specific topics as needed._
