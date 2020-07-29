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
4. 输入`csrutil disable`
5. 重启电脑
```

#### 4.进入DFU模式
```markdown
1. 完全关闭电脑
2. 拔掉电源线
3. 按住电脑开关然后接上电源线，继续按住电源3秒
4. 用靠近HDMI接口的USB-C接口连接其他Mac电脑
```