# FFmpeg 配置说明

## 为什么需要 FFmpeg？

某些视频平台（如 YouTube）的高清视频（1080p+）音频和视频是**分离存储**的。要获得完整的视频，需要：

1. 下载视频流
2. 下载音频流
3. 使用 FFmpeg 将两者合并

## 下载方式

### macOS

#### 方式 1：使用 Homebrew（推荐）

```bash
# 安装 FFmpeg
brew install ffmpeg

# 运行下载脚本（将复制到项目中）
./build/download-ffmpeg.sh darwin
```

#### 方式 2：手动下载

访问 https://evermeet.cx/ffmpeg/ 下载预编译版本，放置到 `utils/bundled/ffmpeg`

### Linux

#### 自动下载（推荐）

```bash
# 下载静态编译版本
./build/download-ffmpeg.sh linux
```

这将从 https://johnvansickle.com/ffmpeg/ 下载静态编译的 FFmpeg。

#### 使用系统包管理器

```bash
# Ubuntu/Debian
sudo apt install ffmpeg

# 复制到项目
cp $(which ffmpeg) utils/bundled/ffmpeg
```

### Windows

#### 方式 1：手动下载（推荐）

1. 访问 https://www.gyan.dev/ffmpeg/builds/
2. 下载 `ffmpeg-release-essentials.zip`
3. 解压并复制 `ffmpeg.exe` 到 `utils/bundled/`

#### 方式 2：PowerShell 下载

```powershell
# 下载并解压
Invoke-WebRequest -Uri "https://www.gyan.dev/ffmpeg/builds/ffmpeg-release-essentials.zip" -OutFile ffmpeg.zip
Expand-Archive -Path ffmpeg.zip -DestinationPath .
Copy-Item ffmpeg-*/bin/ffmpeg.exe utils/bundled/
```

---

## 验证

```bash
# 检查 FFmpeg 是否存在
ls -lh utils/bundled/ffmpeg*

# 验证版本
./utils/bundled/ffmpeg -version
```

---

## 可选配置

### 如果不想嵌入 FFmpeg

如果您不想将 FFmpeg 嵌入到应用中（减小文件大小），可以：

1. **不下载 FFmpeg**：跳过上述步骤
2. **使用系统 FFmpeg**：应用会自动降级使用系统安装的 `ffmpeg`
3. **提示用户安装**：应用可以检测并提示用户安装 FFmpeg

### 降级行为

应用的 FFmpeg 查找优先级：

1. 嵌入版本（从临时目录提取）
2. 开发环境版本（`utils/bundled/ffmpeg`）
3. 系统安装版本（`ffmpeg` 命令）

---

## 文件大小对比

| 配置            | 可执行文件大小 |
| --------------- | -------------- |
| 仅 yt-dlp       | ~13 MB         |
| yt-dlp + FFmpeg | ~80-100 MB     |

> **注意**：FFmpeg 完整版约 50-70 MB，会显著增加应用大小。

---

## 常见问题

### Q: FFmpeg 下载失败怎么办？

A: 应用仍可运行，但无法合并音视频分离的格式。建议手动下载并放置到 `utils/bundled/`。

### Q: 可以使用精简版 FFmpeg 吗？

A: 可以！只需确保包含基本的编解码器（H.264、AAC）即可。

### Q: Windows 下载太慢？

A: 可以使用国内镜像或手动从其他来源下载。

---

## 推荐配置

### 开发环境

- 安装系统版 FFmpeg（`brew install ffmpeg` 或 `apt install ffmpeg`）
- 应用会自动使用系统版本

### 生产打包

- 下载并嵌入 FFmpeg 到 `utils/bundled/`
- 提供完整功能，无需用户配置

---

## 更新 FFmpeg

```bash
# macOS (Homebrew)
brew upgrade ffmpeg
./build/download-ffmpeg.sh darwin

# Linux
./build/download-ffmpeg.sh linux

# Windows
# 重新下载最新版本
```
