=====================================================
APPS TO BE REMOVED
=====================================================

Google app paths:
Play Music - com.google.android.music
Play Videos - com.google.android.videos
Google Photos - com.google.android.apps.photos

Facebooks App paths:
com.facebook.appmanager
com.facebook.services
com.facebook.system

Android Studio > Whats New > SDK platform Tools for adb, fastboot, and systrace
https://developer.android.com/studio/releases/platform-tools
https://www.microsoft.com/en-us/download/confirmation.aspx?id=53840
https://developer.android.com/studio/command-line/adb

=====================================================
PRE-INSTALLATION CHECKLIST FOR CUSTOM ROM INSTALLATION
=====================================================

Custom ROM Installation Process:
> Backup factory ROM and Data from recovery for Nandroid backup
> Flash custom ROM
> If sucessfull, reboot to recovery and Wipe/Factory Rest (Dalvik Cache, Cache and Data)
> Flash Gapps or microGApps and setup phone
> If failure restore backedup factory ROM for Nandroid image

Root not required to install custom ROM, bootloader unlock and custom recovery is required as factory recovery will only flash signed images
For older phone you have a seperate boot and recovery partition due to which only recovery is flashed available as an *.img file
On never phones boot and recovery are together so a .img and a xxx-installer.zip is available for twrp

LG devices will delete twrp recovery on boot
For Samsung devices which use ODIN a different recovery file is needed
Never Windows have ADB drivers but they are wrong. Proper drivers for ADB have to be downloaded and installed for Windows. This is not required for Linux or Mac.
Sometime no-verify-opt-encrypt may not work if decrypting the entire filesystem and some data may remain encrypted
adb logcat -v long > logcat.txt #If something goes wrong get the log in the cwd
fastboot reboot #to reboot phone

=====================================================
CUSTOM ROM INSTALLATION PROCESS
=====================================================

Preparation - Collect information and required files:
> Check build, version from About Phone better take a screenshot. Check whether phone is treble supported and partition type (A or A/B)
> Pull a buildprops file from adb (adb pull /system/build.prop OR fastboot getvar all)
> build.prop value of ro.product.name gives device code name
> adb getprop ro.treble.enabled should return true for Treble support
> Some newer phones have /recovery in /boot for these there is a seperate twrp-installer.zip to be installed in the /boot. These phones should not be flashed twrp.img and the twrp installer needs to be on the phone as it will need to be installed after each time a custom ROM is flashed.
> Check for a recovery. root, unroot, custom ROM and GApps (pico) for your phone if available download all these and also stock ROM as backup
> Check if phone is encrypted in which case a No-verify-opt-encrypt.zip file is also requried to be downloaded as well
> If rooting with Magisk.zip then also get a Magisk-unintaller.zip and a Magisk Manager APK
> When booting from twrp you will see a message "Unmodified system partition" if phone is encrypted and will need your PIN to decrypt or do a data wipe

=====================================================

ADB and Fastboot Installation:
> Download platform-tools and put it into a folder and add that path to the session path with a batch file
> Install ADB drivers > after connecting phone it should install Google ADB interface
	<phone name> and under it <phone name ADB interface> should show in device manager after installing ADB drivers

=====================================================

Bootloader Unlocking Process: UNLOCKING BOOTLOADER WIPES DATA, BACKUP DATA BEFORE THIS
> Copy all files to be flashed to the folder with fastboot and adb
> Enable developer mode (Click 7 times on build number in settings)
> Enable USB Debugging (Settings)
> Enable "OEM Unlock" in settings (Andoid M onwards has this option)
> Connect device and put it in in file tranfer mode (MTP) #for general compaitibility not necessary in most cases
adb devices #check if your device is showing (should show an ID and say device next to it) it will confirm is drivers are installed. USB debugging must be enabled on the phone and install via USB should be enabled in developer options, connect in file transfer mode  and accept connection on device
adb reboot bootloader #to go into fastboot mode or Vol Up+Pwr button
fastboot devices #should show your device with an ID and say fastboot next to it which means fastboot is working
fastboot oem device-id #should give device ID if drivers are properly installed good command to verify before making system changes
fastboot oem unlock #to unlock bootloader replace with lock for locking bootloader
fastboot flashing unlock #for new version (if previous command doesn't work)) again replace with lock to lock

=====================================================

Recovery Flashing Process:
fastboot flash recovery <filename>.img #Many devices will replace custom recovery after installation. To prevent this TWRP will patch the stock ROM if you reboot into recovey after flashing TWRP
ALTERNATE:
fastboot boot twrp.img #boot image through fastboot which is temporary there is no flashing

=====================================================

Rooting Process:
> Copy Magisk.zip, Magisk-unintaller.zip and Magisk Manager APK to the device
> Flash Magisk from recovery if there are errors then flash Magisk uninstaller
> After booting into the device if you dont see Magisk Mager in Apps then intall the APK
> Open Magisk Manager and check version for instll verification and also do Safely Net check

=====================================================
USEFUL COMMANDS
=====================================================

Other ADB commands:
adb reboot recovery #To go to recovery
adb reboot download #To go to ODIN
adb install <packagename>
adb shell #Or prefix each commands with "adb shell". Admin priveleges may be required to go into adb shell
$> cmd appops set <pkgname> RUN_IN_BACKGROUND ignore #to disable background running use "allow" to enable 
$> cmd appops set <pkgname> WAKE_LOCK ignore #to disable Wakelock. Use "allow" to enable
$> pm list packagees | grep <pkgname> #list all packages and pipe them to grep such as "amazon/flipkart/Xiaomi/samsung" etc
$> pm list packages -d #list all
$> pm hide <pkgname> #hide apps use "nohide" to show for pre-5.0 use "block"
$> pm disable <packagename> #System will ignore these pacakages. "enable" to enable again. If it doesn't enable sometime it can happen, then factory reset.
$> pm uninstall -k --user 0 <name of package> #Using -k will leaave cache and data in place allows prevents checks for some OEM software allowing uninstall. It uninstalls only for one user so package will remain on system. System apps in system partition can be disabled as uninstalling it will not give back space as the system partition is not used for any other purpose.
$> pm uninstall <packagename> #to remove the 0kb entries after uninstalling an app. <packagename> here is the name of the 0kb entry
$> pm clear <pkgname> #delete data
$> cmd package install-existing <name of package> #to install system package again
$> chmod 755 /pathtoapplication/applicationname #Only chmod after copy to andriod FS. If file has been copied from FAT32 parition which doens't save permissions
$> rm </path/filename> #To delete files. Required to be mounted as rw
adb push <filename> </pathtodirectoryonphone/> #copy files to phone
adb pull </pathtofile/filename> <destination> #copy files to computer

Other fastboot commands:
fastboot flash boot boot.img
fastboot flash system system.img
fastboot flash userdata data.img
fastboot reboot 

Other Android commands:
mount -o rw,remount /dev/block/stl9 /system #mount a partition as rw
dd if=/sdcard/test.txt of=/system/app/test.txt #copying files within phone safter than cp command
