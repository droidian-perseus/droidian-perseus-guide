# Droidian for the Poco F1
A collection of tips to install and use Droidian on the Pocophone F1 (beryllium)

### Requirements
- A computer with fastboot and adb access to the phone
- A USB 2.0 port/hub with actual USB 2.0 controller (fastboot on USB 3.0 can be problematic with Poco F1)
- Unlocked bootloader
- Backup all your data, as **your phone will be WIPED**
- It is also recommended to take a note about your `Acces Point Name` in Android `Settings` before starting the procedure (you will need it for mobile data)

## Installation
### 0. Download files
- Latest nightly or stable release of `droidian-rootfs` and `droidian-devtools` for `arm64` from [the Droidian repo](https://github.com/droidian-images/rootfs-api28gsi-all/releases)
- Latest [boot image](https://github.com/Unofficial-droidian-for-pocof1/linux_android_xiaomi_beryllium/releases)
- Latest [adaptation zip](https://github.com/Unofficial-droidian-for-pocof1/android-recovery-beryllium-adaptation/releases)
- [Vendor image](https://github.com/ubports-beryllium/artifacts/releases/download/v3/vendor.img)
- Android 9 Pie [official firmware](https://xiaomifirmwareupdater.com/download/?file=fw_beryllium_miui_POCOF1Global_9.6.27_6673f8a455_9.0.zip)
- Latest [TWRP](https://dl.twrp.me/beryllium/)

### 1. Install TWRP 
- Boot to fastboot mode by pressing the Vol- and Power buttons until the phone vibrates
- Check that the phone is recognized by running `fastboot devices`
- Install TWRP by running `fastboot flash recovery twrp-*-beryllium.img`

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
- Install image: `boot.img` to `Boot` partition
- Install image: `vendor.img` to `Vendor` partition
- Install zip file: `fw_beryllium_miui_POCOF1Global_9.6.27_6673f8a455_9.0.zip`
- Install zip file: `droidian-rootfs-api28gsi_arm64_YYYYMMDD.zip` 
- Install zip file: `droidian-devtools_arm64_YYYYMMDD.zip`
- Install zip file: `android-recovery-beryllium-adaptation.zip`
- Go back to main menu and reboot to `System` (TWRP might complain that there is no OS installed, but that's fine)
- The first boot may take longer, and at least one spontaneous reboot is expected during the process
- If all goes well, your phone will boot to the Droidian lock screen, the unlock code is `1234`
- Now open the `King's Cross` terminal app and run this command: `sudo systemctl enable enable-ipa` (the password is `1234`)
- Reboot the phone (long press power button)
- Installation is complete
- Flashing the `devtools` zip enabled `SSH` over USB. To use it, connect your phone to your computer and type `ssh droidian@10.15.19.82`, the password is `1234` (on Windows, you may need [PuTTY](https://www.chiark.greenend.org.uk/~sgtatham/putty/))

## Notes

### SIM slot
Dual-SIM mode is not supported as of now. Only the SIM2 slot is active, so a microSD card can be used at the same time.

### Mobile data
Mobile data should work, but it needs to be set up manually. The good part is that the configuration is persistent, so you need to do this only once.
- Open the `Settings` app and tap `Mobile`, then tap `Access Point Names`
- Tap the `+` in the top right corner of the pop-up
- Fill out the textboxes based on your settings in Android. The `Name` can be anything, e. g., the name of your carrier. The `APN` is likely some sort of an URL, like `internet.carrier.net` or something similar. If you didn't see a `Username` and `Password` in Android, you can skip these. 

In some cases, rebooting your phone or turning mobile data on and off a few times is enough.
Otherwise we'll have to give the same settings to [oFono](https://en.wikipedia.org/wiki/OFono) as well.
- Open the `King's Cross` terminal app or use `SSH` and type `cd /usr/share/ofono/scripts`
- To check your current setup, type `./list-contexts`, look for the first context, called `[ /ril_1/context1 ]`
- Notice that context has `Name`, `Type`, `AccessPointName`, `Username`, and `Password` attributes among others, we'll need to change these to match the valid settings from Android. 
- Now deactivate this context to be able to make changes to it: `./deactivate-context 1`
- And now make your changes like this: `./set-context-property 1 $ATTRIBUTE $VALUE`, where the `1` is for `[ /ril_1/context1 ]`, the `$ATTRIBUTE` is one of the attributes listed above, and the `$VALUE` will be the value you need to enter. make sure that the `Name` and `AccessPointName` match the `Name` and `APN` you entered in the settings menu. If an attribute needs to be empty, set it to `""`.
- When you make your changes, you can use `./list-contexts` to see them.
- When everything looks good, activate the updated context: `./activate-context 1` 
- If all went well, by running`./list-contexts` again you should see that the `Active` attribute is now `1`, and under the `Settings` attribute you can see the network parameters (Address, Netmask, Gateway, etc.) assigned by your carrier.
- You may need to reboot or turn mobile data on and off a few times, but mobile data should be working now.

- Pro tip: once you configured everything, you can type `history` to see your previous commands. Save them to a script that does all of this for you next time.

### Additional tweaks
For other tweaks, open the `King's Cross` terminal app, and run `beryllium-extras.sh`.
The following options are available:
- Notch fix (moves the clock from its original invisible position to the right side)
- Switching between dark mode and light mode (Adwaita theme)
- Automated installation of Waydroid

## Credit
[Joel Selvaraj](https://github.com/joelselvaraj)

[1petro](https://github.com/1petro)

[Droidian](http://droidian.org/)

[UBports](https://ubuntu-touch.io/)

[Yunior](https://gitlab.com/Yuniorkaito) 

For further assistance, visit the [Droidian for Poco F1](https://t.me/pocof1droidian) and [Droidian](https://t.me/droidianlinux) Telegram groups.
