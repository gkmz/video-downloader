# 构建和打包指南

## 快速开始

本项目使用统一的构建脚本 `build/build-cross.sh` 来管理多平台构建。

### 依赖要求

- Go 1.21+
- Git
- Docker (用于 Windows/Linux 交叉编译)

### 构建命令

```bash
# 构建所有平台 (推荐)
./build/build-cross.sh all

# 仅构建 macOS (本地构建)
./build/build-cross.sh macos

# 仅构建 Windows (使用 Docker + fyne-cross)
./build/build-cross.sh windows

# 仅构建 Linux (使用 Docker + fyne-cross)
./build/build-cross.sh linux
```

## 构建产物

构建完成后，产物会输出到：

- **临时构建目录**: `build/output/`
- **最终发布包**: `build/dist/`

发布包示例：

- `vdd-v1.0.1-macos.zip`
- `vdd-v1.0.1-windows-amd64.zip`
- `vdd-v1.0.1-linux-amd64.tar.xz`

## 自动化特性

### 1. 版本管理

构建脚本会自动从 `ui/about_window.go` 读取 `AppVersion` 常量作为构建版本号。
**无需手动修改脚本中的版本变量。**

### 2. 依赖管理

脚本会自动下载以下依赖的二进制文件：

- **yt-dlp**: 自动下载对应平台的最新 Release。
- **ffmpeg**: 自动下载并解压对应平台的构建版。

### 3. 图标处理

脚本会自动使用 `assets/icon.png` 打包应用图标。
对于 macOS，代码中已通过 `embed` 嵌入图标以修复托盘显示问题。

## 常见问题

### Q: 为什么 Windows/Linux 构建需要 Docker?

A: 我们使用 `fyne-cross` 工具进行交叉编译，它依赖 Docker 容器来提供 Linux/Windows 的编译环境（CGO 依赖）。

### Q: macOS 构建失败?

A: macOS 构建直接使用本地环境。请确保已安装 `fyne` 命令行工具：

```bash
go install fyne.io/fyne/v2/cmd/fyne@latest
```

## 发布流程

详细的发布流程请参考 [发布指南](RELEASE_GUIDE.md)。
