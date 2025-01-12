# Flatpak

You will need the FreeDesktop.org 23.08 SDK installed, if you don't have it,
install [Flathub](https://flathub.org/) which provides it.

To build and install Sonic 1 Forever and Sonic 2 Absolute, you need Data.rsdk, decompiled scripts and the mod assets.

# Sonic the Hedgehog

To build and install the flatpak, run:
**System-wide:**
```
sudo flatpak-builder --install --force-clean sonic1 com.sega.Sonic1.json
```
**User:**
```
$ flatpak-builder --user --install --force-clean sonic1 com.sega.Sonic1.json
```
Run the game once for the next steps.


To get Data.rsdk, buy Android APK for the game from https://www.sega.com/games/sonic-hedgehog.
Once you have one, move the Data.rsdk to ```~/.var/app/com.sega.Sonic1/```

**To install scripts, run:**
```
git clone https://github.com/RSDKModding/RSDKv4-Script-Decompilation.git && cd RSDKv4-Script-Decompilation/
mv "Sonic 1/Scripts/ ~/.var/app/com.sega.Sonic1/"
```

**To install mod assets, run:**

```
git clone https://github.com/ElspethThePict/S1Forever.git && cd S1Forever/
mv Mods/ SonLVLObjDefs/ Forever.ini ~/.var/app/com.sega.Sonic1/
```

# Sonic the Hedgehog 2

To build and install the flatpak, run:
**System-wide:**
```
sudo flatpak-builder --install --force-clean sonic2 com.sega.Sonic2.json
```
**User:**
```
$ flatpak-builder --user --install --force-clean sonic2 com.sega.Sonic2.json
```
Run the game once for the next steps.


To get Data.rsdk, buy Android APK for the game from https://www.sega.com/games/sonic-hedgehog.
Once you have one, move the Data.rsdk to ```~/.var/app/com.sega.Sonic2/```

**To install scripts, run:**
```
git clone https://github.com/RSDKModding/RSDKv4-Script-Decompilation.git && cd RSDKv4-Script-Decompilation/
mv "Sonic 2/Scripts/ ~/.var/app/com.sega.Sonic2/"
```

**To install mod assets, run:**

```
git clone https://github.com/ElspethThePict/S2Absolute.git && cd S2Absolute/
mv Mods/ SonLVLObjDefs/ Absolute.ini ~/.var/app/com.sega.Sonic2/
```
