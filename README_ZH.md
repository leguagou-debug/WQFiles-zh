# WQ Files 中文版源码（基于官方 v0.7）

来源：https://github.com/kolbicz/WQFiles ，tag v0.7，GPL-3.0
已翻译：全部用户可见界面文字（见下文“全量界面汉化”）。
未翻译：日志正文、文件路径、数据键名（故意保留英文，避免破坏功能）。

## 全量界面汉化（2026-11-10 第二版）

第一版只翻了主菜单和常用按钮，用户反馈“还有好多没有翻译”，
第二版把剩下的界面文字全部翻成中文，共约 530 处字符串，覆盖：

- 主界面：Containers / Tools 分区标题、四项容器入口、底部两段说明、作者署名区
- 缓存清理页：标题、可清理数、扫描进度与“扫描不完整”说明、选择菜单（全选/全不选/大缓存）、
  每行 cache/temp 详情、崩溃日志行、页脚删除范围说明、清理确认框与清理结果
- 应用列表页：搜索框、表头/页脚说明、每行状态（无法访问/无标识符/已备份等）、
  备份/恢复/清除的全部弹窗与结果提示
- 文件浏览页：搜索框、新建/导入/复制路径/重命名/删除、备份多选与删除确认、
  恢复/替换确认、系统组列表与“打开系统组”
- 文本查看器、Plist 编辑器（含类型名：字符串/整数/实数/布尔值/日期/数据/字典/数组/引用）、
  十六进制查看器：全部按钮、菜单、弹窗、输入提示与保存/放弃确认
- 分享流程、保存/编码失败等错误提示、权限不足提示

`tests/browser_ui_regressions.py` 里原来断言英文界面文字的 9 处检查已同步改成断言中文，
本地运行结果：`browser UI regression checks: PASS`。

### 仍保留英文的部分及原因

- 日志正文（Log 页与 `wq_log` 输出）：诊断用，保留英文便于对照上游 issue 与报错原文。
- 文件路径、Bundle ID、entitlements 里的 `group.cz.kolbi.wqfiles`：改了就用不了。
- 数据键与清单字段：`Container` / `Backup` / `Safety` 等 journal key、`Created` / `Sequence` / `Reason` 等
  manifest 字段、备份原因值（如 `invalid manifest`、`no typed manifest`）——既是数据又是显示，
  翻了会破坏读写与校验逻辑，只翻纯显示用法。
- 系统 App 的备用显示名表（`WQLaunchServices.m` 内 `wq_builtin_names`）中无明确中文官方名的品牌与内部服务名，
  如 Safari、App Store、FaceTime、Siri、Keynote、SpringBoard 等；知名 App（天气、照片、文件、设置等）已翻成中文。
- `YES` / `NO`（Plist 布尔值摘要）、`tmp`（目录名）、`Library/Caches`（路径）、`osanalytics`（服务名）、
  `de ad be ef` / `0x0`（输入示例）、`WQ Files`（App 名与作者署名）、十六进制占位文本：属于值、路径或专名。
- `identity validation failed` 等仅写入日志的内部原因串：界面不显示，保留英文。
- 因 `%@` 复数后缀在中文里没有对应形式，少数格式串去掉了英文复数后缀 `s`（如“%lu 个容器”），
  调用处多传的参数会被忽略，不影响运行。

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
