# Device Checklist for Pocophone F1 (beryllium) on Droidian
This represents the state of the Droidian port when flashed according to the [guide](https://github.com/Unofficial-droidian-for-pocof1/droidian-beryllium-guide).
 
### Working
- Actors: Manual brightness
- Actors: Notification LED
- Actors: Torchlight
- Actors: Vibration
- Bluetooth: Driver loaded at startup
- Bluetooth: Enable/disable and flightmode works
- Bluetooth: Pairing with headset works, volume control ok
- Bluetooth: Persistent MAC address between reboots
- Camera: Ensure proper cameras are in use
- Camera: Flashlight
- Camera: Photo
- Camera: Switch between back and front camera
- Cellular: Carrier info, signal strength
- Cellular: Change audio routings (Speakerphone, Earphone)
- Cellular: Flightmode works
- Cellular: Incoming, outgoing calls
- Cellular: Voice in calls
- Cellular: SMS in, out
- Endurance: Battery lifetime > 24h from 100%
- Misc: Waydroid
- Misc: AppArmor patches applied to kernel
- Misc: Battery percentage
- Misc: Date and time are correct after reboot (go to flight mode before)
- Misc: Online charging (Green charging symbol, percentage increase in stats etc)
- Misc: SD card detection and access
- Sensors: Automatic brightness
- Sensors: Rotation works in Phosh
- Sensors: Touchscreen registers input across whole surface
- Sound: Loudspeaker, volume control ok
- Sound: Microphone, recording works
- Sound: System sounds and effects plays correctly (Camera shutter, Screenshot taken, Notifications)
- USB: SSH access (`ssh droidian@10.15.19.82`)
- WiFi: Driver loaded at startup (see instructions for first boot, otherwise works)
- WiFi: Enable/disable and flightmode works
- WiFi: Hotspot can be configured, switched on and off (network is working, no internet access)
- WiFi: Persistent MAC address between reboots

### Working with additional steps
- Misc: Reset to factory defaults (can be done in recovery)

### Not working
- Camera: Video (creates an empty `.mkv` file and freezes; in Waydroid camera functions fully)
- Sensors: Fingerprint reader, register and use fingerprints (fingerprint sensor just wakes up screen)
- Cellular: Data connection
- Cellular: Enable/disable mobile data
- Cellular: Switch connection speed between 2G/3G/4G works for SIM2 (no mobile data)
- Cellular: Switch preferred SIM for calling and SMS (no dual SIM support)
- WiFi: Hotspot cannot serve data to clients (no mobile data)
- Misc: Shutdown / Reboot (phone hangs after both, long press Power button to turn on again)
- Misc: Offline charging (Power down, connect USB cable, device boots to Droidian)
- GPU: Hardware video decoding (no support yet)
- USB: ADB access (use SSH instead: `ssh droidian@10.15.19.82`)
- USB: MTP access (use SCP instead: `scp your_file_to_copy droidian@10.15.19.82:/home/droidian`)

### Not tested
- Cellular: MMS in, out
- Cellular: PIN unlock
- Misc: logcat, dmesg & syslog do not spam errors and service restarts
- Sensors: GPS
- Sensors: Proximity works during a phone call
- Sound: Earphones detected, volume control ok
- Endurance: No reboot needed for 1 week (let us know if you achieved this)
