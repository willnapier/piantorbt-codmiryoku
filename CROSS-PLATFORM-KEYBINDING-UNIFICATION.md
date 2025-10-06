# Cross-Platform Keybinding Unification Project

**Date**: 2025-10-06
**Purpose**: Unified keyboard experience across macOS and Linux with platform-optimized firmware
**Hardware**: Two Piantor Pro BT keyboards (one dedicated to each OS)

---

## 🎯 **PROJECT GOAL**

**Same physical gestures, platform-appropriate output**
- Same finger movements on both keyboards
- Each keyboard sends OS-appropriate key sequences
- Single source code, conditional compilation for two firmware builds

---

## 📊 **CURRENT STATE INVENTORY**

### Text Navigation

| Action | macOS Current | Linux Current | Physical Gesture Desired |
|--------|---------------|---------------|--------------------------|
| Word Back | Alt+Left | Ctrl+Left | *TBD - combo or HRM+arrow* |
| Word Forward | Alt+Right | Ctrl+Right | *TBD - combo or HRM+arrow* |
| Line Start | Cmd+Left | Home (or Ctrl+A in terminal) | *TBD* |
| Line End | Cmd+Right | End (or Ctrl+E in terminal) | *TBD* |
| Document Start | *Need to verify* | *Need to verify* | *TBD* |
| Document End | *Need to verify* | *Need to verify* | *TBD* |
| Paragraph Forward | *Not currently configured* | *Not currently configured* | *Desired feature* |
| Paragraph Backward | *Not currently configured* | *Not currently configured* | *Desired feature* |

### Text Selection

| Action | macOS Current | Linux Current | Notes |
|--------|---------------|---------------|-------|
| Select Word | Shift+Alt+arrows | Shift+Ctrl+arrows | **CRITICAL**: Space unavailable in NAV layer! |
| Select Line | Shift+Cmd+arrows | *Need to verify* | Same NAV layer conflict |
| Extend Selection | Shift+movement | *Need to verify* | Requires Shift accessible while navigating |

**🚨 NAV Layer Conflict Identified:**
- Left middle thumb: Space (tap) / NAV (hold)
- Text selection requires Shift + movement keys
- But NAV layer has movement keys
- **Problem**: Can't access Space while in NAV layer for selection
- **Solution needed**: Shift must be available while in NAV layer

### Browser/Application Tab Navigation

| Action | macOS Current | Linux/Niri Current | Preference |
|--------|---------------|-------------------|------------|
| Next Tab | Cmd+Shift+] (preferred over Cmd+}) | *Need to verify* | Use Cmd+Shift+] gesture |
| Previous Tab | Cmd+Shift+[ | *Need to verify* | Use Cmd+Shift+[ gesture |
| Close Tab | Cmd+W | **Ctrl+Q (in Niri)** | **Want Cmd+W gesture!** |
| Reopen Closed Tab | Cmd+Shift+T | *Need to verify* | Use frequently, want same |
| New Tab | Cmd+T | Ctrl+T | Standard, probably fine |
| New Window | Cmd+N | Ctrl+N | Standard, probably fine |

**🚨 Close Tab Conflict:**
- Niri uses Ctrl+Q (unfamiliar, disliked)
- Prefer Cmd+W gesture
- **Opportunity for HRM swap approach**

### Common Shortcuts

| Action | macOS | Linux | Notes |
|--------|-------|-------|-------|
| Copy | Cmd+C | Ctrl+C | Standard |
| Cut | Cmd+X | Ctrl+X | Standard |
| Paste | Cmd+V | Ctrl+V | Standard |
| Undo | Cmd+Z | Ctrl+Z | Standard |
| Redo | Cmd+Shift+Z | Ctrl+Shift+Z | Standard |
| Save | Cmd+S | Ctrl+S | Standard |
| Find | Cmd+F | Ctrl+F | Standard |

---

## 💡 **THE BRILLIANT INSIGHT: HRM SWAP APPROACH**

**Instead of conditional macros sending different sequences**, swap the Home Row Mod assignments:

### Current HRM Layout (Same on Both)
```
Left:  A(Ctrl) R(Alt) S(Gui) T(Shift)
Right: N(Shift) E(Gui) I(Alt) O(Ctrl)
```

### Proposed: HRM Swap for Platform Optimization

**macOS Keyboard:**
```
Left:  A(Ctrl) R(Alt) S(Gui) T(Shift)
Right: N(Shift) E(Gui) I(Alt) O(Ctrl)
```
*(Keep as-is for macOS - Gui=Cmd)*

**Linux Keyboard:**
```
Left:  A(Gui) R(Alt) S(Ctrl) T(Shift)
Right: N(Shift) E(Ctrl) I(Alt) O(Gui)
```
*(Swap Gui↔Ctrl positions)*

### Result: Fingers Don't Know the Difference!

**Physical gesture: S+W (same on both keyboards)**
- macOS keyboard: S=Gui → sends Cmd+W
- Linux keyboard: S=Ctrl → sends Ctrl+W
- **Your fingers press S+W either way!**

**Advantages:**
- ✅ No complex conditional macros needed
- ✅ All standard shortcuts work automatically (Cmd/Ctrl + C/V/X/Z/S/F/etc.)
- ✅ Simpler firmware (just swap HRM definitions)
- ✅ Muscle memory identical across platforms
- ✅ No special handling for individual shortcuts

**Disadvantages:**
- ⚠️ System-level Gui key (window management) swaps positions
- ⚠️ Need to verify all layer interactions work correctly

---

## 🔧 **IMPLEMENTATION APPROACHES**

### Approach 1: HRM Swap (Simpler)
- Change home row mod assignments conditionally
- All shortcuts "just work" due to OS conventions
- Minimal code changes

### Approach 2: Conditional Macros (More Complex)
- Keep HRM layout identical
- Create macros for each divergent binding
- Send different sequences per OS

### Approach 3: Hybrid
- Use HRM swap for standard shortcuts (Cmd/Ctrl+letter)
- Use conditional macros for special cases (arrows, etc.)

---

## ✅ **NEXT STEPS**

1. **Complete Linux keybinding inventory** (need SSH to Nimbini)
   - Line start/end defaults
   - Document start/end
   - Tab navigation in Firefox/applications
   - Selection behaviors

2. **Resolve NAV layer Shift conflict**
   - How to make Shift accessible while in NAV layer?
   - Options: Sticky shift? Layer-tap on different key? Combo?

3. **Decide on implementation approach**
   - Pure HRM swap?
   - Conditional macros?
   - Hybrid?

4. **Test HRM swap implications**
   - Does swapping Gui↔Ctrl cause issues with system shortcuts?
   - Layer interactions (SYM, NUM, etc.)?

5. **Create conditional compilation infrastructure**
   - Update build.yaml for dual builds
   - Add #ifdef macros to keymap
   - Test GitHub Actions builds

---

## 📝 **QUESTIONS TO RESOLVE**

- [ ] Text selection: Did you mean **Shift** (not Space) + arrows?
- [ ] Can we access SSH to Linux machine to verify current keybindings?
- [ ] Should we use HRM swap or conditional macros approach?
- [ ] How to handle NAV layer + Shift for text selection?
- [ ] What system shortcuts use Gui/Super key on Linux that might conflict with HRM swap?

---

*This document will be updated as we gather more information and make implementation decisions.*
