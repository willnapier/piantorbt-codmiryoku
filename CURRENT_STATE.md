# Current Keyboard State - Piantor Pro BT Colemak-DH

## Date: 2025-10-07
## Status: WORKING ✅ - Dual Platform Support

## Current Configuration

### Platform-Specific Keymaps (NEW 2025-10-07)

**Two keymap files now maintained:**

1. **`piantor_pro_bt.keymap`** - Linux version (Nimbini)
   - Uses `LC()` (Ctrl) for edit commands
   - Uses `td_ctrlz` tap dance behavior for undo
   - Built automatically by GitHub Actions

2. **`piantor_pro_bt_macos.keymap`** - macOS version
   - Uses `LG()` (Cmd) for edit commands
   - Uses `td_cmdz` tap dance behavior for undo
   - Built manually on local machine

**Differences limited to NAV and MOUSE layers only** - all other layers identical.

### Base Layer Changes
- **Z key**: Simple `&kp Z` (removed redundant `&lt BUTTON Z` layer-tap)
- **Leftmost thumb**: `&lt MEDIA ESC` (hold for MEDIA layer, tap for ESC)
- **Other thumbs**: Unchanged (NAV/SPACE, MOUSE/TAB, SYM/RET, NUM/BSPC, FUN/ESC)

### NUM Layer Optimizations
Complete cognitive consistency achieved with punctuation positions:

```
Row 0: [trans] [ [ ]  [ 7 ]  [ 8 ]  [ 9 ]  [ ] ]  [none] [BASE] [none] [none] [BOOT] [trans]
Row 1: [trans] [ ` ]  [ 4 ]  [ 5 ]  [ 6 ]  [ = ]  [ 0 ]  [SHFT] [GUI]  [ALT]  [CTRL] [ - ]
Row 2: [trans] [ ~ ]  [ 1 ]  [ 2 ]  [ 3 ]  [none] [ * ]  [NUM]  [ , ]  [ . ]  [ / ]  [RESET]
Thumbs:        [none] [SPC]  [none] [none] [none] [DEL]
```

**Key improvements:**
- **MINUS** at [1,11] - same position as NAV layer
- **COMMA** at [2,8] - same position as BASE layer
- **DOT** at [2,9] - same position as BASE layer
- **FSLH** at [2,10] - same position as BASE layer
- **TILDE** at [2,1] - same position as SYM layer
- **PLUS** via Shift+EQUAL (removed redundant key, leveraging standard keyboard behavior)

### What Was Removed
- **num_word behavior**: Caused keyboard malfunction, removed for stability
- **media_num custom behavior**: Complex hold-tap that caused build issues
- **Manual PLUS key**: Redundant since Shift+EQUAL produces PLUS
- **BUTTON layer dual-function**: Redundant with MOUSE layer

### Mathematical Operations
All mathematical operations remain fully functional:
- **Numbers**: 0-9 in standard numpad layout
- **Operators**: `+ - * / =` all accessible
- **Formatting**: `, .` for thousands and decimals
- **Grouping**: `[ ]` brackets, `( )` via smart shift

### Symbol Combos (NEW 2025-10-07)

**11 symbol combos for ergonomic programming:**

| Combo | Keys | Output | Use Cases |
|-------|------|--------|-----------|
| **Original (Pre-existing)** |
| L+U | 7, 8 | `:` / `;` (shifted) | Python, CSS, general punctuation |
| U+Y | 8, 9 | `-` | Minus, hyphen, option flags |
| ,+. | 32, 33 | `?` / `!` (shifted) | Questions, exclamations |
| **NEW (2025-10-07)** |
| A+R | 13, 14 | `#` | Comments, headers, shell |
| W+F | 2, 3 | `[` / `{` (shifted) | Arrays, dicts, JSON, code blocks |
| F+P | 3, 4 | `]` / `}` (shifted) | Closing brackets |
| I+O | 21, 22 | `'` / `"` (shifted) | String literals, quotes |
| C+D | 26, 27 | `|` | Shell pipes, regexes, OR logic |
| X+C | 25, 26 | `@` | Email, handles, decorators |
| H+, | 31, 32 | `+` | Addition, concatenation |
| .+/ | 33, 34 | `£` | UK currency symbol |

**Technical details:**
- All combos use `timeout-ms = <50>` (fast simultaneous press)
- All combos use `require-prior-idle-ms = <150>` (prevent accidental firing)
- Active on BASE layer only
- Shift-aware combos use mod-morph behaviors
- 2-3x faster than switching to SYM layer

