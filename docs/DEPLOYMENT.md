# 部署说明

## 部署说明

### 3.4 准备二进制依赖

VDD 依赖 `yt-dlp`。请将其下载并放置在对应平台的 `assets` 目录下：

```
assets/
└── [macos|windows|linux]/
    └── yt-dlp (或 yt-dlp.exe)
```

> **注意**：FFmpeg 不再直接打包进 VDD。
>
> - VDD 会优先使用用户在设置中配置的 FFmpeg 路径。
> - 如果未配置，尝试使用系统 PATH 中的 FFmpeg。
> - 用户需自行安装 FFmpeg 以获得完整的音视频合并功能。

### 1. 下载 yt-dlp

#### macOS / Linux

```bash
# 下载 yt-dlp
curl -L https://github.com/yt-dlp/yt-dlp/releases/latest/download/yt-dlp -o assets/bundled/yt-dlp

# 添加执行权限
chmod +x assets/bundled/yt-dlp

# 验证版本
./assets/bundled/yt-dlp --version
```

#### Windows (PowerShell)

```powershell
# 下载 yt-dlp
Invoke-WebRequest -Uri "https://github.com/yt-dlp/yt-dlp/releases/latest/download/yt-dlp.exe" -OutFile "assets/bundled/yt-dlp.exe"

# 验证版本
.\assets\bundled\yt-dlp.exe --version
```

### 2. 下载 ffmpeg

#### macOS

```bash
# 使用 Homebrew 安装
brew install ffmpeg

# 复制到项目（可选，用于打包）
cp $(which ffmpeg) assets/bundled/ffmpeg
```

#### Linux (Ubuntu/Debian)

```bash
# 安装 ffmpeg
sudo apt update
sudo apt install ffmpeg

# 复制到项目（可选，用于打包）
cp $(which ffmpeg) assets/bundled/ffmpeg
```

#### Windows

1. 访问 https://ffmpeg.org/download.html
2. 下载 Windows 版本
3. 解压并将 `ffmpeg.exe` 复制到 `assets/bundled/` 目录

### 3. 验证工具

```bash
# 验证 yt-dlp
./assets/bundled/yt-dlp --version

# 验证 ffmpeg
./assets/bundled/ffmpeg -version
```

## 运行应用

### 开发环境运行

```bash
# 运行应用
go run main.go
```

### 编译可执行文件

```bash
# 编译
go build -o vdd main.go

# 运行
./vdd
```

### 使用 Fyne 打包

```bash
# 安装 fyne 命令行工具
go install fyne.io/fyne/v2/cmd/fyne@latest

# 打包为应用
fyne package -os darwin -icon icon.png  # macOS
fyne package -os linux -icon icon.png   # Linux
fyne package -os windows -icon icon.png # Windows
```

## 注意事项

### yt-dlp 快速测试（系统安装版本）

如果您暂时没有下载 yt-dlp 到 `assets/bundled/` 目录，也可以先在系统中安装 yt-dlp 进行测试：

#### macOS / Linux

```bash
# 使用 pip 安装
pip install yt-dlp

# 或使用 Homebrew (macOS)
brew install yt-dlp

# 或直接下载
sudo wget https://github.com/yt-dlp/yt-dlp/releases/latest/download/yt-dlp -O /usr/local/bin/yt-dlp
sudo chmod +x /usr/local/bin/yt-dlp
```

#### Windows

```powershell
# 使用 winget
winget install yt-dlp

# 或使用 pip
pip install yt-dlp
```

程序会自动检测系统中的 yt-dlp，优先顺序为：

1. `assets/bundled/yt-dlp` （项目内置）
2. 系统 PATH 中的 `yt-dlp` （系统安装）

### 网络问题

如果下载 yt-dlp 或 ffmpeg 遇到网络问题，可以：

1. 使用代理
2. 手动访问 GitHub Releases 页面下载
3. 使用镜像站点

### 权限问题

Linux/macOS 用户请确保二进制文件有执行权限：

```bash
chmod +x assets/bundled/yt-dlp
chmod +x assets/bundled/ffmpeg
```

## 目录结构

正确配置后的项目结构应该是：

```
vdd/
├── assets/
│   └── bundled/
│       ├── yt-dlp       # macOS/Linux
│       ├── yt-dlp.exe   # Windows
│       ├── ffmpeg       # macOS/Linux
│       └── ffmpeg.exe   # Windows
├── core/
├── ui/
├── utils/
├── main.go
└── go.mod
```

## 快速开始测试

1. 确保已下载 yt-dlp（项目内置或系统安装）
2. 运行应用：`go run main.go`
3. 输入任意视频链接（如 YouTube），点击"解析"
4. 选择格式并下载

## 常见问题

### Q: 提示找不到 yt-dlp

A: 请检查：

- `assets/bundled/yt-dlp` 是否存在
- 是否有执行权限（Linux/macOS）
- 或系统 PATH 中是否安装了 yt-dlp

### Q: 下载失败提示网络错误

A: 可能是目标网站需要代理，后续版本将支持代理配置

### Q: 某些网站无法下载

A: yt-dlp 需要定期更新以支持最新的网站变化，请更新 yt-dlp：

```bash
./assets/bundled/yt-dlp -U
```
