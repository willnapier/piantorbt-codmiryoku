# Combo Namespace Inventory - Piantor Pro BT (42-key)

**Date**: 2025-10-06
**Purpose**: Map available combo real-estate for cross-platform shortcut unification

---

## Piantor 42-Key Layout Map

```
Key Position Numbers (0-41):

Left Half:                                Right Half:
 0   1   2   3   4   5                    6   7   8   9  10  11
[none] Q   W   F   P   B                  J   L   U   Y   '   ?
12  13  14  15  16  17                   18  19  20  21  22  23
[SS]  A   R   S   T   G                  M   N   E   I   O  [SS]
24  25  26  27  28  29                   30  31  32  33  34  35
[none] Z   X   C   D   V                  K   H   ,   .   /   :

        36      37      38                39  40  41
        ESC     SPC     TAB               RET BSPC ESC
      (MEDIA) (NAV)  (MOUSE)            (SYM)(NUM)(FUN)

Legend:
- [SS] = Smart Shift (produces ( or ) when shifted)
- [none] = Extra keys on 42-key layout (vs 36-key)
```

### Physical Layout (Colemak-DH Base)
```
Left Hand:
Row 0 (top):    [none]  Q      W      F      P      B
Row 1 (home):   [SS]    A(Ctrl) R(Alt) S(Gui) T(Shft) G
Row 2 (bottom): [none]  Z      X(Alt) C      D      V
Thumbs:         ESC/MEDIA  SPACE/NAV  TAB/MOUSE

Right Hand:
Row 0 (top):    J      L      U      Y      '      ?/!
Row 1 (home):   M      N(Shft) E(Gui) I(Alt) O(Ctrl) [SS]
Row 2 (bottom): K      H      ,      .      /      :
Thumbs:         RET/SYM  BSPC/NUM  ESC/FUN
```

---

## Current Combos in Use

### Horizontal Combos (Adjacent Keys, Same Row)
| Keys | Positions | Output | Layer | Timeout | Status |
|------|-----------|--------|-------|---------|--------|
| L + U | 7, 8 | `:` (colon) | BASE | 50ms | ✅ Active |
| U + Y | 8, 9 | `-` (minus) | BASE | 50ms | ✅ Active |
| , + . | 32, 33 | `?/!` (morph) | BASE | 50ms | ✅ Active |

### Safety Combos
| Keys | Positions | Output | Purpose | Timeout |
|------|-----------|--------|---------|---------|
| A + Z | 13, 25 | `none` | Prevent accidental Ctrl+Z | 50ms |

### Bootloader Combos (Special)
| Keys | Positions | Output | Purpose | Timeout |
|------|-----------|--------|---------|---------|
| Q + W + F | 1, 2, 3 | Bootloader | Left half flash | 100ms |
| U + Y + ' | 8, 9, 10 | Bootloader | Right half flash | 100ms |

---

## Available Combo Real-Estate

### Vertical Combos (Same Column, Adjacent Rows)
Following urob's pattern of vertical combos for symbols/commands:

#### Left Hand Vertical Combos (Available)
| Top + Home | Position | Top + Bottom | Position | Home + Bottom | Position |
|------------|----------|--------------|----------|---------------|----------|
| Q + A | 1, 13 | Q + Z | 1, 25 | A + Z | 13, 25 (USED) |
| W + R | 2, 14 | W + X | 2, 26 | R + X | 14, 26 |
| F + S | 3, 15 | F + C | 3, 27 | S + C | 15, 27 |
| P + T | 4, 16 | P + D | 4, 28 | T + D | 16, 28 |
| B + G | 5, 17 | B + V | 5, 29 | G + V | 17, 29 |

**Total available**: 14 vertical combos (1 used for safety)

