# Piantor Pro BT Layer Optimization Tracking

**Focus:** Identifying and reallocating redundant layer bindings to maximize available prime real estate

**Last Updated:** 2025-10-08
**Status:** Active Analysis - Redundancy Identification Phase

---

## Core Insight (2025-10-08)

**Discovery:** The SYM and NUM layers have significant overlap due to traditional keyboard Shift+number associations. This creates **double coverage** for the same symbols, wasting prime keyboard real estate.

### The Redundancy Pattern

**NUM layer provides symbols TWO ways:**
1. **Direct number access** (1-9, 0)
2. **Shift+number = traditional symbols** (!@£$%^&*())

**SYM layer ALSO provides the same symbols:**
- Explicitly bound to specific positions
- **Result:** Same symbol accessible via two completely different methods

### Strategic Opportunity

**By choosing the preferred access method for each symbol, we can free up slots on the SYM layer for new functions.**

---

## Current Layer State Analysis

### SYM Layer (Left Side) - Position 1-5

```
Position:  1        2           3           4           5           6
Row 1:     {        &           *           (           }           (right side)
           (LBRC)   (AMPS)      (ASTRK)     (LPAR)      (RBRC)

Row 2:     ;        $           %           ^           +
           (SEMI)   (DLLR)      (PRCNT)     (CARET)     (PLUS)

Row 3:     ~        !           @           £           |
           (TILDE)  (EXCL)      (AT)        (LS(N3))    (PIPE)
```

### NUM Layer (Left Side) - Position 1-5

```
Position:  1        2           3           4           5           6
Row 1:     [        7           8           9           ]           (right side)
           (LBKT)   (N7)        (N8)        (N9)        (RBKT)

Row 2:     `        4           5           6           =
           (GRAVE)  (N4)        (N5)        (N6)        (EQUAL)

Row 3:     ~        1           2           3           |
           (TILDE)  (N1)        (N2)        (N3)        (PIPE)

Thumb:                          0
                                (N0)
