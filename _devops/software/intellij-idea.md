---
title: "IntelliJ IDEA"
sequence: '002'
---

## 安装

- 第一步，在飞秋共享 `Software/D_软件开发/Jetbrains/idea` 文件夹内，下载 `ideaIU-2022.3.2.win.zip` 和 `app.jar` 文件
- 第二步，解压 `ideaIU-2022.3.2.win.zip`
- 第三步，替换 `lib/app.jar` 文件
- 第四步，启动 IDEA， 输入 License Server: `https://In.God.We.Trust`

## 设置 UTF-8 编码

Settings --> Editor --> File Encodings

- 将 **Global Encoding** 和 **Project Encoding** 设置为`UTF-8`
- 在 Properties Files 处，将 **Default encoding for properties files** 设置为 `UTF-8`，并勾选 **Transparent native-to-ascii conversion**

{:refdef: style="text-align: center;"}
![](/assets/image/windows/software/intellij-idea/settings-editor-file-encodings-utf8.png)
{: refdef}

## 快捷键

### 上下移动代码行

有的时候，想把当前代码行向上或向下移动两行，复制和粘贴挺麻烦，可以使用快捷键：

- `Ctrl + Shift + Up/Down`

### Debugging

主要的键盘值：`F7`~`F9`

1、断点

- `Ctrl + F8`: Toggle breakpoint
- `Ctrl + Shift + F8`: View breakpoints

2、单独键：

- `F7`: Step into
- `F8`: Step over
- `F9`: Resume program

3、组合键

- `Shift + F7`: Smart step into
- `Shift + F8`: Smart step out
- `Alt + F8`: Evaluate expression
- `Alt + F9`: Run to cursor

### Bookmark

切换：

- `F11`: Toggle bookmark
- `Ctrl + F11`: Toggle bookmark with mnemonic

切换和跳转：

- `Ctrl + Shift + #[0-9]`: Toggle numbered bookmark
- `Ctrl + #[0-9]`: Go to numbered bookmark

查看：

- `Shift + F11`: Show bookmarks
- `Alt + 2`: Bookmarks tool window

- 添加或移除Bookmark: `Ctrl + Shift + 数字键`
- 跳转到指定的Bookmark: `Ctrl + 数字键`
- 查看所有的Bookmarks: `Alt + 2`


