# 黏黏世界光标

把《黏黏世界》(World of Goo) 里那只黏黏球，变成你系统里的鼠标指针。

它会跟着指针呼吸、拖尾、收缩，而真正的系统光标被藏了起来 —— 有那么一瞬间，你会觉得桌面变成了游戏里的一关。

macOS 和 Windows 都能用，直接去 [Releases](https://github.com/ccrichard3/WoGCursormouse/releases) 下最新版就行。

## 先看看效果

macOS：指针停下来的时候，黏黏球在安静地呼吸

![macOS](docs/mac.png)

Windows：快速拖动时，会拖出一条长长的尾巴

![Windows](docs/windows.png)

设置窗口：颜色、大小、拖尾长度、呼吸周期，都能自己调

![设置](docs/settings.png)

## 怎么装

### macOS

1. 双击 dmg，把 `WoGCursormouse.app` 拖进「应用程序」文件夹
2. 打开它，然后就不用管了 —— 它会安静地待在菜单栏里

第一次打开大概率会被系统拦下来。这不是你的问题：这个应用是本地构建、没有 Apple 签名，Gatekeeper 自然会警惕。右键点它选「打开」，或者在终端跑一句：

```bash
xattr -d com.apple.quarantine /Applications/WoGCursormouse.app
```

### Windows

1. 解压，文件夹放哪都行，比如 `D:\Tools\`
2. 双击 `WoGCursormouse.exe`

四个文件要放在同一个目录里，别只把 exe 单独拎出来。

## 怎么用

Windows 和 macOS 的操作习惯不太一样，这里说清楚：

- **Windows**：左键单击托盘图标打开设置；**右键单击直接退出**。想退出的时候不用再翻菜单。
- **macOS**：点菜单栏图标，里面什么都有 —— 设置、暂停、隐藏光标、开机自启动、退出。

设置窗口里能调的东西：

- 光标颜色、边框颜色
- 黏黏球的大小（呼气半径 / 吸气半径）、边框粗细
- 拖尾长度、呼吸周期、刷新率
- **应用黑名单**：哪些应用在前台时不想看到黏黏球。默认已经加了 **Bob**（截图工具），因为它的取色十字光标被盖住会很难用
- **暂停效果**：临时让它歇一会儿

## 高级设置（没有界面）

**拖尾采样率（ShrinkRate，默认 200）** 决定拖尾衰减得多快。它和「刷新率」是两件不同的事：刷新率只管画面画得多快，采样率管的是拖尾本身能活多久。默认参数下，85 ÷ 200 ≈ 0.43 秒，也就是尾巴从出现到消失大约半秒。

两端都没有为它做控件，想改只能手写配置：

- Windows：退出程序，编辑 exe 同目录的 `Settings.ini`，在 `[Settings]` 段里改 `ShrinkRate=200`
- macOS：`defaults write com.ccrichard3.wogcursor shrinkRate -float 200`，然后重启程序

调大，尾巴更短、更「贴手」；调小，尾巴更长更飘。低于 30 会明显一顿一顿的。

## 已知限制

- **macOS 上，应用自己画的光标换不掉。** 终端的选字工字光标、某些应用的十字光标会照常显示。这是 macOS 的机制：应用只在第一次解析光标时读一次表，之后缓存到进程结束，属于系统行为，绕不过去。解决办法是把那个应用加进上面的黑名单，让黏黏球暂时让位。
- **Windows 上，如果进程被强制结束，光标可能停在隐藏状态。** 重新启动一次程序就会自动恢复。
- macOS 版目前只支持 Apple 芯片。

## 致谢

- 特效创意与 **Windows 原版** by **Mygod** —— <https://github.com/Mygod/WoGCursor>
- 这个仓库是在原版失效多年之后，独立做的 macOS 重制，以及对 Windows 版的新系统适配
- 《World of Goo》是 2D Boy 的作品

---

# English

The GEN-U-INE cursor of *World of Goo*, out of the game and onto your desktop: a breathing,
trailing blob follows your pointer while the real system cursor is hidden.

Prebuilt binaries for **macOS (Apple silicon)** and **Windows (.NET Framework 4.8)** are on the
[Releases](https://github.com/ccrichard3/WoGCursormouse/releases) page. This repository ships binaries only — no source.

- **macOS**: open the `.dmg`, drag `WoGCursormouse.app` to Applications, then launch it. Menu-bar app.
  It is ad-hoc signed and not notarised, so right-click → Open the first time (or
  `xattr -d com.apple.quarantine`).
- **Windows**: unzip and keep all four files together, then run `WoGCursormouse.exe`.
  Left-click the tray icon for settings, right-click to quit.

The effect and the original Windows build are by **Mygod** (<https://github.com/Mygod/WoGCursor>);
this repository is an independent macOS port plus a modernisation of the Windows build.
*World of Goo* is a 2D Boy property.
