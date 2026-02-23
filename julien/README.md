# FileCarver

## Installation de RootAVD
```bash
git clone https://gitlab.com/newbit/rootAVD.git
cd rootAVD
sudo chmod +x rootAVD.sh
```

**Chemin vers le AVD du Androidphone** : /home/julien/.var/app/com.google.AndroidStudio/config/.android/avd/Medium_Phone.avd/

**WorkingDirectories** : 
- le repo du projet
- ~/Git_Repos/rootAVD

## Chronologie

```bash
cd /home/julien/.var/app/com.google.AndroidStudio/config/.android/avd
ls
```

* Création du Pixel Android 13

```bash
# 1. Va dans le dossier de ton nouvel AVD
cd ~/.var/app/com.google.AndroidStudio/config/.android/avd/Pixel_5.avd

# 2. Affiche la ligne qui nous donne le chemin exact
cat config.ini | grep -E 'image.sysdir|android-'
image.sysdir.1=system-images/android-33/google_apis/x86_64/
target=android-33
```

* Trouver ramdisk.img pour 
```bash

ls ~/Android/Sdk/system-images/android-33/google_apis/x86_64/
 advancedFeatures.ini   build.prop   data   encryptionkey.img   kernel-ranchu   NOTICE.txt   package.xml   ramdisk.img   source.properties   system.img   userdata.img   vendor.img   VerifiedBootParams.textproto
 
```

* Démarrer la VM
 Lancer avec commande directement sans passer par AndroidStudio : 
 ```bash
 ANDROID_AVD_HOME=~/.var/app/com.google.AndroidStudio/config/.android/avd \
~/Android/Sdk/emulator/emulator -avd Pixel_5 -writable-system -no-snapshot &
```

* Vérif
```bash
~/Android/Sdk/platform-tools/adb devices
List of devices attached
emulator-5554	device
```

* Taper cette commande depuis le repo RootAVD
Ce script aura pour effet d'éteindre la VM Android, ce qui est normal. 
```bash
./rootAVD.sh system-images/android-33/google_apis/x86_64/ramdisk.img
```

Exemple : 

