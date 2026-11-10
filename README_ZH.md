# WQ Files 中文版源码（基于官方 v0.7）

来源：https://github.com/kolbicz/WQFiles ，tag v0.7，GPL-3.0
已翻译：主菜单、常用按钮（取消/完成/保存/编辑/删除/分享/打开/恢复/清理）、应用/缓存清理/日志等标题。
未翻译：深层提示文案、日志内容、文件路径、数据键名（故意保留英文，避免破坏功能）。

## 为什么这里没有直接给你一个中文 IPA

这台编译机是 Linux，WQFiles 的 build.sh 必须用 macOS + Xcode：
`xcrun --sdk iphoneos`、`codesign`、`PlistBuddy`，Linux 上没有这些，
强行交叉编译出来的包很可能装不上 / 权限丢了（App Group 丢了就用不了）。

## 在 Mac 上一分钟编译

1. 把这个文件夹拷到 Mac 上
2. 终端进这个文件夹，运行：
   ./build.sh
3. 得到 WQFiles.ipa，用 SideKite / 其他签名工具重签，
   签名时保留 App Group 权限（group.cz.kolbi.wqfiles），再装到 iOS 26.0-26.7.2 / iOS 27 的手机上。
4. 打开 App 看 Log，确认没有 "No App Group"。

没有 Mac 的话，先用英文原版 + 下面这张对照表顶一下：
应用=Apps，缓存清理=Cache Cleaner，跳转到路径=Go to Path，应用备份=App Backups，备份=Backups，日志=Log
取消=Cancel，完成=Done，保存=Save，编辑=Edit，删除=Delete，分享=Share，打开=Open，恢复=Restore，清理=Clean

## 在 GitHub 上编译（不用自己有 Mac）

1. 在 GitHub 上新建一个公开/私有仓库，把这个文件夹全部传上去
2. 点仓库上方的 Actions，找到 "Build WQFiles zh"，点 Run workflow
3. 等几分钟跑完，点那次运行记录，下方 Artifacts 里下载 WQFiles-zh
4. 解压得到 WQFiles.ipa，用 SideKite 重签（保留 App Group 权限）再装
