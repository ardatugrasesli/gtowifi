# 🛠️ Samsung Tab A 8.0 (SM-T290) Boot Image Fixer

This repository provides tools to fix the infamous **"SECURE CHECK FAIL"** error on the Samsung Galaxy Tab A 8.0 (2019). 

## 📝 Background
The T290's bootloader has a specific security requirement. It refuses to load any `boot` or `recovery` images that are missing:
1.  The `SignerVer02` magic string in the header.
2.  An **AVB (Android Verified Boot) Footer** at the end of the partition containing the exact image size.

If these are missing, you will see the red error message on your splash screen and the device will fail to boot. 🚫

---

## 🚀 How to Fix?

You have two ways to resolve this issue depending on your current setup.

### Option A: Flashable ZIP (via TWRP) 📲
If you already have TWRP installed and want to fix the image currently residing on your device:

1.  Download the [FixBootImage.zip](https://github.com/ardatugrasesli/gtowifi/releases/download/Release/FixBootImage.zip).
2.  Transfer it to your SD Card or Internal Storage.
3.  Boot into **TWRP Recovery**.
4.  Select **Install**, choose the zip, and swipe to flash.
5.  **Reboot** and enjoy! ✨

### Option B: Python Script (PC Method) 💻
Use this method to "patch" an image file on your computer before flashing it via Odin or Heimdall.

**Prerequisites:** Python 3.x installed.

1.  Place the `fix_bootable_image.py` script in the same folder as your `.img` file.
2.  Open your terminal/command prompt and run:
    ```bash
    python fix_bootable_image.py original_boot.img fixed_boot.img
    ```
3.  Flash the resulting `fixed_boot.img` to your device. ✅

---

## 🔍 Technical Details
The script performs the following binary modifications:
* **Header Injection:** It injects the `SignerVer02` identifier into the boot header.
* **Footer Calculation:** It calculates the precise block size of the image and appends an AVB Footer, satisfying the bootloader's integrity check.

---

## ⚠️ Disclaimer
> [!CAUTION]
> Modifying your bootloader or flashing custom images triggers the **Knox Warranty Void** bit. I am not responsible for bricked devices, though this fix is specifically designed to un-brick them from signature errors!