#### Right Hand Vertical Combos (Available)
| Top + Home | Position | Top + Bottom | Position | Home + Bottom | Position |
|------------|----------|--------------|----------|---------------|----------|
| J + M | 6, 18 | J + K | 6, 30 | M + K | 18, 30 |
| L + N | 7, 19 | L + H | 7, 31 | N + H | 19, 31 |
| U + E | 8, 20 | U + , | 8, 32 | E + , | 20, 32 |
| Y + I | 9, 21 | Y + . | 9, 33 | I + . | 21, 33 |
| ' + O | 10, 22 | ' + / | 10, 34 | O + / | 22, 34 |

**Total available**: 15 vertical combos

### Horizontal Combos (Same Row, Adjacent Keys)
Following urob's pattern for navigation/editing:

#### Left Hand Horizontal (Available)
**Top Row:**
| Combo | Positions | Status |
|-------|-----------|--------|
| Q + W | 1, 2 | Available (conflicts with bootloader combo) |
| W + F | 2, 3 | Available (conflicts with bootloader combo) |
| F + P | 3, 4 | Available |
| P + B | 4, 5 | Available |

**Home Row:**
| Combo | Positions | Status |
|-------|-----------|--------|
| A + R | 13, 14 | Available |
| R + S | 14, 15 | Available |
| S + T | 15, 16 | Available (urob uses for leader key) |
| T + G | 16, 17 | Available |

**Bottom Row:**
| Combo | Positions | Status |
|-------|-----------|--------|
| Z + X | 25, 26 | Available |
| X + C | 26, 27 | Available |
| C + D | 27, 28 | Available |
| D + V | 28, 29 | Available |

#### Right Hand Horizontal (Available)
**Top Row:**
| Combo | Positions | Status |
|-------|-----------|--------|
| J + L | 6, 7 | Available |
| L + U | 7, 8 | ✅ USED (colon) |
| U + Y | 8, 9 | ✅ USED (minus) |
| Y + ' | 9, 10 | Available (conflicts with bootloader) |

**Home Row:**
| Combo | Positions | Status |
|-------|-----------|--------|
| M + N | 18, 19 | Available |
| N + E | 19, 20 | Available |
| E + I | 20, 21 | Available |
| I + O | 21, 22 | Available |

**Bottom Row:**
| Combo | Positions | Status |
|-------|-----------|--------|
| K + H | 30, 31 | Available |
| H + , | 31, 32 | Available |
| , + . | 32, 33 | ✅ USED (question/exclaim) |
| . + / | 33, 34 | Available |

### Three-Key Combos (More Complex Patterns)
- **Sequential three keys**: Can be used for less common actions
- **Example patterns**: Q+W+F (bootloader), U+Y+' (bootloader)

**Available patterns**: Many, but recommend using sparingly for truly rare actions

---

## Shortcuts Requiring Platform-Specific Handling

### Category 1: Standard Application Shortcuts (High Priority)
**Pattern**: Cmd+key (macOS) vs Ctrl+key (Linux)

| Shortcut | macOS | Linux | Frequency | Priority |
|----------|-------|-------|-----------|----------|
| Copy | Cmd+C | Ctrl+C | Very High | ⭐⭐⭐⭐⭐ |
| Cut | Cmd+X | Ctrl+X | Very High | ⭐⭐⭐⭐⭐ |
| Paste | Cmd+V | Ctrl+V | Very High | ⭐⭐⭐⭐⭐ |
| Undo | Cmd+Z | Ctrl+Z | Very High | ⭐⭐⭐⭐⭐ |
| Redo | Cmd+Shift+Z | Ctrl+Shift+Z | High | ⭐⭐⭐⭐ |
| Save | Cmd+S | Ctrl+S | Very High | ⭐⭐⭐⭐⭐ |
| Find | Cmd+F | Ctrl+F | High | ⭐⭐⭐⭐ |
| Select All | Cmd+A | Ctrl+A | High | ⭐⭐⭐⭐ |
| New Tab | Cmd+T | Ctrl+T | High | ⭐⭐⭐⭐ |
| Close Tab | Cmd+W | Ctrl+W | High | ⭐⭐⭐⭐ |
| Reopen Tab | Cmd+Shift+T | Ctrl+Shift+T | Medium | ⭐⭐⭐ |
| New Window | Cmd+N | Ctrl+N | Medium | ⭐⭐⭐ |
| Close Window | Cmd+Q | Ctrl+Q | Medium | ⭐⭐⭐ |
| Refresh | Cmd+R | Ctrl+R | Medium | ⭐⭐⭐ |

