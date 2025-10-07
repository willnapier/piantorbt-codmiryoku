# Piantor Pro BT Combo Allocation Proposal

**Cross-Platform Keyboard Shortcuts for Colemak-DH + Miryoku + CAGS HRMs**

**Last Updated:** 2025-10-07
**Status:** In Design Review - Revised Architecture

---

## Design Philosophy (REVISED 2025-10-07)

### Platform Paradigm Respect

**Key Insight:** Don't try to unify what already works differently. Respect each platform's native paradigm and use combos to **fill gaps**, not replicate existing shortcuts.

**macOS Paradigm:**
- Application-centric (Cmd+Tab cycles apps)
- Modal window switching (Cmd+` with menu)
- Cmd+Space for launcher (Alfred/Spotlight) → **Keep using this!**
- Result: Use existing shortcuts that already have good muscle memory

**Niri Paradigm:**
- Spatial/column-centric (navigate by position)
- Direct window/column switching (no modal menus)
- Super+Space for launcher+focus (rofi) → **OS-level binding, not combo**
- Manual column organization convention
- Result: Use OS-level bindings for compositor-specific actions

### Combos Are for Gaps, Not Replacement

**Use combos for:**
- ✅ Universal editing operations (Copy/Paste/Cut/Undo/Save/Find)
- ✅ Things that lack good shortcuts on either platform
- ✅ Frequently-used actions that are awkward to reach

**Don't use combos for:**
- ❌ Replicating platform shortcuts that already work well
- ❌ OS-specific navigation that belongs in compositor config
- ❌ Things that are better handled at OS level

### Frequency-First Ergonomics

Following the **Colemak-DH principle**: align comfort with frequency.

- **Most frequent operations** → **Most comfortable positions**
- **Bottom row horizontals** → Editing operations (left hand free for mouse)
- **Adjacent verticals** → Document operations with mnemonics (e.g., F+S = Save)
- **Top row horizontals** → Utility operations
- **Home row combos** → **TBD - may not need them if OS handles navigation**

---

## OS-Level Shortcuts (Not Combos)

**These are handled at OS level or with existing HRM + keys - no firmware combos needed:**

### Application & Window Management

| Action                    | macOS                     | Niri                                                  | Notes                          |
| ------------------------- | ------------------------- | ----------------------------------------------------- | ------------------------------ |
| Application Launcher      | Cmd+Space (Alfred)        | Super+Space → `rofi -show window`                     | OS binding, same muscle memory |
| App Switching             | Cmd+Tab                   | Manual column organization + navigation               | Keep native behavior           |
| Window Cycling (Same App) | Cmd+\` (S+\`)             | Super+\` → `focus-window-down-or-top` (S+\`)          | HRM + existing key, no combo   |
| Reverse Window Cycle      | Cmd+Shift+\` (S+Shift+\`) | Super+Shift+\` → `focus-window-up-or-bottom` (S+Shift+\`) | HRM + existing key, no combo   |

**Niri Setup Notes:**
- See `NIMBINI-SETUP-NOTES.md` for rofi installation
- Bind Super+Space in Niri config to `rofi -show window`
- Bind Super+` to `focus-window-down-or-top` (cycles down through stack, wraps to top)
- Bind Super+Shift+` to `focus-window-up-or-bottom` (cycles up through stack, wraps to bottom)
- Both directions provide intuitive spatial control in Niri's column paradigm

**Result:** Same physical gestures (Cmd/Super + Space/Backtick) across platforms with platform-appropriate behavior.

---

## NAV Layer Analysis: Existing Edit Commands (2025-10-07)

### **DISCOVERY: Edit Commands Already Implemented**

**NAV Layer (Right Hand Top Row):**
```
Hold NAV (left thumb on SPACE) + right hand:
- J (pos 6):  LC(Y) → Redo
- L (pos 7):  LC(V) → Paste
- U (pos 8):  LC(C) → Copy
- Y (pos 9):  LC(X) → Cut
- ' (pos 10): td_ctrlz → Undo (tap dance)
```

**Also available on MOUSE layer** (same positions)

**Why this matters:**
- ✅ **Already cross-platform** - uses `LC()` which maps to Cmd on macOS, Ctrl on Linux via HRM
- ✅ **Left hand holds layer** - right hand free for execution
- ✅ **Proven system** - already implemented and presumably working
- ✅ **Ergonomic** - deliberate layer hold vs. precise timing required for combos

**Conclusion:** Edit commands (Copy/Paste/Cut/Undo/Redo) **do not need combos** - they're already handled elegantly by the NAV layer.

**Cross-Platform Implementation (2025-10-07):**
To support both macOS (Cmd) and Linux (Ctrl), two separate keymap files are now maintained:
- `piantor_pro_bt.keymap` - Linux version with `LC()` (Ctrl)
- `piantor_pro_bt_macos.keymap` - macOS version with `LG()` (Cmd)

See [CROSS-PLATFORM-KEYMAP-GUIDE.md](./CROSS-PLATFORM-KEYMAP-GUIDE.md) for complete details.

---

## Core Combo Allocation (REVISED 2025-10-07)

### Current Status: **OBSERVATION PHASE**

**Existing combos working well:**
- ✅ L+U → `:` (colon) / `;` (semicolon shifted)
- ✅ U+Y → `-` (minus)
- ✅ ,+. → `?` (question) / `!` (exclamation shifted)

**Previously considered (now recognized as redundant):**
- ~~Copy/Paste/Cut~~ → Already on NAV layer
- ~~Undo/Redo~~ → Already on NAV layer (td_ctrlz + LC(Y))
- ~~L+N (Application Launcher)~~ → Super/Cmd+Space (OS binding)
- ~~Q+W (Window Cycling)~~ → S+` (HRM + existing key)

---

### Category B: Navigation (Home Row Center) - STATUS: TBD

**Decision Pending:** May not need combos for navigation at all if OS-level shortcuts suffice.

**User Workflow Context:**
- No workspaces needed (single workspace model)
- No monitor switching needed (single monitor per machine)
- Navigation needs: Column left/right (Niri), Window up/down (both platforms handled by S+`)

**Options Under Consideration:**

#### Option 1: OS-Level Bindings Only (Niri)
```
Niri config bindings:
- Super+H → focus-column-left
- Super+L → focus-column-right
```
**Pros:** Simple, no firmware complexity
**Cons:** Different from macOS (but macOS uses Cmd+Tab which works fine)

#### Option 2: Use Combos for Niri Column Navigation
```
S+T combo → focus-column-left
N+E combo → focus-column-right
```
**Pros:** Symmetric positioning, home row comfort
**Cons:** Combos used for platform-specific action that could be OS-level

#### Option 3: Wait and See
- Implement core combos first (editing, document operations)
- Use Niri for 1-2 weeks with OS-level bindings
- Only add combos if genuine need emerges

**Recommendation:** Option 3 - implement essentials first, add navigation combos only if needed

**Previously Proposed Three-Tier System:**
- ~~Tier 1: S+T / N+E (Primary)~~
- ~~Tier 2: R+S / E+I (Secondary)~~
- ~~Tier 3: A+R / I+O (Tertiary)~~
- **Status:** Simplified workflow doesn't require three tiers

---

### Category C: Editing Operations - **NOT NEEDED**

**~~Bottom Row Horizontals~~ - Already handled by NAV layer**

| ~~Combo~~          | ~~Keys~~ | ~~Positions~~ | Current Solution | Status |
| -------------- | ----------------- | --------- | -------------------- | ---------- |
| ~~Copy~~           | ~~X + C~~             | ~~25, 26~~    | NAV+U (LC(C))         | ✅ Implemented |
| ~~Paste~~          | ~~C + D~~             | ~~26, 27~~    | NAV+L (LC(V))         | ✅ Implemented |
| ~~Cut~~            | ~~X + D~~             | ~~25, 27~~    | NAV+Y (LC(X))         | ✅ Implemented |

**Why combos are unnecessary:**
- NAV layer already provides cross-platform Copy/Paste/Cut
- Layer hold is more deliberate than precise combo timing
- Left thumb holds NAV, right hand executes - ergonomically sound
- Adding combos would create redundancy and potential conflicts

---

### Category D: Document Operations - **FUTURE CONSIDERATION**

**Vertical Adjacent combos for file operations - evaluate after observation period**

| Combo | Keys (Colemak-DH) | Positions | Type       | Shortcut | Current Status |
| ----- | ----------------- | --------- | ---------- | -------------------- | ---------- |
| Save  | F + S             | 3, 15     | Top → Home | Cmd/Ctrl + S         | Deferred - observe usage |
| Find  | P + T             | 4, 16     | Top → Home | Cmd/Ctrl + F         | Deferred - observe usage |

**Rationale for deferral:**
- **F+S mnemonic** compelling but unproven necessity
- Most editors (Helix) have mode-specific save workflows
- Find is application-specific (different in browser vs editor)
- **Decision:** Only implement if friction emerges during real usage

---

## Reserved Symbol Combos (Do Not Use)

These positions are already allocated to symbols in your base layer:

| Combo | Keys (Colemak-DH) | Positions           | Output |
| ----- | ----------------- | ------------------- | ------ |
| L + U | 7, 8              | `:` / `;` (shifted) |        |
| U + Y | 8, 9              | `-` (minus/hyphen)  |        |
| , + . | 32, 33            | `?` / `!` (shifted) |        |

**Status:** ✅ Fixed L+U to use `colon_semi` morph behavior for proper shift support (in piantor_pro_bt.keymap).

---

## Implementation Phases (REVISED 2025-10-07)

### Phase 1: **OBSERVATION ONLY - No New Combos Needed**

**Current system already covers essential operations:**

1. ✅ **Copy/Paste/Cut/Undo/Redo** - Already on NAV layer (cross-platform via LC())
2. ✅ **Symbol combos** - L+U (colon), U+Y (minus), ,+. (question) working well
3. ✅ **Application management** - OS-level shortcuts (Cmd/Super+Space, S+`)

**Phase 1 Action Items:**
- **Use current system** for 2-4 weeks
- **Observe friction points** during real workflow
- **Document pain points** if any emerge
- **Only proceed to Phase 2** if genuine gaps are identified

**Expected effort:** Zero implementation time, active observation
**Impact:** Validates existing system is sufficient

### Phase 2: OS-Level Setup (Nimbini - ~4 weeks from 2025-10-07)

**Configure OS shortcuts (not firmware combos):**

1. **Install anyrun** (preferred, Rust-based) or rofi (fallback) - see NIMBINI-SETUP-NOTES.md
2. **Bind Super+Space** to anyrun/rofi in Niri config
3. **Validate existing Niri bindings:**
   - Super+Shift (SS) for focus operations
   - Alt+Super+Shift (ASS) for move operations
   - See NIRI-CONFIG-SA-PREFIX-SYSTEM.md for complete grammar

**Expected effort:** 30 minutes setup
**Impact:** Complete application/window management on Linux

### Phase 3: Evaluate and Extend (After 2-4 Weeks Real Usage)

**After using Phase 1+2 in practice:**

1. **Review observation notes** from Phase 1
2. **Identify genuine friction** not covered by existing shortcuts
3. **Consider combo additions** only if clear patterns emerge:
   - Save/Find (F+S, P+T) if file operations feel awkward
   - Navigation combos if Niri SS/ASS system insufficient
4. **Prioritize by frequency × friction** - not theoretical optimization

**Philosophy:** Observation-driven design, not assumption-driven implementation

---

## Conditional Macro Implementation

### Cross-Platform Macro Pattern

```c
// Example: Copy macro
#ifdef CONFIG_MACOS_BUILD
    ZMK_MACRO(macro_copy,
        wait-ms = <0>;
        tap-ms = <5>;
        bindings = <&kp LGUI &kp C &kp LGUI>;
    )
#else
    ZMK_MACRO(macro_copy,
        wait-ms = <0>;
        tap-ms = <5>;
        bindings = <&kp LCTRL &kp C &kp LCTRL>;
    )
#endif

// Combo definition
combo_copy {
    timeout-ms = <50>;
    require-prior-idle-ms = <150>;
    key-positions = <25 26>;  // X + C
    bindings = <&macro_copy>;
    layers = <BASE>;
}
```

### Platform-Specific Application Launcher

```c
// L+N = Application Launcher
#ifdef CONFIG_MACOS_BUILD
    ZMK_MACRO(macro_app_launcher,
        wait-ms = <0>;
        tap-ms = <5>;
        bindings = <&kp LGUI &kp SPACE &kp LGUI>;  // Cmd+Space for Alfred
    )
#else
    ZMK_MACRO(macro_app_launcher,
        wait-ms = <0>;
        tap-ms = <5>;
        // Spawn fuzzel via niri msg or direct keybind
        bindings = <&kp LALT &kp LGUI &kp D>;  // Super+Alt+D for fuzzel
    )
#endif
```

### Within-App Window Cycling

```c
// Q+W = Cycle within app windows
#ifdef CONFIG_MACOS_BUILD
    ZMK_MACRO(macro_cycle_app_windows,
        wait-ms = <0>;
        tap-ms = <5>;
        bindings = <&kp LGUI &kp GRAVE &kp LGUI>;  // Cmd+`
    )
