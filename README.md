# 💻 ASUS K56CB BIOS Recovery using CH341A Programmer

This project documents the full recovery of a bricked ASUS K56CB laptop using a CH341A programmer and SOP8 clip.  
After a failed BIOS update, the laptop was completely unresponsive — black screen, no keyboard backlight, no POST.  
With no internal recovery options available, I manually flashed a clean BIOS dump directly to the chip.

---

## 🧰 Tools & Hardware Used

- CH341A USB Programmer (Black edition)
- SOP8 Clip with cable
- CH341A Programmer software (v1.34 or AsProgrammer)
- UEFITool (for BIOS analysis)
- Verified 8MB BIOS `.bin` dump (W25Q64FV chip)
- Flux + tweezers (optional, for better pin contact)

---

## 🛠️ Step-by-Step Recovery Process

### 1. Identify the BIOS chip  
Located the 8-pin SPI BIOS chip on the motherboard (Winbond W25Q64FV — 8MBytes).

### 2. Connect the clip to the chip  
- Align pin 1 of the SOP8 clip (red wire) with pin 1 of the chip (notch/dot on top left).
- Connect the clip to the CH341A programmer via the included adapter.

### 3. Dump and back up the original BIOS  
- Open CH341A Programmer → Read → Save as `bios_backup.bin`
- Always keep this file in case you need to restore.

### 4. Extract or find a proper BIOS `.bin` file  
- Avoid ASUS `.209` update files — they are not full dumps.
- Use UEFITool to verify the structure:
  - Must include Descriptor Region + ME Region + BIOS Region.
- File size must be **exactly 8,388,608 bytes (8MB)**.

### 5. Flash the new BIOS  
- Erase → Open the new `.bin` file → Program → Verify
- All operations should return “successful” messages.

### 6. Reassemble and test  
- Disconnect SOP8 clip and USB programmer.
- Optional: Clear CMOS (remove battery for 30s).
- Power on: device should boot into BIOS automatically.

---

## ✅ Result

BIOS successfully flashed.  
Laptop now boots correctly and is fully functional again.  
This saved the machine from being e-waste — and it cost less than €10 in hardware.

---

## 📷 Images

See the `/images` folder for detailed connection photos and software screenshots.

---

## 📁 Files Included

- `bios_backup.bin` → Original dump before flashing
- `K56CB_fixed.bin` → Clean BIOS dump used for recovery
- Tool links & references in `/tools`

---

## 📎 Useful Links

- [UEFITool (GitHub)](https://github.com/LongSoft/UEFITool)
- [CH341A Programmer Tools](https://github.com/nofeletru/UsbAsp-flash/wiki/CH341A)
- [Win-Raid BIOS Dump Forum](https://winraid.level1techs.com/)
- [BIOS-Mods.com](https://www.bios-mods.com/)

---

## 🧠 Lessons Learned

- Always back up your original BIOS before doing anything.
- Don’t flash `.209` files directly — they’re incomplete for external programmers.
- A €10 programmer and some patience can save a laptop.
- There's very little documentation — so I made my own.

---

## 📇 Author

Repaired and documented by [@kiz4ru](https://github.com/kiz4ru)  
If this helped you, consider ⭐️ starring the repo!

