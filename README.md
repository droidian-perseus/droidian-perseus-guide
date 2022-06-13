# Droidian for the Xiaomi Mi MIX 3
A collection of tips to install and use Droidian on the Xiaomi Mi MIX 3 (perseus)

### Requirements
- A computer with fastboot and adb access to the phone
- A USB 2.0 port/hub with actual USB 2.0 controller (fastboot on USB 3.0 can be problematic with Xiaomi devices)
- Unlocked bootloader
- Backup all your data, as **your phone will be WIPED**

## Installation
### 0. Download files
- Latest [TWRP](https://dl.twrp.me/perseus/twrp-3.6.2_9-0-perseus.img)
- Android 9 [Vendor](https://github.com/TryHardDood/mi-vendor-updater/releases/download/perseus-weekly/fw-vendor_perseus_miui_MIMIX3_9.9.3_a9dbc91c30_9.0.zip)
- Latest nightly of `droidian-rootfs` for `arm64` from [the Droidian](https://images.droidian.org/rootfs-api28gsi-all/nightly/arm64/generic/rootfs.zip)
- Latest [adaptation zip](https://github.com/droidian-perseus/android-recovery-perseus-adaptation/releases/download/v1/android-recovery-perseus-adaptation-20220613.zip)

### 1. Install TWRP 
- Boot to fastboot mode by pressing the Vol- and Power buttons until the phone vibrates
- Check that the phone is recognized by running `fastboot devices`
- Install TWRP by running `fastboot flash recovery twrp-*-perseus.img`

### 2. Install Droidian in TWRP
TWRP:
- Boot into TWRP by pressing Vol+ and Power buttons until the phone vibrates
- Go to `Wipe` and `Format data` (type yes)
- IMPORTANT: **Reboot into TWRP again**

PC:
- Connect the phone via USB
- The internal storage is now available over MTP from the PC
- Copy the downloaded files to the internal storage of the phone

TWRP:
- Install zip file: fw-vendor_perseus_miui_MIMIX3_9.9.3_a9dbc91c30_9.0.zip
- Install zip file: `droidian-rootfs-api28gsi_arm64_YYYYMMDD.zip` 
- Install zip file: `android-recovery-perseus-adaptation_YYYYMMDD.zip`
- Go back to main menu and reboot to `System` (TWRP might complain that there is no OS installed, but that's fine)
- The first boot may take longer, and at least one spontaneous reboot is expected during the process
- If all goes well, your phone will boot to the Droidian lock screen, the unlock code is `1234`
- Installation is complete

## Notes

### SIM slot
Dual-SIM mode is not supported as of now. Only the SIM1 slot is active.

### Mobile data
Basic cellular features (phone calls, SMS) and mobile data are working. In order to get mobile data, set your Access Point Name (`APN`) in `Settings`.

### Additional tweaks
For other tweaks, open the `Console` terminal app, and run `perseus-extras.sh`.
The following options are available:
- Switching between dark mode and light mode (Adwaita theme)
- Automated installation of Waydroid (GAPPS included)

## Credit
[Perseus X](https://github.com/xperseus-dev)
[Joel Selvaraj](https://github.com/joelselvaraj)
[1petro](https://github.com/1petro)
[Droidian](http://droidian.org/)
[UBports](https://ubuntu-touch.io/)


For further assistance, visit the [MIX 3 Community](https://t.me/MiMix3Global) and [Droidian](https://t.me/droidianlinux) Telegram groups.