**Total**: 14 shortcuts

### Category 2: Text Navigation (Medium Priority)
**Pattern**: Cmd+arrows (macOS) vs Home/End/Ctrl+arrows (Linux)

| Shortcut | macOS | Linux | Frequency | Priority |
|----------|-------|-------|-----------|----------|
| Line Start | Cmd+Left | Home | High | ⭐⭐⭐⭐ |
| Line End | Cmd+Right | End | High | ⭐⭐⭐⭐ |
| Document Start | Cmd+Up | Ctrl+Home | Medium | ⭐⭐⭐ |
| Document End | Cmd+Down | Ctrl+End | Medium | ⭐⭐⭐ |
| Word Back | Alt+Left | Ctrl+Left | High | ⭐⭐⭐⭐ |
| Word Forward | Alt+Right | Ctrl+Right | High | ⭐⭐⭐⭐ |

**Note**: Word movement works identically with unified HRM (Shift+arrows)

**Total**: 6 shortcuts (4 truly different)

### Category 3: Text Selection (Medium Priority)
**Pattern**: Shift + navigation

| Shortcut | macOS | Linux | Frequency | Priority |
|----------|-------|-------|-----------|----------|
| Select Line Start | Shift+Cmd+Left | Shift+Home | Medium | ⭐⭐⭐ |
| Select Line End | Shift+Cmd+Right | Shift+End | Medium | ⭐⭐⭐ |
| Select Doc Start | Shift+Cmd+Up | Shift+Ctrl+Home | Low | ⭐⭐ |
| Select Doc End | Shift+Cmd+Down | Shift+Ctrl+End | Low | ⭐⭐ |

**Total**: 4 shortcuts

### Category 4: Browser/Tab Navigation (Medium Priority)
| Shortcut | macOS | Linux | Frequency | Priority |
|----------|-------|-------|-----------|----------|
| Next Tab | Cmd+Shift+] | Ctrl+Shift+] | Medium | ⭐⭐⭐ |
| Previous Tab | Cmd+Shift+[ | Ctrl+Shift+[ | Medium | ⭐⭐⭐ |

**Note**: Most handled by Category 1 shortcuts

**Total**: 2 shortcuts

---

## Summary: Combo Real Estate Availability

### Total Available Combos
- **Left hand vertical**: 13 available (14 total, 1 safety combo)
- **Right hand vertical**: 15 available
- **Left hand horizontal**: 11 available (some conflict with bootloader)
- **Right hand horizontal**: 8 available (4 in use)
- **Three-key patterns**: Many available

**Grand Total**: ~47 two-key combos available

### Total Shortcuts Needing Unification
- **Category 1 (Standard shortcuts)**: 14 shortcuts
- **Category 2 (Navigation)**: 4 unique shortcuts
- **Category 3 (Selection)**: 4 shortcuts
- **Category 4 (Tabs)**: 2 shortcuts

**Grand Total**: 24 shortcuts need platform-specific handling

### Verdict: **Plenty of Real Estate** ✅

We have **~47 available combo positions** for **24 required shortcuts**.

This leaves room for:
- Future expansion
- Ergonomic placement optimization
- Memorable, symmetrical patterns (following urob's philosophy)

---

## Next Steps

1. **Prioritize shortcut allocation** - Start with 5-star frequency items
2. **Design ergonomic combo patterns** - Follow urob's vertical/horizontal logic
3. **Implement platform-specific macros** - Use conditional compilation
4. **Test extensively** - Ensure no misfires with require-prior-idle-ms tuning

---

*This inventory provides the foundation for true cross-platform keyboard unification.*
