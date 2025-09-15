# Current Keyboard State - Piantor Pro BT Colemak-DH

## Date: 2025-09-15
## Status: WORKING ✅

## Current Configuration

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

### Layer Access
- **BASE**: Default layer, Colemak-DH
- **SYM**: Hold right thumb enter key
- **NUM**: Hold right thumb backspace key
- **NAV**: Hold left thumb space key
- **MOUSE**: Hold left thumb tab key
- **MEDIA**: Hold leftmost thumb key
- **FUN**: Hold rightmost thumb key

## Lessons Learned

### What Worked
1. **Cognitive consistency**: Placing punctuation in same positions across layers dramatically improves usability
2. **Standard keyboard conventions**: Using Shift+EQUAL for PLUS is more intuitive than a dedicated key
3. **Simple layer-tap behaviors**: Basic hold/tap behaviors are reliable and stable

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