#else
    // Niri: focus-window-down (within column)
    // This would need niri msg integration or pre-bound key
    ZMK_MACRO(macro_cycle_app_windows,
        wait-ms = <0>;
        tap-ms = <5>;
        // Use whatever key you bind to focus-window-down in Niri config
        bindings = <&kp LCTRL &kp LGUI &kp DOWN>;  // Example binding
    )
#endif
```

### Contextual Navigation Macros

**Use generic naming for flexibility:**

```c
// Tier 1: Primary Navigation (S+T / N+E)
macro_nav_prev_primary  // macOS: Cmd+Tab / Niri: focus-column-left
macro_nav_next_primary  // macOS: Cmd+Shift+Tab / Niri: focus-column-right

// Tier 2: Secondary Navigation (R+S / E+I) - assign after testing
macro_nav_prev_secondary  // Workspace / Monitor / Context-dependent
macro_nav_next_secondary

// Tier 3: Tertiary Navigation (A+R / I+O) - assign after testing
macro_nav_prev_tertiary
macro_nav_next_tertiary
```

**Remap the macro contents** after workflow observation without changing combo positions.

---

## Visual Combo Map

### Top Row (Application Management)

**Colemak-DH Layout:**

```
Left Side:                 Right Side:
Q ─ [W]                    [L] ─ [N]              [Y] ─ [']
    │                        │                        │
  Within-App             App Launcher              Undo
   Cycle                 ⭐⭐⭐⭐⭐              ⭐⭐⭐⭐⭐
  ⭐⭐⭐⭐⭐
                         (Shift versions = reversed/redo)
```

### Home Row (Three-Tier Navigation)

**Colemak-DH Layout:**

```
Left Hand:                                Right Hand:
A ─ [R] ─ [S] ─ [T]                      [N] ─ [E] ─ [I] ─ [O]
    │     │     │                          │     │     │     │
Tertiary  │     │                          │     │  Tertiary │
  ⭐⭐⭐   │     │                          │   Secondary    │
     Secondary │                          │     ⭐⭐⭐⭐      │
      ⭐⭐⭐⭐   │                       Primary              │
           Primary                     ⭐⭐⭐⭐⭐              │
          ⭐⭐⭐⭐⭐                                         ⭐⭐⭐

Directional Logic: ← Left-to-right = Forward/Next →
```

### Bottom Row (Editing)

**Colemak-DH Layout:**

```
[X] ─ [C] ─ [D]
  │     │     │
  └─────┴─ Cut (skip-one) ⭐⭐⭐
  │     │
 Copy  Paste
⭐⭐⭐⭐⭐ ⭐⭐⭐⭐⭐
```

### Left Hand Verticals (Document Operations)

**Colemak-DH Layout:**

```
F ──┐
    ├─ Save (⌘S / ^S) ⭐⭐⭐⭐⭐
S ──┘

P ──┐
    ├─ Find (⌘F / ^F) ⭐⭐⭐⭐
T ──┘
```

---

## Platform-Specific Notes

### macOS Behavior

**Application Switching:**

- S+T / N+E → Cmd+Tab / Cmd+Shift+Tab (cycles through apps)
- Q+W → Cmd+` (cycles windows within current app)

**Application Launcher:**

- L+N → Cmd+Space (triggers Alfred or Spotlight)

**Standard Shortcuts:**

- All Cmd-based shortcuts (Copy, Paste, Undo, Save, Find)

### Niri/Linux Behavior

**Spatial Navigation:**

- S+T / N+E → `focus-column-left` / `focus-column-right`
- Q+W → `focus-window-down` (within column - requires convention: same app = same column)

**Application Launcher:**

- L+N → Super+Alt+D (launches fuzzel)

**Window Management:**

- No "application" concept - navigate spatially
- User convention: Keep instances of same app in same column
- Tier 2/3 navigation maps to workspaces, monitors, or other spatial units

**Integration Requirements:**

- Bind Niri actions to match combo macros
- Configure fuzzel for application launching
- Establish workflow conventions (same-app-same-column)

---

## Available Expansion Options

**Reserved for future needs (not currently allocated):**

### Additional Vertical Adjacent Combos

**Top → Home:**

- Q+A, W+R, B+G (3 available)

**Home → Bottom:**

- A+Z (safety combo), R+X, S+C, T+D, G+V (4 available)

### Skip-Two Horizontals

**Top row:** W+P, F+B, J+U, L+Y, etc. **Home row:** A+S, R+T, M+E, N+I, etc. **Bottom row:** Z+C, X+V, etc.

### Top Outer Pinkies (Stretch Positions)

- Q (position 1), ' (position 11) - available but require reach
- Lower priority due to ergonomics

### Layer-Switch on Single Alphas

Potential for entire new layers accessible via hold-tap on underused base keys.

**Philosophy:** Only add complexity when prime real estate is exhausted and genuine need exists.

---

## Summary (REVISED 2025-10-07)

**Status:** Phase 1 implementation complete - tab/history combos added
**Total Active Combos:** 7 combos (3 symbols + 4 navigation)
**Edit Commands:** Already on NAV layer (no combos needed)
**Tab/History Navigation:** New home row combos (S+T, N+E, R+S, E+I)
**Prime Real Estate Preserved:** Outer positions (A+R, I+O) still available
**Implementation Time:** Awaiting build and testing
**Coverage:** Symbol entry + cross-platform edit commands + tab/history navigation + OS-level window management

### Key Design Principles

1. **Platform Paradigm Respect:** Don't replicate what already works - macOS keeps Cmd+Tab/Cmd+`, Niri uses Super+Space/SS/ASS with platform-appropriate behavior

2. **OS-Level First:** Application/window management handled at OS level (anyrun/rofi, Niri compositor bindings) rather than firmware combos

3. **Layer System Recognition:** NAV layer already provides cross-platform edit commands elegantly - no need to duplicate with combos

4. **Observation-Driven Design:** Only add combos when real usage reveals genuine friction, not based on theoretical optimization

5. **Same HRM Layout:** Both platforms use identical A(Ctrl) R(Alt) S(Gui) T(Shift) - no swapping, preserves muscle memory for apps with consistent shortcuts (terminals, Helix)

6. **SS/ASS Grammar:** Niri uses Super+Shift (focus) and Alt+Super+Shift (move) for window management - memorable, conflict-free, ergonomic

### Architecture Decisions

**OS-Level (Not Combos):**
- Application launcher: Super/Cmd+Space (same gesture, platform-appropriate tool - anyrun/Alfred)
- Window cycling: S+` (HRM + existing key, no combo needed)
- Niri window management: SS (focus) and ASS (move) grammar via compositor bindings

**NAV Layer (Not Combos):**
- ✅ Copy/Paste/Cut: NAV+U/L/Y (already implemented, cross-platform via LC())
- ✅ Undo/Redo: NAV+'/J (td_ctrlz and LC(Y), already implemented)

**Firmware Symbol Combos (Current):**
- ✅ L+U → colon/semicolon
- ✅ U+Y → minus
- ✅ ,+. → question/exclamation

**Firmware Navigation Combos (NEW 2025-10-07):**
- ✅ S+T → Previous tab (Cmd+Shift+[ on macOS, Ctrl+PgUp on Linux)
- ✅ N+E → Next tab (Cmd+Shift+] on macOS, Ctrl+PgDn on Linux)
- ✅ R+S → Back in history (Cmd+[ on macOS, Alt+Left on Linux)
- ✅ E+I → Forward in history (Cmd+] on macOS, Alt+Right on Linux)

See [TAB-HISTORY-COMBOS-IMPLEMENTATION.md](./TAB-HISTORY-COMBOS-IMPLEMENTATION.md) for complete details.

**Future Expansion (If Needed):**
- Outer home row (A+R, I+O) reserved for future needs
- Save/Find (F+S, P+T) deferred until friction emerges
- Add only based on real usage observation, not theoretical optimization

---

_Phase 1: Observation mode - no implementation needed. Phase 2: Nimbini OS-level setup awaits access (~4 weeks)._