```

### Traditional Keyboard Shift+Number Mappings

**When Shift is held on NUM layer, you get:**
- Shift+1 = `!`
- Shift+2 = `@`
- Shift+3 = `£` (UK layout)
- Shift+4 = `$`
- Shift+5 = `%`
- Shift+6 = `^`
- Shift+7 = `&`
- Shift+8 = `*`
- Shift+9 = `(`
- Shift+0 = `)`

---

## Redundancy Analysis

### Complete Overlap Table

| Symbol | SYM Layer Location | NUM Layer Access (Shift+) | Already Combo? | User Preference |
|--------|-------------------|---------------------------|----------------|-----------------|
| `!` | Row 3, Pos 2 | Shift+1 | ❌ No | **KEEP SYM** (high frequency) |
| `@` | Row 3, Pos 3 | Shift+2 | ❌ No | **→ NUM** (Shift+2 muscle memory) |
| `£` | Row 3, Pos 4 | Shift+3 | ❌ No | **→ NUM** (Shift+3, rarely used) |
| `$` | Row 2, Pos 2 | Shift+4 | ❌ No | **KEEP SYM** (variables, strings) |
| `%` | Row 2, Pos 3 | Shift+5 | ❌ No | **→ NUM** (Shift+5 easy) |
| `^` | Row 2, Pos 4 | Shift+6 | ❌ No | **→ NUM** (Shift+6, moderate use) |
| `&` | Row 1, Pos 2 | Shift+7 | ❌ No | **KEEP SYM** (references, AND) |
| `*` | Row 1, Pos 3 | Shift+8 | ✅ NUM layer has STAR at pos 6 | **KEEP SYM** (pointers, multiply, wildcards) |
| `(` | Row 1, Pos 4 | Shift+9 | ✅ Smart Shift on base | **→ SMART SHIFT** (already covered!) |
| `)` | N/A on SYM | Shift+0 | ✅ Smart Shift on base | **→ SMART SHIFT** (already covered!) |

### Combo Coverage Check

**Symbols with combo access (even better than layer access!):**

| Symbol | Combo Keys | Positions | Notes |
|--------|-----------|-----------|-------|
| `[` `{` | W+F | 2, 3 | Shift variant: `{` |
| `]` `}` | F+P | 3, 4 | Shift variant: `}` |

**User stated:** "Since the combo access to [] and {} is so convenient, I'm pretty sure I'll never want to use any other bindings for those"

**Impact:** This means:
- SYM Row 1, Pos 1: `{` (LBRC) → **REDUNDANT** (have W+F combo)
- SYM Row 1, Pos 5: `}` (RBRC) → **REDUNDANT** (have F+P combo)
- NUM Row 1, Pos 1: `[` (LBKT) → **REDUNDANT** (have W+F combo)
- NUM Row 1, Pos 5: `]` (RBKT) → **REDUNDANT** (have F+P combo)

---

## Prime Real Estate Identification

### **AVAILABLE SLOTS (High-Value Positions)**

Based on user preferences and redundancy analysis:

#### SYM Layer - Left Hand Freed Slots

| Position | Current Binding | Redundancy Reason | Priority |
|----------|----------------|-------------------|----------|
| **Row 1, Pos 1** | `{` (LBRC) | W+F combo provides this | ⭐⭐⭐⭐⭐ (top-left corner) |
| **Row 1, Pos 4** | `(` (LPAR) | Smart Shift provides this | ⭐⭐⭐⭐⭐ (ring finger home row access) |
| **Row 1, Pos 5** | `}` (RBRC) | F+P combo provides this | ⭐⭐⭐⭐ (pinky stretch but usable) |
| **Row 3, Pos 3** | `@` (AT) | Shift+2 on NUM layer | ⭐⭐⭐ (bottom row, convenient) |
| **Row 3, Pos 4** | `£` (LS(N3)) | Shift+3 on NUM layer | ⭐⭐⭐ (bottom row, convenient) |
| **Row 2, Pos 3** | `%` (PRCNT) | Shift+5 on NUM layer | ⭐⭐⭐⭐ (middle row, home position) |
| **Row 2, Pos 4** | `^` (CARET) | Shift+6 on NUM layer | ⭐⭐⭐⭐ (middle row, home position) |

#### NUM Layer - Left Hand Freed Slots

| Position | Current Binding | Redundancy Reason | Priority |
|----------|----------------|-------------------|----------|
| **Row 1, Pos 1** | `[` (LBKT) | W+F combo provides this | ⭐⭐⭐⭐⭐ (top-left corner) |
| **Row 1, Pos 5** | `]` (RBKT) | F+P combo provides this | ⭐⭐⭐⭐ (pinky stretch but usable) |

**Total Available Prime Slots: 9 positions** (7 on SYM, 2 on NUM)

---

## Function Allocation Wishlist

### High-Priority Candidates for Prime Real Estate

**Category: Programming/Development**

| Function | Current Access | Frequency | Candidate Position |
|----------|---------------|-----------|-------------------|
| `<` `>` | Not on layers? | High (comparisons, HTML, generics) | SYM Row 2, Pos 3-4? |
| `=` | NUM Row 2, Pos 5 | High (assignment) | Keep, maybe duplicate? |
| Underscore `_` | NAV layer (pos 10, UNDER) | High (identifiers) | Consider SYM copy |
| Backtick `` ` `` | NUM Row 2, Pos 1 (GRAVE) | Moderate (markdown, shell) | Keep |

**Category: Navigation Shortcuts**

| Function | Current Access | Frequency | Candidate Position |
|----------|---------------|-----------|-------------------|
| `Tab` | BASE thumb (MOUSE layer) | High | Consider SYM duplicate? |
| `Esc` | BASE thumb (MEDIA/FUN layer) | High | Consider SYM duplicate? |

**Category: Helix Editor Shortcuts**

| Function | Shortcut | Frequency | Notes |
|----------|----------|-----------|-------|
| Select Mode | `v` | High | Already on base layer |
| Delete Line | `Alt+d` | Moderate | HRM already provides |
| Join Lines | `Alt+j` | Moderate | HRM already provides |

**Category: Application-Specific**

| Function | Context | Frequency | Notes |
|----------|---------|-----------|-------|
| Terminal: Ctrl+C | Kill process | High | HRM already provides |
| Browser: Ctrl+T | New tab | High | HRM already provides |
| Browser: Ctrl+W | Close tab | High | HRM already provides |

### Lower-Priority Candidates

**Category: Macros/Composed Actions**

| Function | Description | Complexity |
|----------|-------------|------------|
| `->` | Arrow operator (Rust, C++) | Could be macro |
| `=>` | Fat arrow (JS, Rust) | Could be macro |
| `!=` | Not equals | Could be macro |
| `==` | Equals comparison | Could be macro |
| `<=` `>=` | Comparison operators | Could be macro |

---

## Decision Framework

### Questions to Answer for Each Candidate

1. **Frequency × Friction Score**
   - How often is this used?
   - How awkward is current access?

2. **Alternative Access Quality**
   - Can this be done easily another way?
   - Is there a good combo position available?

3. **Cognitive Load**
   - Does this create a memorable pattern?
   - Does it conflict with existing muscle memory?

4. **Future-Proofing**
   - Is this specific to current workflow?
   - Will this still be useful in 6 months?

### Scoring System

**Frequency:**
- ⭐⭐⭐⭐⭐ Multiple times per hour
- ⭐⭐⭐⭐ Multiple times per day
- ⭐⭐⭐ Daily use
- ⭐⭐ Weekly use
- ⭐ Monthly or less

**Friction:**
- ⭐⭐⭐⭐⭐ Requires awkward stretch or multiple modifiers
- ⭐⭐⭐⭐ Requires layer switch + stretch
- ⭐⭐⭐ Requires layer switch
- ⭐⭐ Requires modifier
- ⭐ Single keypress

**Priority = Frequency × Friction**

---

## Implementation Strategy

### Phase 1: Conservative Cleanup (Immediate)

**Remove confirmed redundancies with strong alternatives:**

1. ✅ `(` on SYM Row 1, Pos 4 → Remove (Smart Shift covers this)
2. ✅ `)` if present → Remove (Smart Shift covers this)
3. ✅ `{` on SYM Row 1, Pos 1 → Remove (W+F combo covers this)
4. ✅ `}` on SYM Row 1, Pos 5 → Remove (F+P combo covers this)

**Result:** 4 slots freed, zero functionality lost

### Phase 2: User Preference Migration (After testing)

**Migrate symbols to preferred access method:**

1. `@` → Remove from SYM, rely on Shift+2 on NUM
2. `£` → Remove from SYM, rely on Shift+3 on NUM
3. `%` → Remove from SYM, rely on Shift+5 on NUM
4. `^` → Remove from SYM, rely on Shift+6 on NUM

**Result:** Additional 4 slots freed (8 total)

**Testing period:** 1-2 weeks to confirm NUM+Shift is comfortable

### Phase 3: Allocation Planning (After observation)

**With 8+ free slots, evaluate:**

1. Most-requested missing symbols
2. Macro opportunities for composed operators
3. Editor-specific shortcuts that are awkward
4. Application-specific power-user shortcuts

**Philosophy:** Observation-driven allocation, not theoretical optimization

---

## Proposed Layer Changes

### Option A: Conservative (Remove only confirmed redundancies)

**SYM Layer Changes:**
```diff
Row 1, Pos 1:  { (LBRC)  → &none  (W+F combo covers this)
Row 1, Pos 4:  ( (LPAR)  → &none  (Smart Shift covers this)
Row 1, Pos 5:  } (RBRC)  → &none  (F+P combo covers this)
```

**NUM Layer Changes:**
```diff
Row 1, Pos 1:  [ (LBKT)  → &none  (W+F combo covers this)
Row 1, Pos 5:  ] (RBKT)  → &none  (F+P combo covers this)
```

**Freed slots:** 5 positions
**Risk:** Zero (alternatives proven)

### Option B: Aggressive (Migrate to NUM layer preferences)

**SYM Layer Changes (in addition to Option A):**
```diff
Row 2, Pos 3:  % (PRCNT)  → &none  (Shift+5 on NUM)
Row 2, Pos 4:  ^ (CARET)  → &none  (Shift+6 on NUM)
Row 3, Pos 3:  @ (AT)     → &none  (Shift+2 on NUM)
Row 3, Pos 4:  £ (LS(N3)) → &none  (Shift+3 on NUM)
```

**Freed slots:** 9 positions (5 from Option A + 4 additional)
**Risk:** Medium (need to verify NUM+Shift comfort)

---

## Next Steps

### Immediate Actions

1. ✅ Document current state (this file)
2. ⏳ **Get user confirmation** on which slots to free
3. ⏳ Identify top 3-5 functions for prime real estate allocation
4. ⏳ Implement Option A (conservative) changes
5. ⏳ Test for 1 week, observe friction
6. ⏳ Proceed to Option B if no issues

### Questions for User

1. **Which symbols do you use most frequently in programming?**
   - Missing from current layout?
   - Awkward to access currently?

2. **Are there Helix shortcuts you wish were easier to reach?**
   - Mode switches?
   - Selection operations?
   - File operations?

3. **Any application-specific shortcuts you use constantly?**
   - Browser?
   - Terminal?
   - Specific languages (Rust, Python, etc.)?

4. **Preference confirmation:**
   - Confirm: Keep `!` `$` `&` `*` on SYM (high frequency)?
   - Confirm: Move `@` `£` `%` `^` to NUM+Shift (moderate frequency)?
   - Confirm: Smart Shift for `(` `)` is good enough (no layer binding needed)?

---

## Design Principles

### The Prime Real Estate Rule

**Not all positions are equal. Guard the most accessible slots carefully.**

**Top Priority Positions:**
- Row 2 (home row) positions 2-4: Index/middle/ring finger
- Row 1 positions 2-3: Strong fingers, minimal stretch
- Row 3 positions 2-3: Comfortable thumb zone access

**Use these only for:**
- Highest-frequency symbols (multiple times per hour)
- Critical editor operations (save work, undo mistakes)
- Functions with no good alternative access

**Lower Priority Positions:**
- Pinkies (positions 1, 5): Weaker fingers, more stretch
- Bottom row pinkies (positions 25, 34): Awkward reach
- Use these for moderate-frequency but still useful functions

### The Redundancy Elimination Principle

**If a symbol/function is accessible three ways, eliminate the worst two.**

**Example: Parentheses**
1. Smart Shift (thumb + shift) → Fast, no hand movement
2. SYM layer position → Requires layer hold + reach
3. NUM+Shift → Requires layer + modifier

**Decision:** Keep Smart Shift, remove SYM layer binding, NUM+Shift is free fallback

### The Observation-Before-Allocation Principle

**Don't fill slots just because they're empty.**

**Better to have:**
- Empty slots available for future needs
- Time to observe real usage patterns
- Flexibility to adapt to workflow changes

**Than to have:**
- Premature optimization based on guesses
- Cognitive load from too many obscure bindings
- Need to relearn when real needs emerge

---

## Historical Context

### Previous Optimization Efforts

**Symbol Combos (2025-10-07):**
- Added 8 symbol combos for high-frequency programming symbols
- W+F / F+P for brackets - now proven so convenient they make layer bindings redundant
- See: `SYMBOL-COMBOS-IMPLEMENTATION.md`

**Tab/History Navigation (2025-10-07):**
- Added home row combos for browser/editor navigation
- S+T / N+E for tab switching
- R+S / E+I for history navigation
- See: `TAB-HISTORY-COMBOS-IMPLEMENTATION.md`

**NAV Layer Edit Commands:**
- Copy/Paste/Cut/Undo/Redo already on NAV layer
- Cross-platform via LC() (Ctrl) / LG() (Cmd)
- No combos needed - layer system works well
- See: `COMBO-ALLOCATION-PROPOSAL.md`

### Lessons Learned

1. **Combos work great for high-frequency symbols** - less cognitive load than remembering layer positions
2. **Layer system works great for edit commands** - deliberate hold more reliable than combo timing
3. **Redundancy creates opportunities** - when you find double/triple coverage, you found free real estate

---

_This file tracks the ongoing optimization of layer bindings to maximize the utility of available keyboard positions. Updated based on user feedback and real-world usage observations._