**See:** [SYMBOL-COMBOS-IMPLEMENTATION.md](./SYMBOL-COMBOS-IMPLEMENTATION.md) for complete documentation

### Navigation Combos (NEW 2025-10-07)

**4 home row combos for tab and history navigation:**

| Combo | Keys | macOS Shortcut | Linux Shortcut | Function |
|-------|------|---------------|----------------|----------|
| S+T | 15, 16 | Cmd+Shift+[ | Ctrl+PgUp | Previous tab |
| N+E | 19, 20 | Cmd+Shift+] | Ctrl+PgDn | Next tab |
| R+S | 14, 15 | Cmd+[ | Alt+Left | Back in history |
| E+I | 20, 21 | Cmd+] | Alt+Right | Forward in history |

**Design rationale:**
- Most frequent (tabs) on inner positions (S+T, N+E)
- Less frequent (history) on outer positions (R+S, E+I)
- Left hand = "previous/back" semantic
- Right hand = "next/forward" semantic

**See:** [TAB-HISTORY-COMBOS-IMPLEMENTATION.md](./TAB-HISTORY-COMBOS-IMPLEMENTATION.md) for complete documentation

### NAV Layer Edit Commands (2025-10-07)

**Cross-platform edit commands on right hand top row:**

| Action | macOS Version | Linux Version | Base Key |
|--------|--------------|---------------|----------|
| Redo   | Cmd+Y | Ctrl+Y | J (pos 6) |
| Paste  | Cmd+V | Ctrl+V | L (pos 7) |
| Copy   | Cmd+C | Ctrl+C | U (pos 8) |
| Cut    | Cmd+X | Ctrl+X | Y (pos 9) |
| Undo   | Cmd+Z (double-tap) | Ctrl+Z (double-tap) | ' (pos 10) |

**Usage:** Hold NAV (left thumb on SPACE) + press right hand key

**Also available on MOUSE layer** with identical mappings

### Layer Access
- **BASE**: Default layer, Colemak-DH
- **SYM**: Hold right thumb enter key
- **NUM**: Hold right thumb backspace key
- **NAV**: Hold left thumb space key (includes edit commands)
- **MOUSE**: Hold left thumb tab key (includes edit commands)
- **MEDIA**: Hold leftmost thumb key
- **FUN**: Hold rightmost thumb key

## Lessons Learned

### What Worked
1. **Cognitive consistency**: Placing punctuation in same positions across layers dramatically improves usability
2. **Standard keyboard conventions**: Using Shift+EQUAL for PLUS is more intuitive than a dedicated key
3. **Simple layer-tap behaviors**: Basic hold/tap behaviors are reliable and stable
4. **Platform-specific keymaps** (2025-10-07): Separate keymap files for macOS/Linux provides true cross-platform support without complexity
5. **NAV layer edit commands**: Placing Copy/Paste/Cut/Undo/Redo on NAV layer provides ergonomic, consistent access across platforms
6. **Symbol combos** (2025-10-07): Frequency-driven combo allocation provides 2-3x faster access to programming symbols than SYM layer
7. **Navigation combos** (2025-10-07): Home row tab/history navigation with platform-specific macros provides universal browser navigation

### What Failed
1. **Complex custom behaviors**: media_num hold-tap with num_word caused complete keyboard failure
2. **Parameter confusion**: Mixing layer names vs numbers in behavior definitions
3. **Over-engineering**: Trying to pack too much functionality into single keys

### Future Considerations
If num_word is reconsidered:
1. Use combos instead of layer-tap
2. Test extensively in separate branch
3. Keep emergency firmware backup ready
4. Consider if the complexity is worth the benefit

## Build Information
- **Board**: piantor_pro_bt (left/right)
- **Shield**: nice_view
- **Base firmware**: ZMK main branch
- **Additional modules**: urob/zmk-auto-layer v0.2 (currently unused)
- **Build system**: GitHub Actions

## Known Issues
- None currently - keyboard fully functional

## Documentation
- See `NUM_WORD_IMPLEMENTATION.md` for the full journey and why num_word was removed
- See `CLAUDE.md` for project overview and quick commands
- See `SYMBOL-COMBOS-IMPLEMENTATION.md` for complete symbol combo documentation (2025-10-07)
- See `TAB-HISTORY-COMBOS-IMPLEMENTATION.md` for navigation combo documentation (2025-10-07)
- See `CROSS-PLATFORM-KEYMAP-GUIDE.md` for platform-specific keymap details (2025-10-07)
- See `COMBO-ALLOCATION-PROPOSAL.md` for complete combo design philosophy and allocation