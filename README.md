## 1. What your DFU output proves (this is excellent news)

This block is gold:

```shell
idVendor=0483, idProduct=df11
Product: STM32 BOOTLOADER
Manufacturer: STMicroelectronics
```

And this:

```shell
@Internal Flash  /0x08000000/0128*0002Kg
```

Interpretation:

* MCU is **STM32**
* Using **ST’s ROM DFU bootloader** (not a custom one)
* Internal flash starts at `0x08000000`
* Flash layout: `128 × 2 KB = 256 KB` total flash

This immediately rules out a whole class of risks.

### What this means concretely

* Bootloader is **in ROM**, not flash → cannot be overwritten
* DFU recovery is **always available**
* You can always reflash a `.bin`
* Even a bad firmware flash is recoverable

---

**Rule:**
Never write to:
* `@OTP Memory`
* `@Option Bytes`

---
 
Discipline:
* incremental flashes
* minimal firmware first
* always keeping the stock `.bin`

## 2. Support email: suggested message (copy, adapt, send)
[ONGOING]

---

## 3. Project documentation: suggested structure (start this now)
### Project: Keychron K12 Pro – Experimental QMK Port

**1. Goals**
* Enable full QMK firmware on K12 Pro
* Preserve Bluetooth functionality
* Add layer-aware RGB behavior
* Maintain full DFU recoverability

**2. Hardware**
* Keyboard: Keychron K12 Pro ANSI RGB
* MCU: STM32 (exact model TBD)
* Bootloader: STM32 ROM DFU
* Flash: 256 KB internal

**3. Safety Guarantees**
* Stock firmware archived
* DFU recovery verified
* OTP and Option Bytes never modified

**4. Toolchain**
* dfu-util
* QMK (forked / experimental)
* Linux (Debian)

**5. Phase Plan**
* Phase 0: Stock firmware flash verification ✅
* Phase 0: Keychron Support Contact
* Phase 1: MCU identification
* Phase 2: Minimal QMK “hello world”
* Phase 3: Matrix bring-up
* Phase 4: Keymap parity
* Phase 5: RGB bring-up
* Phase 6: Bluetooth validation

**6. Validation Checklist** 
* USB enumeration
* Key scanning
* Layer switching
* RGB correctness
* Bluetooth pairing persistence
* DFU recovery intact

---

## 4. Final calibration
**Current collection:**
* a ROM bootloader
* a verified DFU path
* a restore image
* a documented plan

### ToDo
- [ ] **identify the exact STM32 model** (either via support or USB descriptors), then choose a *closest existing QMK STM32 keyboard* as a porting base.

## Objectives
The end goal is to tweak the RGB and Layer functions for visual cues: Setting WASD as arrow keys in fn1 Layer and display them in an orange color rather than default solid cyan, setting S and P pivotal keys for fourth finger in a fuschia color for quick hand positioning in the dark and a few minor purple visual cues for 3, 8, f, j. The design may be lacking a ` ~ key more than \ | and I will use my project to correct that too. For my personal usage I will make an alternate that maps ctrl as capslock and correct Linux/S25 functions.
