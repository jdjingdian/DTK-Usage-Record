# Record
[中文版链接](https://github.com/jdjingdian/DTK-Usage-Record/blob/master/Record-CN.md)
---
#### 1. `pod install` crashes out badly
[Official Forum Discussion Link](https://developer.apple.com/forums/thread/652109)
```markdown
Solution: When you need to use `pod install`, just open terminal in Rosetta mode( Command + I and clik the Terminal Icon, Then it should work fine.)
```

#### 2. How to boot into the local Recovery partiton?(Maybe DTK only)
```markdown
1. Power off the DTK completely
2. Press and hold the power button until the system indicator light turns from white to orange（about 10 ~ 15 seconds)
3. Choose setting selection and boot.
```

#### 3.Turn Off SIP
```markdown
1. Boot into Recovery.
2. Choose Apple Icon——Startup Disk——System——Security Policy——Reduced Security&&Allow kernel extensions from identified developers
3. Exit Startup Disk，choose Terminal in Utilities
4. Type  csrutil disable
5. Reboot and good to go
```

#### 4.Enter DFU mode
```markdown
1. Turn off DTK completely
2. Unplug power cable
3. Press and hold the power button and connect power cable, continue pressing power button for 3 seconds.
4. Use USB-C connector closest to HDMI port to connect with other mac
```

#### 5. Install iOS apps on DTK

**Introduction:**

**Ipa** download directly from the App Store or helper like *iMazing* are encrypted. This kind of ipa can not be run on the DTK, so we need to decrypt the app and resign it.

```markdown
1. Decrypt the ipa(You may need a jailbroken device to do this)
2. Turn off SIP
3. Turn off AMFI(Open Terminal and type: sudo nvram boot-args="amfi_get_out_of_my_way=1") . You need to reboot to take effect.
4. Install Developer certificate on your DTK
5. Create a script
	 `#!/bin/sh
		codesign -d --entitlements :- "$1" > temp.xcent
		codesign -f -s "Apple Development: 你的开发者名字Han Mei Mei (XXXXXXXXXX)" --entitlements temp.xcent "$1"/Frameworks/*
		codesign -f -s "Apple Development: 你的开发者名字Han Mei Mei (XXXXXXXXXX)" --entitlements temp.xcent "$1"`
6. Drag the script to the Terminal and then drag the app you want to resign after it.（Show the content and you will find the real .app file in Payload directory
7. The unmodified iOS app should now be running smoothly.
```

#### 6. Install X86 VMs
```
1. Download the latest ipa installer from UTM's GitHub repository.
2. Install it follow Section 5.
3. Launch UTM and install virtual machine.
```

