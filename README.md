# Display driver patch for Wexler Tab 7200, 3.3.0 kernel
### Fixes non-square pixel
Full kernel source:

http://dl.linux-sunxi.org/SDK/A20-SDK-2.0/aw.tar.bz2 (linux-3.3 folder)

Works with TAB7200_A20_4.2.2_4.2.2_2013071102_0308_ru firmware, 3.3.0 kernel

Does not work with 3.4.39+ kernel

Sets screen framebuffer size to 864x480 and displays only 854x480+5+0 region
Set android virtual screen resolution to 854x480 to make it fill that region

## Installation:

Put disp.ko and gt9xx_ts.ko to /system/vendor/modules and chmod it to 755

```
adb remount
adb push gt9xx_ts.ko /system/vendor/modules/
adb push disp.ko /system/vendor/modules/
adb shell chmod 755 /system/vendor/modules/*
```

Mount nanda partition

```
adb shell mkdir /mnt/nanda
adb shell busybox mount /dev/block/nanda /mnt/nanda
```

Put script.bin and script0.bin to /mnt/nanda/

```
adb push script0.bin /mnt/nanda
adb push script.bin /mnt/nanda
```

Set screen resolution to 854x480

```
adb shell am display-size 854x480
```

Reboot your device

```
adb shell sync
adb reboot
```
