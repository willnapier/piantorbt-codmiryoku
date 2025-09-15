# num_word Implementation Problem Analysis

## Problem Statement
**Goal**: Implement urob's num_word behavior with dual functionality on leftmost thumb key:
- **Tap**: Activate num_word (automatic number layer)
- **Hold**: Access MEDIA layer

**Outcome**: Complete keyboard malfunction requiring emergency fixes

## Implementation Attempts

### Attempt 1: Custom Hold-Tap Behavior
```c
media_num: media_num {
    compatible = "zmk,behavior-hold-tap";
    #binding-cells = <2>;
    flavor = "tap-preferred";
    tapping-term-ms = <200>;
    bindings = <&mo>, <&num_word>;
};
```

**Usage**: `&media_num MEDIA NUM`

**Problem**: Invalid parameter syntax - num_word doesn't accept parameters
**Symptom**: Complete keyboard malfunction, all layers unresponsive

### Attempt 2: Layer Numbers Instead of Names
**Change**: `&media_num 4 0` (MEDIA=4, NUM=2 but using 0)

**Problem**: Still incorrect - num_word is standalone behavior
**Symptom**: Build errors continued

### Attempt 3: Direct num_word Usage
**Change**: `&num_word` (no parameters)

**Problem**: Lost MEDIA layer access
**Symptom**: Partial solution but missing required functionality

### Attempt 4: Tap-Dance Behavior
```c
td_num_media: tap_dance_num_media {
    compatible = "zmk,behavior-tap-dance";
    label = "TAP_DANCE_NUM_MEDIA";  // <- Deprecated property
    #binding-cells = <0>;
    tapping-term-ms = <200>;
    bindings = <&num_word>, <&mo MEDIA>;
};
```

**Problem**: Build failure due to deprecated 'label' property
**Error**: `'label' is marked as deprecated in 'properties:' in /zmk/app/dts/bindings/behaviors/zmk,behavior-tap-dance.yaml`

### Attempt 5: Tap-Dance Without Label
**Change**: Removed deprecated 'label' property

**Problem**: Deeper devicetree error
**Error**: `devicetree error: <Node /soc/gpio@50000000> lacks #binding-cells`

## Build Errors

### Error Sequence
1. **Parameter Error**: Invalid hold-tap usage with num_word
2. **Deprecated Property**: tap-dance 'label' property removed in newer ZMK
3. **GPIO Binding Error**: Fundamental devicetree issue suggesting deeper configuration problem

### Critical Error Messages
```
devicetree error: <Node /soc/gpio@50000000 in '/tmp/zmk-config/zephyr/misc/empty_file.c'> lacks #binding-cells
CMake Error at /tmp/zmk-config/zephyr/cmake/modules/dts.cmake:279 (message):
  gen_defines.py failed with return code: 1
```

This suggests the custom behaviors were somehow corrupting the base board devicetree configuration.

## User Experience Impact

### Complete Malfunction Symptoms
- **No layer switching**: NAV, SYM, NUM layers inaccessible
- **Frozen state**: Keyboard appeared stuck in unknown layer state
- **Unresponsive**: Power cycling didn't resolve issues
- **Hardware concerns**: Difficulty entering bootloader mode on right half

### Emergency Recovery
Required reverting to simple `&lt MEDIA ESC` layer-tap to restore functionality.

## Technical Analysis

### What We Know Works
- **Standard layer-tap**: `&lt LAYER KEY` syntax is stable and reliable
- **Simple behaviors**: Basic hold-tap, mod-tap, tap-dance work fine
- **urob's num_word**: The behavior itself functions when used correctly

### What Failed
- **Custom hold-tap with num_word**: Incompatible behavior combination
- **Parameter passing to num_word**: num_word doesn't accept runtime parameters
- **Complex behavior chaining**: Multiple custom behaviors caused instability

### Hypotheses for Failure

#### 1. Behavioral Incompatibility
num_word might be designed as an endpoint behavior that cannot be wrapped in other behaviors like hold-tap.

#### 2. Parameter Architecture Mismatch
num_word configuration might be compile-time only (via behavior definition) rather than runtime parameters.

#### 3. State Machine Conflicts
num_word's auto-layer functionality might conflict with manual layer switching in hold-tap behaviors.

#### 4. Resource Conflicts
Custom behaviors might have exceeded ZMK's behavior definition limits or created circular dependencies.

## Questions for Investigation

### Architecture Questions
1. **Is num_word compatible with hold-tap wrapping?**
   - Can num_word be the "tap" behavior in a hold-tap definition?
   - Are there examples of this working in other configurations?

2. **How should num_word layer be configured?**
   - Should layer be defined in the behavior (`layers = <NUM>;`) or passed as parameter?
   - What's the correct syntax for urob's zmk-auto-layer module?

3. **What caused the complete keyboard malfunction?**
   - Why did invalid behavior syntax break ALL layer switching?
   - How did custom behaviors affect base GPIO configuration?

### Implementation Questions
1. **Alternative approaches:**
   - Combo-based num_word activation?
   - Different key placement for dual functionality?
   - Separate keys for num_word and MEDIA?

2. **Build system issues:**
   - Why did deprecated 'label' property cause GPIO errors?
   - Are there ZMK version compatibility issues?
   - Should zmk-auto-layer module be configured differently?

3. **Recovery mechanisms:**
   - How to test complex behaviors safely?
   - Emergency firmware backup strategies?
   - Better debugging approaches for behavior issues?

## Current Working Configuration

### Baseline That Works
```c
// Simple layer-tap - reliable and stable
&lt MEDIA ESC    // Hold for MEDIA, tap for ESC
```

### NUM Layer Optimizations Retained
Despite num_word failure, valuable improvements were preserved:
- Cognitive consistency (punctuation in matching positions across layers)
- Leveraged standard keyboard shift behaviors
- Simplified key mappings

## Recommendations for Future Attempts

### Safety Measures
1. **Incremental testing**: Test each behavior change separately
2. **Backup firmware**: Keep known-working build available
3. **Branch-based development**: Use git branches for experimental features

### Alternative Approaches
1. **Combo activation**: Use key combinations for num_word instead of layer-tap
2. **Dedicated key**: Sacrifice a less-critical key for num_word
3. **Macro-based solution**: Custom macro that activates num_word and handles layer switching

### Research Needed
1. **ZMK documentation deep-dive**: Behavior composition rules and limitations
2. **Community examples**: Look for working num_word + other behavior combinations
3. **urob's configurations**: Study how the author implements num_word in practice

## Lessons Learned

### Technical
- Custom behavior combinations can cause catastrophic failures
- ZMK's error messages don't always point to root cause
- Simple solutions are often more reliable than clever ones

### Process
- Always maintain working firmware backup
- Test incrementally rather than combining multiple changes
- Document error messages completely for later analysis

### Design Philosophy
- Stability trumps feature completeness
- User experience degradation is worse than missing features
- Cognitive consistency improvements have lasting value even without advanced features

## Files for Reference
- `config/piantor_pro_bt.keymap` - Current working configuration
- Git commits `3760fdd` through `6355725` - Failed implementation attempts
- Build logs from GitHub Actions - Specific error messages
- `NUM_WORD_IMPLEMENTATION.md` - Detailed implementation journey