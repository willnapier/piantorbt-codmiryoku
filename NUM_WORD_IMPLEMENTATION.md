# num_word Implementation Documentation

## Overview
~~Complete implementation~~ **REMOVED** - urob's num_word behavior for the Piantor Pro BT keyboard with Colemak-DH base layer. This document captures the design decisions, pitfalls avoided, ~~and final optimized solution~~ and why it was ultimately removed on 2025-09-15.

## UPDATE: num_word Removed
After extensive implementation work, num_word was removed due to causing complete keyboard malfunction. The complex custom behaviors required created build errors and rendered the keyboard unusable. Decision made to prioritize stability over this feature.

## The Challenge
Implement num_word (automatic number layer) functionality that:
- Activates NUM layer with single tap
- Continues for numbers and mathematical operators
- Exits cleanly without trapping users
- Maintains cognitive consistency across layers
- Leverages standard keyboard conventions

## Implementation Journey

### Initial Problems
1. **Include Path Issues**: Failed build with `#include "zmk-auto-layer/auto_layer.dtsi"`
   - **Solution**: Use pre-built behavior `#include <behaviors/num_word.dtsi>`

2. **Syntax Errors**: Invalid layer-tap syntax `&lt MEDIA num_word`
   - **Solution**: Create custom hold-tap behavior `media_num`

3. **User Traps**: Critical design flaws that would trap users in NUM layer
   - **SPACE trap**: NUM layer had `&kp N0` on SPACE thumb
   - **ENTER trap**: Conditional SYM access would prevent ENTER from exiting
   - **MINUS trap**: MINUS only on NAV layer, but NAV access exits num_word

### Key Design Decisions

#### 1. Custom media_num Behavior
```c
media_num: media_num {
    compatible = "zmk,behavior-hold-tap";
    #binding-cells = <2>;
    flavor = "tap-preferred";
    tapping-term-ms = <200>;
    bindings = <&mo>, <&num_word>;
};
```
- **Tap**: Activates num_word
- **Hold**: Activates MEDIA layer
- **Position**: Leftmost left thumb (replacing redundant ESC)

#### 2. Cognitive Consistency
Punctuation placed in exact same positions across layers:
- **MINUS**: Position [1,11] - matches NAV layer
- **COMMA**: Position [2,8] - matches BASE layer
- **DOT**: Position [2,9] - matches BASE layer
- **FSLH**: Position [2,10] - matches BASE layer

#### 3. Leveraging Standard Keyboard Shift Behavior
Discovery: Miryoku philosophy uses standard shift behaviors rather than explicit key placement
- **Removed manual PLUS**: Shift+EQUAL naturally produces PLUS
- **Freed position [2,1]**: Available for future optimizations
- **Maintains full functionality**: All math operations accessible

## Final NUM Layer Layout

```
Row 0: [trans] [ [ ]  [ 7 ]  [ 8 ]  [ 9 ]  [ ] ]  [none] [BASE] [none] [none] [BOOT] [trans]
Row 1: [trans] [ ` ]  [ 4 ]  [ 5 ]  [ 6 ]  [ = ]  [ 0 ]  [SHFT] [GUI]  [ALT]  [CTRL] [ - ]
Row 2: [trans] [none] [ 1 ]  [ 2 ]  [ 3 ]  [none] [ * ]  [NUM]  [ , ]  [ . ]  [ / ]  [RESET]
Thumbs:        [none] [SPC]  [none] [none] [none] [DEL]
```

## num_word Behavior

### Continuation Characters (stay in NUM layer)
- Numbers: 0-9
- DOT (.)
- COMMA (,)
- MINUS (-)
- FSLH (/)
- EQUAL (=)
- BACKSPACE/DELETE

### Exit Characters
- SPACE (primary exit)
- ENTER (secondary exit)
- STAR (*) - intentionally exits for deliberate operations
- Any letter or non-continuation character
- Transparent keys that fall through to BASE layer

### Mathematical Operations
- **Addition**: Use Shift+EQUAL for PLUS
- **Subtraction**: Direct MINUS key
- **Multiplication**: STAR key (exits num_word)
- **Division**: FSLH key (continues num_word)
- **Decimals**: DOT key
- **Thousands**: COMMA key

## Lessons Learned

### 1. Test Exit Mechanisms
Always ensure multiple clean exit paths from any modal state. Users should never be trapped.

### 2. Cognitive Consistency Matters
Placing punctuation in the same physical positions across layers reduces cognitive load and improves muscle memory.

### 3. Leverage Existing Standards
Using standard keyboard shift behaviors (like Shift+EQUAL = PLUS) is more intuitive than custom mappings.

### 4. Transparent Fallthrough Behavior
`&trans` keys evaluate their final resolved keycode against continue-list, providing natural exit points.

### 5. Simple Solutions Often Best
Direct key placement proved superior to complex conditional layer switching proposals.

## Testing Confirmation
Tested and working as of 2025-09-15:
- ✅ All numbers accessible and continue num_word
- ✅ Mathematical operators working correctly
- ✅ Clean exits via SPACE and ENTER
- ✅ Shift+EQUAL produces PLUS
- ✅ No user traps or stuck states
- ✅ Cognitive consistency maintained

## Future Optimization Opportunities
- Position [2,1] available for dual-purpose key (e.g., `&kp N5` for 5 and Shift+5 for %)
- Position [2,5] available for additional functionality
- Consider adding STAR to continue-list if continuous multiplication desired

## Configuration Files
- **Keymap**: `config/piantor_pro_bt.keymap`
- **Module**: Uses urob's zmk-auto-layer v0.2
- **Build**: GitHub Actions automatic firmware generation

## Credits
- urob's zmk-auto-layer module for num_word behavior
- Miryoku layout philosophy for cognitive consistency principles
- ZMK firmware for flexible behavior system