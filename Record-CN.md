# 记录
[English Version](https://github.com/jdjingdian/DTK-Usage-Record/blob/master/Record.md)
---
#### 1.`pod install`时报错
[官方论坛讨论地址](https://developer.apple.com/forums/thread/652109)
```markdown
解决办法：当需要使用`pod install`的时候，通过Rosetta模式启动命令行来执行pod安装（按住 Command + I 键然后点击命令行图标，这样子应该就可以正常运行了）
```

#### 2.如何引导进入Recovery分区（也许只是DTK需要这样）
```markdown
1. 完全关闭DTK
2. 按住开机按钮直到系统指示灯由白色变成橘黄色（大概10~15秒）
3. 在选择界面选择设置选项并启动
```

#### 3.关闭SIP
```markdown
1. 进入recovery模式
2. 选择左上角的 苹果图标——Startup Disk——System——Security Policy——Reduced Security&&Allow kernel extensions from identified developers
3. 退出启动磁盘，在Utilities选项卡中选择Terminal
4. 输入	csrutil disable
5. 重启电脑
```

#### 4.进入DFU模式
```markdown
1. 完全关闭电脑
2. 拔掉电源线
3. 按住电脑开关然后接上电源线，继续按住电源3秒
4. 用靠近HDMI接口的USB-C接口连接其他Mac电脑
```

#### 5.安装iOS应用
**前言：**

直接从App Store上或者应用助手上下载的ipa文件是被加密过的，这种ipa目前是没有办法在Mac上运行的，所以必须先对ipa进行脱壳解密，然后再重新签名，才能安装到Mac上。

```markdown
1. 用工具将应用解密（必须拥有越狱设备，工具可以用frida)
2. 关闭SIP
3. 关闭AMFI
	打开终端输入：sudo nvram boot-args="amfi_get_out_of_my_way=1"，然后重启以生效
4. 在你的DTK上安装你的开发证书
5. 创建一个脚本
	 `#!/bin/sh
		codesign -d --entitlements :- "$1" > temp.xcent
		codesign -f -s "Apple Development: 你的开发者名字Han Mei Mei (XXXXXXXXXX)" --entitlements temp.xcent "$1"/Frameworks/*
		codesign -f -s "Apple Development: 你的开发者名字Han Mei Mei (XXXXXXXXXX)" --entitlements temp.xcent "$1"`
6. 在终端拖入脚本，按下空格，再拖入要重签名的.app(解压缩已经解密的ipa包，.app在Payload目录下)
7. 如无意外，应该可以成功运行

```

