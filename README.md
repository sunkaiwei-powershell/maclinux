# maclinux 1.0 · 发布说明 / Release Notes

> **语言 / Languages**： [中文](#中文) · [English](#english) · [日本語](#日本語) · [한국어](#한국어) · [Deutsch](#deutsch)

---

## 中文

### 这是什么
**maclinux 1.0** 是一张「开箱即 macOS 风格」的 Live 定制镜像 —— 基于 **Kubuntu 24.04.5 LTS**（KDE Plasma 5.27 / X11）重制，把 macOS 的外观与交互习惯成体系地移植到 Linux 上：Dock、红绿灯窗口按钮、毛玻璃、慢节奏动画、动态视频壁纸、视频登录界面，并内置一个 Windows 11 风格的任务管理器。

它是一张 **Live 镜像**：可直接挂到虚拟机或写入 U 盘启动，**不需要安装到硬盘**。

### 基本信息
| 项目 | 内容 |
|---|---|
| 版本 | maclinux 1.0 |
| 底座 | Kubuntu 24.04.5 LTS（Plasma 5.27 / X11） |
| 镜像大小 | 5,656,215,552 字节（5.27 GB） |
| 构建时间戳 | 2026-10-18 09:42 UTC（镜像内 `cat /usr/share/maclinux/VERSION` 可查） |
| 整包 SHA-256 | `824da302e0ccd631cc271fe55c43b112ad9dbf5a70e62f936570d6da9eae43f3` |
| 分卷 | 4 卷，每卷 1.5 GB（1,500,000,000 字节）：`.001` `.002` `.003` `.004` |

### 分卷合并（本页对应上传的 4 个分卷）
分卷是**按字节顺序切开的**，必须**按序合并**，合并后大小必须等于 5,656,215,552 字节。

**Windows（CMD）**
```
copy /b maclinux-1.0.iso.001+maclinux-1.0.iso.002+maclinux-1.0.iso.003+maclinux-1.0.iso.004 maclinux-1.0.iso
```
（PowerShell 里请用 `cmd /c copy /b ...`）

**7-Zip**：选中 `maclinux-1.0.iso.001` → 右键 → 7-Zip → 解压到当前目录（或「合并文件」）

**Linux / macOS**
```
cat maclinux-1.0.iso.0* > maclinux-1.0.iso
```

**校验合并结果（Windows）**
```
certutil -hashfile maclinux-1.0.iso SHA256
```
结果应与上方「整包 SHA-256」完全一致；各分卷的 SHA-256 见下：

| 分卷 | 大小 | SHA-256 |
|---|---|---|
| `maclinux-1.0.iso.001` | 1,500,000,000 | `{{P1_SHA256}}` |
| `maclinux-1.0.iso.002` | 1,500,000,000 | `{{P2_SHA256}}` |
| `maclinux-1.0.iso.003` | 1,500,000,000 | `{{P3_SHA256}}` |
| `maclinux-1.0.iso.004` | 1,156,215,552 | `{{P4_SHA256}}` |

### 怎么启动
- **虚拟机（推荐，已实测）**：VMware 新建虚拟机（客户机选 Linux / Ubuntu 64 位）→ CD/DVD 指向合并后的 ISO → 直接开机。建议 **4 GB 以上内存、2~4 个 CPU 核心**；要毛玻璃和动画流畅，请启用 **3D 加速**（镜像已预装 open-vm-tools / open-vm-tools-desktop）。**每次测试前请完全关机，不要挂起或恢复旧快照。**
- **U 盘**：用 **Rufus（DD 模式）** 或 **balenaEtcher** 写入，支持 BIOS 与 UEFI 双启动。
- **引导菜单**：GRUB 默认 5 秒后进入「**maclinux (Live 桌面)**」；如果显卡异常导致花屏/黑屏，选「**Kubuntu (safe graphics)**」（带 `nomodeset`）。
- **登录**：Live 会话自动登录进桌面；**注销或锁屏**时会出现 macOS 风格的登录界面（WhiteSur 主题 + 视频背景）。

### 首次启动会发生什么
登录进入桌面后约 4 秒，会依次：
1. 后台自动应用整套 macOS 美化（窗口装饰、Dock、毛玻璃、动画节奏、主题/配色/图标/光标/字体、动态壁纸）
2. 播放 hello 动画（白底黑字、循环；按任意键或点击可跳过）
3. 弹出欢迎向导

> 说明：Live 模式下家目录在内存里，所以**每次开机都会重新播一次**首次体验；美化本身每次登录都会自动重新应用一遍。

### 已实现的功能
**外观与交互**
- **Dock**：底部 Latte Dock —— 鼠标悬停**不放大**、毛玻璃半透明、程序启动时图标上下弹跳；内置启动器：访达(Dolphin)、**终端**、**系统设置**、**任务管理器**、KWrite、Gwenview、Ark、Firefox；最右还有**废纸篓**
- **红绿灯窗口按钮**：WhiteSur 原版（三个彩色圆点常显、悬停显示标志），按钮组靠左，窗口圆润
- **毛玻璃**：KWin 模糊开启（强度 4 / 噪点 0），拖窗更顺
- **动画节奏**：全局时长倍率 2.0（更慢、更"悠闲"）
- **动态壁纸**：视频位于**桌面最底层**，登录后从「流动」缓慢减速到定格（NASA 航拍素材 3 段）
- **静态壁纸**：Monterey / Sonoma / Ventura / WhiteSur 各深浅两版，共 8 张
- **登录界面**：SDDM WhiteSur-dark 主题 + 视频背景
- **图标 / 光标 / 字体**：WhiteSur 图标、WhiteSur-cursors 光标、Inter + Noto Sans CJK 字体
- **窗口装饰可切换**：`maclinux-deco klassy` 可换成 Klassy（可调窗口圆角）

**任务管理器（Windows 11 风格）**
- 左侧图标导航：**进程 / 性能 / 应用历史记录 / 启动 / 用户 / 详细信息 / 服务**
- **进程页**：按应用分组可展开、系统守护进程归入「系统进程」、每行应用图标、**CPU 列热度配色**（绿→黄→红）、可搜索排序、右键菜单（结束任务 / 结束进程树）
- **结束任务 = 最高权限**：经 pkexec 调用 root 助手发 **SIGKILL**，任何进程都无法拒绝；活动会话**免密**（polkit 规则）
- **性能页**：CPU / 内存 / 磁盘 / 网络 组件列表 + 网格曲线 + 利用率 / 速度 / 进程 / 线程 / 运行时间
- 其他页：应用历史记录（本会话累计 CPU）、启动项启停、会话注销、服务启停重启

### 内置命令
| 命令 | 作用 |
|---|---|
| `maclinux-taskmgr` | 任务管理器（Dock 上也有图标） |
| `maclinux-doctor` | **一键自检**：版本、Dock 状态、启动器、组件、日志尾部 |
| `maclinux-deco aurorae\|klassy` | 切换窗口装饰 |
| `maclinux-preview-login` | 在桌面会话里预览登录界面 |
| `maclinux-hello` / `maclinux-welcome` | 重播 hello 动画 / 欢迎向导 |
| 日志 | `~/.config/maclinux/apply-desktop.log` |

### 已知限制
- Live 镜像：**不提供「一键安装到硬盘」的定制向导**（菜单里的 OEM install 项属原版功能，未做定制）
- 进程「磁盘 / 网络」列：对**非本用户**的进程会显示 `—`（内核限制，读取需要更高权限）
- 「应用历史记录」为**本会话累计**，不做跨会话持久统计
- 视频壁纸会占用一定 CPU / GPU：虚拟机未开 3D 加速时建议改用静态壁纸
- 仅在 VMware 下实测；真机 U 盘启动请自行验证

### 排障
遇到「Dock 没出现 / 壁纸不动 / 没有毛玻璃」等情况，在桌面终端里跑：
```
maclinux-doctor
```
它会打印 ISO 身份、Dock 进程、布局里的启动器列表、组件是否到位、美化日志尾部 —— 把整段输出反馈即可定位。

### 许可与致谢
- **本项目原创部分**（构建流水线、任务管理器、动画/向导、视频壁纸插件、各脚本）：**CC BY-NC-SA 4.0**（署名 · 非商业 · 相同方式共享）
- **第三方组件**（版权归各自作者，遵循其原始许可）：Kubuntu 24.04 / KDE Plasma 5.27 / Latte Dock / WhiteSur-kde 与 WhiteSur SDDM 主题（vinceliuice）/ Klassy / NASA 航拍视频素材（公有领域）
- 本镜像不含任何 Apple 官方资源；macOS 相关素材均为社区复刻主题，仅供个人学习与美化

---

## English

### What this is
**maclinux 1.0** is a live, ready-to-run **macOS-look-alike Linux remaster** built on **Kubuntu 24.04.5 LTS** (KDE Plasma 5.27 / X11). It ports the macOS look and feel as a coherent set: Dock, traffic-light window buttons, frosted-glass blur, slow-paced animations, a live video wallpaper, a video login screen — plus a built-in **Windows 11 style task manager**.

It is a **live image**: boot it in a VM or write it to a USB stick — **no installation to disk required**.

### Basics
| Item | Value |
|---|---|
| Version | maclinux 1.0 |
| Base | Kubuntu 24.04.5 LTS (Plasma 5.27 / X11) |
| Image size | 5,656,215,552 bytes (5.27 GB) |
| Build stamp | 2026-10-18 09:42 UTC (`cat /usr/share/maclinux/VERSION` inside the image) |
| Whole-image SHA-256 | `824da302e0ccd631cc271fe55c43b112ad9dbf5a70e62f936570d6da9eae43f3` |
| Split parts | 4 parts × 1.5 GB (1,500,000,000 bytes): `.001` `.002` `.003` `.004` |

### Joining the split parts
The parts are a **raw byte split** — join them **in order**; the result must be exactly 5,656,215,552 bytes.

**Windows (CMD)**
```
copy /b maclinux-1.0.iso.001+maclinux-1.0.iso.002+maclinux-1.0.iso.003+maclinux-1.0.iso.004 maclinux-1.0.iso
```
(In PowerShell use `cmd /c copy /b ...`)

**7-Zip** — select `maclinux-1.0.iso.001` → right-click → 7-Zip → Extract here

**Linux / macOS**
```
cat maclinux-1.0.iso.0* > maclinux-1.0.iso
```

**Verify (Windows)**
```
certutil -hashfile maclinux-1.0.iso SHA256
```
It must match the whole-image SHA-256 above. Per-part hashes:

| Part | Size (bytes) | SHA-256 |
|---|---|---|
| `maclinux-1.0.iso.001` | 1,500,000,000 | `{{P1_SHA256}}` |
| `maclinux-1.0.iso.002` | 1,500,000,000 | `{{P2_SHA256}}` |
| `maclinux-1.0.iso.003` | 1,500,000,000 | `{{P3_SHA256}}` |
| `maclinux-1.0.iso.004` | 1,156,215,552 | `{{P4_SHA256}}` |

### How to boot
- **Virtual machine (tested)** — VMware: create a Linux / Ubuntu 64-bit VM, point CD/DVD at the joined ISO, power on. **4 GB+ RAM, 2–4 vCPUs**; enable **3D acceleration** for smooth blur/animations (open-vm-tools is preinstalled). **Fully shut the VM down between tests — do not resume an old snapshot.**
- **USB stick** — write with **Rufus (DD mode)** or **balenaEtcher**; BIOS and UEFI are both supported.
- **Boot menu** — GRUB auto-boots "**maclinux (Live 桌面)**" after 5 s; if graphics misbehave, pick "**Kubuntu (safe graphics)**" (`nomodeset`).
- **Login** — the live session auto-logs in; the macOS-style login screen (WhiteSur theme + video background) appears on logout or lock.

### First boot experience
About 4 seconds after login: macOS beautification is applied in the background, the hello animation plays (white background, black text, loop; press any key or click to skip), then the welcome wizard appears.

> In live mode the home directory lives in RAM, so this first-boot experience replays on every boot; beautification is re-applied on every login.

### Features
**Look & feel**
- **Dock** — bottom Latte Dock: **no hover zoom**, frosted translucency, launcher bounce; built-in launchers: Dolphin, **Konsole**, **System Settings**, **Task Manager**, KWrite, Gwenview, Ark, Firefox; plus **Trash** on the right
- **Traffic-light buttons** — WhiteSur original (three colored dots always visible, glyphs on hover), buttons on the left, rounded windows
- **Blur** — KWin blur on (strength 4 / noise 0) for smoother dragging
- **Animation pacing** — global duration factor 2.0 (slower, calmer)
- **Live wallpaper** — video sits on the **bottom layer of the desktop** and eases from "flowing" to frozen after login (3 NASA aerial clips)
- **Static wallpapers** — Monterey / Sonoma / Ventura / WhiteSur, light+dark, 8 total
- **Login screen** — SDDM WhiteSur-dark theme with video background
- **Icons / cursor / fonts** — WhiteSur icons, WhiteSur-cursors, Inter + Noto Sans CJK
- **Switchable decoration** — `maclinux-deco klassy` swaps in Klassy (adjustable corner radius)

**Task manager (Windows 11 style)**
- Left icon rail: **Processes / Performance / App history / Startup / Users / Details / Services**
- **Processes** — expandable per-app groups, system daemons under "系统进程", per-row app icons, **CPU heat colors** (green→yellow→red), search & sort, right-click menu (End task / End process tree)
- **End task = highest privilege** — pkexec → root helper → **SIGKILL**; no process can refuse. Passwordless for active sessions (polkit rule)
- **Performance** — CPU / Memory / Disk / Network list, grid graphs, utilization / speed / processes / threads / uptime
- **Others** — app history (session cumulative CPU), startup enable/disable, session logout, service start/stop/restart

### Built-in commands
| Command | Purpose |
|---|---|
| `maclinux-taskmgr` | Task manager (also on the Dock) |
| `maclinux-doctor` | One-shot self-check: version, Dock, launchers, components, log tail |
| `maclinux-deco aurorae\|klassy` | Switch window decoration |
| `maclinux-preview-login` | Preview the login screen inside the session |
| `maclinux-hello` / `maclinux-welcome` | Replay the hello animation / welcome wizard |
| Log | `~/.config/maclinux/apply-desktop.log` |

### Known limitations
- Live image: **no customized "install to disk" wizard** (the OEM install entry is stock, uncustomized)
- Disk / Network columns show `—` for processes **not owned by your user** (kernel restriction)
- "App history" is **per-session cumulative**, not persisted
- The video wallpaper costs CPU/GPU; switch to a static wallpaper without 3D acceleration
- Only tested under VMware; verify USB boot on real hardware yourself

### Troubleshooting
If the Dock is missing, the wallpaper is static, or blur is off, run in a terminal:
```
maclinux-doctor
```
It prints the ISO identity, Dock process, layout launchers, component presence and the beautification log tail — share that output.

### License & credits
- **Original work of this project** (build pipeline, task manager, animation/wizard, video-wallpaper plugin, scripts): **CC BY-NC-SA 4.0**
- **Third-party** (respective licenses): Kubuntu 24.04 / KDE Plasma 5.27 / Latte Dock / WhiteSur-kde & WhiteSur SDDM themes (vinceliuice) / Klassy / NASA aerial footage (public domain)
- No Apple assets are included; all macOS-like assets are community recreations for personal use

---

## 日本語

### これは何か
**maclinux 1.0** は、**Kubuntu 24.04.5 LTS**（KDE Plasma 5.27 / X11）をベースに作り直した「起動するだけで macOS 風」の Live カスタムイメージです。Dock、信号機ボタン、すりガラス、ゆったりしたアニメーション、動画壁紙、動画ログイン画面をまとめて移植し、さらに **Windows 11 風のタスクマネージャー**を内蔵しました。

**Live イメージ**なので、仮想マシンに接続するか USB に書き込むだけで起動でき、**ディスクへのインストールは不要**です。

### 基本情報
| 項目 | 内容 |
|---|---|
| バージョン | maclinux 1.0 |
| ベース | Kubuntu 24.04.5 LTS（Plasma 5.27 / X11） |
| イメージサイズ | 5,656,215,552 バイト（5.27 GB） |
| ビルド日時 | 2026-10-18 09:42 UTC（イメージ内 `cat /usr/share/maclinux/VERSION`） |
| 全体 SHA-256 | `824da302e0ccd631cc271fe55c43b112ad9dbf5a70e62f936570d6da9eae43f3` |
| 分割 | 4 分割・各 1.5 GB（1,500,000,000 バイト）：`.001` `.002` `.003` `.004` |

### 分割ファイルの結合
分割は**バイト単位の単純分割**です。**順番どおり**に結合してください。結合後のサイズは 5,656,215,552 バイトでなければなりません。

**Windows（CMD）**
```
copy /b maclinux-1.0.iso.001+maclinux-1.0.iso.002+maclinux-1.0.iso.003+maclinux-1.0.iso.004 maclinux-1.0.iso
```
（PowerShell では `cmd /c copy /b ...`）

**7-Zip** — `maclinux-1.0.iso.001` を選び → 右クリック → 7-Zip → ここに解凍

**Linux / macOS**
```
cat maclinux-1.0.iso.0* > maclinux-1.0.iso
```

**検証（Windows）**
```
certutil -hashfile maclinux-1.0.iso SHA256
```
上記の全体 SHA-256 と一致すれば正常です。各分割の SHA-256：

| 分割 | サイズ（バイト） | SHA-256 |
|---|---|---|
| `maclinux-1.0.iso.001` | 1,500,000,000 | `{{P1_SHA256}}` |
| `maclinux-1.0.iso.002` | 1,500,000,000 | `{{P2_SHA256}}` |
| `maclinux-1.0.iso.003` | 1,500,000,000 | `{{P3_SHA256}}` |
| `maclinux-1.0.iso.004` | 1,156,215,552 | `{{P4_SHA256}}` |

### 起動方法
- **仮想マシン（動作確認済み）** — VMware で Linux / Ubuntu 64bit の VM を作成 → CD/DVD に結合後の ISO を指定 → 起動。**メモリ 4 GB 以上、CPU 2〜4 コア**を推奨。すりガラスとアニメーションを滑らかにするには **3D アクセラレーション**を有効に（open-vm-tools はプリインストール済み）。**検証のたびに完全シャットダウンし、古いスナップショットを復元しないでください。**
- **USB メモリ** — **Rufus（DD モード）**または **balenaEtcher**で書き込み。BIOS / UEFI 両対応。
- **ブートメニュー** — GRUB は 5 秒後に「**maclinux (Live 桌面)**」を自動起動。画面が乱れる場合は「**Kubuntu (safe graphics)**」（`nomodeset`）を選択。
- **ログイン** — Live セッションは自動ログイン。**ログアウト／ロック時**に macOS 風ログイン画面（WhiteSur テーマ＋動画背景）が表示されます。

### 初回起動の流れ
ログインから約 4 秒後：バックグラウンドで macOS 風の美化を適用 → hello アニメーション（白背景・黒文字・ループ、任意のキー／クリックでスキップ）→ ウェルカムウィザード。

> Live モードではホームディレクトリがメモリ上にあるため、初回体験は**毎回の起動で再生**されます。美化は毎ログイン時に再適用されます。

### 実装済みの機能
**外観・操作**
- **Dock** — 下部の Latte Dock：ホバーで**拡大しない**、すりガラス半透明、起動時アイコンが跳ねる。内蔵ランチャー：Dolphin、**Konsole**、**システム設定**、**タスクマネージャー**、KWrite、Gwenview、Ark、Firefox、右端に**ゴミ箱**
- **信号機ボタン** — WhiteSur オリジナル（3 色の丸を常時表示、ホバーで記号）、左寄せ、角丸ウィンドウ
- **すりガラス** — KWin ブラー有効（強度 4 / ノイズ 0）
- **アニメーション** — 全体の時間倍率 2.0（よりゆっくり）
- **動画壁紙** — デスクトップ**最下層**で再生し、ログイン後に「流れる」状態からゆっくり停止（NASA 空撮 3 本）
- **静止壁紙** — Monterey / Sonoma / Ventura / WhiteSur の明暗 2 種ずつ、計 8 枚
- **ログイン画面** — SDDM WhiteSur-dark テーマ＋動画背景
- **アイコン／カーソル／フォント** — WhiteSur アイコン、WhiteSur-cursors、Inter + Noto Sans CJK
- **装飾の切替** — `maclinux-deco klassy` で Klassy（角丸調整可）に変更

**タスクマネージャー（Windows 11 風）**
- 左のアイコン列：**プロセス / パフォーマンス / アプリの履歴 / スタートアップ / ユーザー / 詳細 / サービス**
- **プロセス** — アプリ単位でグループ化・展開可、システムデーモンは「系统进程」に集約、行ごとのアプリアイコン、**CPU のヒートカラー**（緑→黄→赤）、検索・並べ替え、右クリックメニュー（タスクの終了／プロセスツリーの終了）
- **タスクの終了＝最高権限** — pkexec → root ヘルパー → **SIGKILL**。どのプロセスも拒否できません。アクティブセッションでは**パスワード不要**（polkit ルール）
- **パフォーマンス** — CPU / メモリ / ディスク / ネットワークの一覧、グリッドグラフ、使用率／速度／プロセス数／スレッド数／稼働時間
- **その他** — アプリの履歴（セッション累積 CPU）、スタートアップの有効/無効、セッションのログアウト、サービスの開始/停止/再起動

### 内蔵コマンド
| コマンド | 用途 |
|---|---|
| `maclinux-taskmgr` | タスクマネージャー（Dock からも起動可） |
| `maclinux-doctor` | **一括セルフチェック**：バージョン、Dock、ランチャー、コンポーネント、ログ末尾 |
| `maclinux-deco aurorae\|klassy` | ウィンドウ装飾の切替 |
| `maclinux-preview-login` | セッション内でログイン画面をプレビュー |
| `maclinux-hello` / `maclinux-welcome` | hello アニメ／ウェルカムウィザードの再生 |
| ログ | `~/.config/maclinux/apply-desktop.log` |

### 既知の制限
- Live イメージのため、**ディスクへのインストール用カスタムウィザードはありません**（OEM install はオリジナルのまま）
- 「ディスク / ネットワーク」列は**他ユーザーのプロセス**では `—` 表示（カーネル制限）
- 「アプリの履歴」は**セッション内の累積**で、永続化しません
- 動画壁紙は CPU/GPU を消費します。3D アクセラレーション無効時は静止壁紙を推奨
- 検証は VMware のみ。実機 USB 起動はご自身で確認してください

### トラブルシューティング
Dock が出ない／壁紙が動かない／すりガラスが無い場合は、ターミナルで：
```
maclinux-doctor
```
ISO の識別情報、Dock プロセス、ランチャー一覧、コンポーネントの有無、美化ログの末尾を出力します。そのまま共有してください。

### ライセンスと謝辞
- **本プロジェクトのオリジナル部分**（ビルドパイプライン、タスクマネージャー、アニメーション／ウィザード、動画壁紙プラグイン、各スクリプト）：**CC BY-NC-SA 4.0**
- **サードパーティ**（各原著者のライセンスに従います）：Kubuntu 24.04 / KDE Plasma 5.27 / Latte Dock / WhiteSur-kde・WhiteSur SDDM テーマ（vinceliuice）/ Klassy / NASA 空撮素材（パブリックドメイン）
- Apple 公式素材は含みません。macOS 風素材は個人利用を目的としたコミュニティ再現です

---

## 한국어

### 소개
**maclinux 1.0** 은 **Kubuntu 24.04.5 LTS**(KDE Plasma 5.27 / X11) 기반으로 다시 만든 「부팅하면 바로 macOS 스타일」인 Live 커스텀 이미지입니다. Dock, 신호등 버튼, 반투명 블러, 느긋한 애니메이션, 동영상 배경화면, 동영상 로그인 화면을 체계적으로 이식했고, **Windows 11 스타일 작업 관리자**까지 내장했습니다.

**Live 이미지**이므로 가상 머신에 연결하거나 USB에 쓰기만 하면 부팅되며, **디스크 설치가 필요 없습니다**.

### 기본 정보
| 항목 | 내용 |
|---|---|
| 버전 | maclinux 1.0 |
| 기반 | Kubuntu 24.04.5 LTS (Plasma 5.27 / X11) |
| 이미지 크기 | 5,656,215,552 바이트 (5.27 GB) |
| 빌드 시각 | 2026-10-18 09:42 UTC (이미지 내 `cat /usr/share/maclinux/VERSION`) |
| 전체 SHA-256 | `824da302e0ccd631cc271fe55c43b112ad9dbf5a70e62f936570d6da9eae43f3` |
| 분할 | 4개, 각 1.5 GB (1,500,000,000 바이트): `.001` `.002` `.003` `.004` |

### 분할 파일 합치기
분할은 **바이트 단위 단순 분할**입니다. **순서대로** 합치세요. 합친 크기는 정확히 5,656,215,552 바이트여야 합니다.

**Windows (CMD)**
```
copy /b maclinux-1.0.iso.001+maclinux-1.0.iso.002+maclinux-1.0.iso.003+maclinux-1.0.iso.004 maclinux-1.0.iso
```
(PowerShell 에서는 `cmd /c copy /b ...`)

**7-Zip** — `maclinux-1.0.iso.001` 선택 → 마우스 오른쪽 → 7-Zip → 여기에 압축 풀기

**Linux / macOS**
```
cat maclinux-1.0.iso.0* > maclinux-1.0.iso
```

**검증 (Windows)**
```
certutil -hashfile maclinux-1.0.iso SHA256
```
위의 전체 SHA-256 과 일치해야 합니다. 각 분할의 SHA-256:

| 분할 | 크기(바이트) | SHA-256 |
|---|---|---|
| `maclinux-1.0.iso.001` | 1,500,000,000 | `{{P1_SHA256}}` |
| `maclinux-1.0.iso.002` | 1,500,000,000 | `{{P2_SHA256}}` |
| `maclinux-1.0.iso.003` | 1,500,000,000 | `{{P3_SHA256}}` |
| `maclinux-1.0.iso.004` | 1,156,215,552 | `{{P4_SHA256}}` |

### 부팅 방법
- **가상 머신(권장, 검증됨)** — VMware 에서 Linux / Ubuntu 64비트 VM 생성 → CD/DVD 를 합친 ISO 로 지정 → 전원 켜기. **메모리 4GB 이상, CPU 2~4 코어** 권장. 블러와 애니메이션을 부드럽게 보려면 **3D 가속**을 켜세요(open-vm-tools 사전 설치됨). **테스트 전에는 항상 완전히 종료하고, 이전 스냅샷을 복원하지 마세요.**
- **USB 메모리** — **Rufus(DD 모드)** 또는 **balenaEtcher** 로 쓰기. BIOS / UEFI 모두 지원.
- **부팅 메뉴** — GRUB 는 5초 후 「**maclinux (Live 桌面)**」을 자동 부팅합니다. 화면이 깨지면 「**Kubuntu (safe graphics)**」(`nomodeset`)을 선택하세요.
- **로그인** — Live 세션은 자동 로그인입니다. **로그아웃/잠금** 시 macOS 스타일 로그인 화면(WhiteSur 테마 + 동영상 배경)이 나타납니다.

### 첫 부팅 흐름
로그인 후 약 4초 뒤: 백그라운드로 macOS 미화 적용 → hello 애니메이션(흰 배경·검은 글자·반복, 아무 키나 클릭으로 건너뛰기) → 환영 마법사.

> Live 모드에서는 홈 디렉터리가 메모리에 있으므로 첫 부팅 체험은 **부팅할 때마다 다시 재생**됩니다. 미화는 로그인할 때마다 다시 적용됩니다.

### 구현된 기능
**외관 · 조작**
- **Dock** — 하단 Latte Dock: 마우스를 올려도 **확대되지 않음**, 반투명 블러, 실행 시 아이콘 튀어오름. 내장 런처: Dolphin, **Konsole**, **시스템 설정**, **작업 관리자**, KWrite, Gwenview, Ark, Firefox, 오른쪽 끝에 **휴지통**
- **신호등 버튼** — WhiteSur 원본(3색 원 항상 표시, 호버 시 기호), 왼쪽 정렬, 둥근 창
- **블러** — KWin 블러 켜짐(강도 4 / 노이즈 0)
- **애니메이션** — 전체 시간 배율 2.0(더 느리게)
- **동영상 배경화면** — 데스크톱 **최하단 레이어**에서 재생, 로그인 후 「흐름」에서 서서히 정지(NASA 항공 촬영 3편)
- **정적 배경화면** — Monterey / Sonoma / Ventura / WhiteSur 밝음·어두움 각 2종, 총 8장
- **로그인 화면** — SDDM WhiteSur-dark 테마 + 동영상 배경
- **아이콘 / 커서 / 글꼴** — WhiteSur 아이콘, WhiteSur-cursors, Inter + Noto Sans CJK
- **창 장식 전환** — `maclinux-deco klassy` 로 Klassy(모서리 반경 조절 가능)로 변경

**작업 관리자 (Windows 11 스타일)**
- 왼쪽 아이콘 레일: **프로세스 / 성능 / 앱 기록 / 시작 프로그램 / 사용자 / 자세히 / 서비스**
- **프로세스** — 앱 단위 그룹(펼침 가능), 시스템 데몬은 「系统进程」으로 묶음, 행마다 앱 아이콘, **CPU 히트 컬러**(초록→노랑→빨강), 검색·정렬, 오른쪽 클릭 메뉴(작업 끝내기 / 프로세스 트리 끝내기)
- **작업 끝내기 = 최고 권한** — pkexec → root 헬퍼 → **SIGKILL**. 어떤 프로세스도 거부할 수 없습니다. 활성 세션에서는 **암호 불필요**(polkit 규칙)
- **성능** — CPU / 메모리 / 디스크 / 네트워크 목록, 그리드 그래프, 사용률 / 속도 / 프로세스 / 스레드 / 가동 시간
- **기타** — 앱 기록(세션 누적 CPU), 시작 프로그램 사용/중지, 세션 로그아웃, 서비스 시작/중지/재시작

### 내장 명령
| 명령 | 용도 |
|---|---|
| `maclinux-taskmgr` | 작업 관리자(Dock 에도 아이콘) |
| `maclinux-doctor` | **원샷 자가 점검**: 버전, Dock, 런처, 구성 요소, 로그 끝부분 |
| `maclinux-deco aurorae\|klassy` | 창 장식 전환 |
| `maclinux-preview-login` | 세션 안에서 로그인 화면 미리보기 |
| `maclinux-hello` / `maclinux-welcome` | hello 애니메이션 / 환영 마법사 재생 |
| 로그 | `~/.config/maclinux/apply-desktop.log` |

### 알려진 제한
- Live 이미지이므로 **디스크 설치용 커스텀 마법사는 없습니다**(OEM install 항목은 원본 그대로)
- 「디스크 / 네트워크」 열은 **다른 사용자의 프로세스**에서 `—` 로 표시(커널 제한)
- 「앱 기록」은 **세션 누적**이며 영구 저장되지 않습니다
- 동영상 배경화면은 CPU/GPU 를 사용합니다. 3D 가속이 없으면 정적 배경화면을 권장
- VMware 에서만 검증했습니다. 실제 하드웨어 USB 부팅은 직접 확인하세요

### 문제 해결
Dock 이 없거나 배경화면이 멈춰 있거나 블러가 없으면 터미널에서:
```
maclinux-doctor
```
ISO 식별 정보, Dock 프로세스, 런처 목록, 구성 요소 존재 여부, 미화 로그 끝부분을 출력합니다. 그대로 공유해 주세요.

### 라이선스 및 감사
- **본 프로젝트의 원본 부분**(빌드 파이프라인, 작업 관리자, 애니메이션/마법사, 동영상 배경화면 플러그인, 각 스크립트): **CC BY-NC-SA 4.0**
- **서드파티**(각 저작자의 라이선스를 따름): Kubuntu 24.04 / KDE Plasma 5.27 / Latte Dock / WhiteSur-kde · WhiteSur SDDM 테마(vinceliuice) / Klassy / NASA 항공 촬영 소재(퍼블릭 도메인)
- Apple 공식 리소스는 포함하지 않습니다. macOS 스타일 소재는 개인적 사용을 위한 커뮤니티 재현물입니다

---

## Deutsch

### Was ist das
**maclinux 1.0** ist ein bootfähiges **Live-Remaster im macOS-Look**, aufgebaut auf **Kubuntu 24.04.5 LTS** (KDE Plasma 5.27 / X11). Es überträgt die macOS-Optik und -Bedienung als zusammenhängendes Paket: Dock, Ampel-Knöpfe, Milchglas-Blur, ruhige Animationen, lebendiges Video-Wallpaper, Video-Anmeldebildschirm — plus einen integrierten **Task-Manager im Windows-11-Stil**.

Es ist ein **Live-Image**: im VM einbinden oder auf USB schreiben — **keine Installation auf die Festplatte nötig**.

### Eckdaten
| Punkt | Wert |
|---|---|
| Version | maclinux 1.0 |
| Basis | Kubuntu 24.04.5 LTS (Plasma 5.27 / X11) |
| Image-Größe | 5.656.215.552 Bytes (5,27 GB) |
| Build-Stempel | 2026-10-18 09:42 UTC (im Image: `cat /usr/share/maclinux/VERSION`) |
| SHA-256 (gesamt) | `824da302e0ccd631cc271fe55c43b112ad9dbf5a70e62f936570d6da9eae43f3` |
| Teile | 4 Teile à 1,5 GB (1.500.000.000 Bytes): `.001` `.002` `.003` `.004` |

### Teile zusammenfügen
Die Teile sind ein **reiner Byte-Split** — **in Reihenfolge** zusammenfügen; das Ergebnis muss exakt 5.656.215.552 Bytes groß sein.

**Windows (CMD)**
```
copy /b maclinux-1.0.iso.001+maclinux-1.0.iso.002+maclinux-1.0.iso.003+maclinux-1.0.iso.004 maclinux-1.0.iso
```
(In PowerShell: `cmd /c copy /b ...`)

**7-Zip** — `maclinux-1.0.iso.001` markieren → Rechtsklick → 7-Zip → „Hier entpacken"

**Linux / macOS**
```
cat maclinux-1.0.iso.0* > maclinux-1.0.iso
```

**Prüfen (Windows)**
```
certutil -hashfile maclinux-1.0.iso SHA256
```
Muss mit dem Gesamt-SHA-256 oben übereinstimmen. SHA-256 je Teil:

| Teil | Größe (Bytes) | SHA-256 |
|---|---|---|
| `maclinux-1.0.iso.001` | 1.500.000.000 | `{{P1_SHA256}}` |
| `maclinux-1.0.iso.002` | 1.500.000.000 | `{{P2_SHA256}}` |
| `maclinux-1.0.iso.003` | 1.500.000.000 | `{{P3_SHA256}}` |
| `maclinux-1.0.iso.004` | 1.156.215.552 | `{{P4_SHA256}}` |

### Starten
- **Virtuelle Maschine (getestet)** — VMware: VM als Linux / Ubuntu 64-Bit anlegen, CD/DVD auf das zusammengefügte ISO zeigen, einschalten. Empfohlen: **4 GB+ RAM, 2–4 vCPUs**; für flüssigen Blur/Animationen **3D-Beschleunigung** aktivieren (open-vm-tools ist vorinstalliert). **Vor jedem Test die VM vollständig herunterfahren — keine alten Snapshots fortsetzen.**
- **USB-Stick** — mit **Rufus (DD-Modus)** oder **balenaEtcher** schreiben; BIOS und UEFI werden unterstützt.
- **Bootmenü** — GRUB startet nach 5 s automatisch „**maclinux (Live 桌面)**"; bei Grafikproblemen „**Kubuntu (safe graphics)**" (`nomodeset`) wählen.
- **Anmeldung** — die Live-Sitzung meldet sich automatisch an; der macOS-artige Anmeldebildschirm (WhiteSur-Theme + Video-Hintergrund) erscheint beim Abmelden oder Sperren.

### Erster Start
Etwa 4 Sekunden nach der Anmeldung: macOS-Verschönerung läuft im Hintergrund, die Hello-Animation spielt (weißer Grund, schwarze Schrift, Schleife; beliebige Taste/Klick überspringt), danach der Willkommens-Assistent.

> Im Live-Modus liegt das Home-Verzeichnis im RAM — das Erlebnis wiederholt sich bei **jedem Start**; die Verschönerung wird bei jeder Anmeldung neu angewendet.

### Funktionen
**Optik & Bedienung**
- **Dock** — Latte Dock unten: **kein Hover-Zoom**, Milchglas-Transluzenz, hüpfende Icons beim Start; Launcher: Dolphin, **Konsole**, **Systemeinstellungen**, **Task-Manager**, KWrite, Gwenview, Ark, Firefox; rechts **Papierkorb**
- **Ampel-Knöpfe** — WhiteSur-Original (drei farbige Punkte immer sichtbar, Symbole beim Hover), links angeordnet, abgerundete Fenster
- **Blur** — KWin-Blur aktiv (Stärke 4 / Rauschen 0)
- **Animationen** — globaler Dauerfaktor 2.0 (langsamer, ruhiger)
- **Video-Wallpaper** — Video liegt auf der **untersten Ebene des Desktops** und geht nach der Anmeldung vom „Fließen" langsam ins Standbild über (3 NASA-Aufnahmen)
- **Statische Wallpaper** — Monterey / Sonoma / Ventura / WhiteSur, hell+dunkel, insgesamt 8
- **Anmeldebildschirm** — SDDM-Theme WhiteSur-dark mit Video-Hintergrund
- **Icons / Cursor / Schriften** — WhiteSur-Icons, WhiteSur-cursors, Inter + Noto Sans CJK
- **Umschaltbare Dekoration** — `maclinux-deco klassy` wechselt zu Klassy (einstellbare Eckenradien)

**Task-Manager (Windows-11-Stil)**
- Icon-Leiste links: **Prozesse / Leistung / App-Verlauf / Autostart / Benutzer / Details / Dienste**
- **Prozesse** — aufklappbare App-Gruppen, Systemdienste unter „系统进程", App-Icons pro Zeile, **CPU-Hitzefarben** (grün→gelb→rot), Suche & Sortierung, Kontextmenü (Task beenden / Prozessbaum beenden)
- **Task beenden = höchste Rechte** — pkexec → Root-Helfer → **SIGKILL**; kein Prozess kann sich weigern. In aktiven Sitzungen **ohne Passwort** (polkit-Regel)
- **Leistung** — CPU / Speicher / Datenträger / Netzwerk, Rasterdiagramme, Auslastung / Geschwindigkeit / Prozesse / Threads / Laufzeit
- **Sonstiges** — App-Verlauf (sitzungs-kumulierte CPU), Autostart ein/aus, Sitzung abmelden, Dienste starten/stoppen/neu starten

### Integrierte Befehle
| Befehl | Zweck |
|---|---|
| `maclinux-taskmgr` | Task-Manager (auch im Dock) |
| `maclinux-doctor` | **Selbsttest in einem Schritt**: Version, Dock, Launcher, Komponenten, Log-Ende |
| `maclinux-deco aurorae\|klassy` | Fensterdekoration wechseln |
| `maclinux-preview-login` | Anmeldebildschirm in der Sitzung ansehen |
| `maclinux-hello` / `maclinux-welcome` | Hello-Animation / Willkommens-Assistent erneut zeigen |
| Log | `~/.config/maclinux/apply-desktop.log` |

### Bekannte Einschränkungen
- Live-Image: **kein angepasster „Installation auf Festplatte"-Assistent** (der OEM-Eintrag ist unverändert)
- Spalten „Datenträger / Netzwerk" zeigen `—` für Prozesse, die **nicht dem eigenen Benutzer gehören** (Kernel-Beschränkung)
- „App-Verlauf" ist **pro Sitzung kumuliert**, nicht dauerhaft
- Video-Wallpaper kostet CPU/GPU; ohne 3D-Beschleunigung besser statisches Wallpaper nutzen
- Nur unter VMware getestet; USB-Boot auf echter Hardware bitte selbst prüfen

### Fehlersuche
Fehlt das Dock, steht das Wallpaper, fehlt der Blur — im Terminal:
```
maclinux-doctor
```
Es zeigt ISO-Identität, Dock-Prozess, Launcher-Liste, Komponenten und das Ende des Verschönerungs-Logs. Diese Ausgabe bitte teilen.

### Lizenz & Danksagung
- **Eigene Teile dieses Projekts** (Build-Pipeline, Task-Manager, Animation/Assistent, Video-Wallpaper-Plugin, Skripte): **CC BY-NC-SA 4.0**
- **Drittanbieter** (jeweils eigene Lizenz): Kubuntu 24.04 / KDE Plasma 5.27 / Latte Dock / WhiteSur-kde & WhiteSur-SDDM-Themes (vinceliuice) / Klassy / NASA-Luftaufnahmen (Public Domain)
- Es sind keine Apple-Assets enthalten; alle macOS-artigen Assets sind Community-Nachbauten für den privaten Gebrauch