```bash
╭─julien@fedora ~/Git_Repos/rootAVD ‹master› 
╰─$ ./rootAVD.sh system-images/android-33/google_apis/x86_64/ramdisk.img
[!] and we are NOT in an emulator shell
[*] Set Directorys
[-] source.properties file exist
[*] AVD system-image Pkg.Revision=17
[-] Test if ADB SHELL is working
which: no adb in (/home/julien/Git_Repos/arsenal:/home/julien/.local/bin:/home/julien/.cargo/bin:/usr/local/bin:/usr/bin:/usr/local/sbin:/usr/sbin)
[!] ADB is not in your Path, try to:

export PATH=~/Android/Sdk/platform-tools:$PATH

[*] setting it, just during this session, for you
[-] Test if ADB SHELL is working
[*] ADB connection possible
[-] In any AVD via ADB, you can execute code without root in /data/data/com.android.shell
[*] Cleaning up the ADB working space
[*] Creating the ADB working space
[-] Magisk installer Zip exists already
[*] Push Magisk.zip into /data/data/com.android.shell/Magisk
[-] 
[*] create Backup File of ramdisk.img
[*] Push ramdisk.img into /data/data/com.android.shell/Magisk/ramdisk.img
[-] 
[*] Push rootAVD.sh into /data/data/com.android.shell/Magisk
[-] 
[-] run the actually Boot/Ramdisk/Kernel Image Patch Script
[*] from Magisk by topjohnwu and modded by NewBit XDA
[!] We are in a ranchu emulator shell
[-] Api Level Arch Detect
[-] Device Platform is x64 only
[-] Device SDK API: 33
[-] First API Level: 33
[-] The AVD runs on Android 13
[-] Switch to the location of the script file
[*] Looking for an unzip binary
[-] unzip binary found
[*] Extracting busybox and Magisk.zip via unzip ...
[*] Finding a working Busybox Version
[*] Testing Busybox /data/data/com.android.shell/Magisk/lib/x86/libbusybox.so
[!] Found a working Busybox Version
[!] BusyBox v1.36.1-Magisk (2023-09-02 05:30:11 PDT) multi-call binary.
[*] Move busybox from lib to workdir
[-] Checking AVDs Internet connection...
[!] AVD is online
[!] Checking available Magisk Versions
[?] Choose a Magisk Version to install and make it local
[s] (s)how all available Magisk Versions
[1] local stable '26.4' (ENTER)
[2] stable 30.6
[3] canary 30.6
[-] You choose Magisk local stable Version '26.4'
[*] Re-Run rootAVD in Magisk Busybox STANDALONE (D)ASH
[-] We are now in Magisk Busybox STANDALONE (D)ASH
[*] rootAVD with Magisk '26.4' Installer
[-] Get Flags
[*] System-as-root, keep dm/avb-verity
[-] Encrypted data, keep forceencrypt
[*] RECOVERYMODE=false
[-] KEEPVERITY=true
[*] KEEPFORCEENCRYPT=true
[-] copy all x86_64 files from /data/data/com.android.shell/Magisk/lib/x86_64 to /data/data/com.android.shell/Magisk
[-] copy 'stub.apk' from /data/data/com.android.shell/Magisk/assets to /data/data/com.android.shell/Magisk
[*] Detecting ramdisk.img compression
[!] Ramdisk.img uses lz4_legacy compression
[-] taken from shakalaca's MagiskOnEmulator/process.sh
[*] executing ramdisk splitting / extraction / repacking
[-] API level greater then 30
[*] Check if we need to repack ramdisk before patching ..
[-] Multiple cpio archives detected
[*] Unpacking ramdisk ..
[*] Searching for the real End of the 1st Archive
[-] Dumping from 0 to 1658643 ..
Detected format: [lz4_legacy]
[-] Dumping from 1658643 to 1719053 ..
Detected format: [lz4_legacy]
[*] Repacking ramdisk ..
[!] allowing MANAGE_EXTERNAL_STORAGE permissions to...
[-] Checking ramdisk STATUS=0
[-] Stock boot image detected
[*] Verifying Boot Image by its Kernel Release number:
[-] This AVD = 5.15.119-android13-8-00034-gd34029c8258b-ab10871489
[-]  Ramdisk = 5.15.119-android13-8-00034-gd34029c8258b-ab10871489
[!] Ramdisk is probably from this AVD
[-] Patching ramdisk
[*] Pre-init storage partition: metadata
[!] stub.apk is present, compress and add it to ramdisk
[*] adding overlay.d/sbin folders to ramdisk
Loading cpio: [ramdisk.cpio]
Create directory [overlay.d] (0750)
Create directory [overlay.d/sbin] (0750)
Dumping cpio: [ramdisk.cpio]
[!] patching the ramdisk with Magisk Init
Loading cpio: [ramdisk.cpio]
Add file [init] (100750)
Add file [overlay.d/sbin/magisk64.xz] (100644)
Add file [overlay.d/sbin/stub.xz] (100644)
Patch with flag KEEPVERITY=[true] KEEPFORCEENCRYPT=[true]
Loading cpio: [ramdisk.cpio.orig]
Backup [init] -> [.backup/init]
Record new entry: [overlay.d] -> [.backup/.rmlist]
Record new entry: [overlay.d/sbin] -> [.backup/.rmlist]
Record new entry: [overlay.d/sbin/magisk64.xz] -> [.backup/.rmlist]
Record new entry: [overlay.d/sbin/stub.xz] -> [.backup/.rmlist]
Create directory [.backup] (0000)
Add file [.backup/.magisk] (100000)
Dumping cpio: [ramdisk.cpio]
[*] repacking back to ramdisk.img format
[!] Rename Magisk.zip to Magisk.apk
[*] Pull ramdiskpatched4AVD.img into ramdisk.img
[-] 
[*] Pull Magisk.apk into 
[-] 
[*] Pull Magisk.zip into .
[-] 
[-] Clean up the ADB working space
[-] Install all APKs placed in the Apps folder
[*] Trying to install Apps/Magisk.apk
[*] Performing Streamed Install
[*] Success
[-] Shut-Down & Reboot (Cold Boot Now) the AVD and see if it worked
[-] Root and Su with Magisk for Android Studio AVDs
[-] Trying to shut down the AVD
[!] If the AVD doesn't shut down, try it manually!
[-] Modded by NewBit XDA - Jan. 2021
[!] Huge Credits and big Thanks to topjohnwu, shakalaca, vvb2060 and HuskyDG
```



* Retaper : 
```bash
ANDROID_AVD_HOME=~/.var/app/com.google.AndroidStudio/config/.android/avd \
~/Android/Sdk/emulator/emulator -avd Pixel_5 -writable-system -no-snapshot &
```