# 构建脚本同步更新说明

## 已更新的文件

### ✅ build/build.sh
- **更新内容**：
  - 添加 ffmpeg 下载逻辑（步骤 3）
  - 调用 `download-ffmpeg.sh` 自动下载
  - 支持 macOS/Linux/Windows

### ✅ build/build.bat  
- **更新内容**：
  - 添加 ffmpeg 下载提示（步骤 3）
  - 提供手动下载说明
  - 提供 PowerShell 自动下载命令
  - 更新步骤编号（4-7）

### ✅ build/build-all.sh
- **无需更新**：
  - 该脚本只是循环调用 `build.sh`
  - 已自动继承 `build.sh` 的所有更新
  - 每个平台都会自动下载对应的 yt-dlp 和 ffmpeg

---

## 构建流程对比

### build.sh（Unix/Linux）
```bash
1. 清理构建
2. 下载 yt-dlp
3. 下载 ffmpeg  ← 新增
4. 安装 fyne
5. 打包应用
6. 显示信息
```

### build.bat（Windows）
```batch
1. 清理构建
2. 下载 yt-dlp
3. 下载 ffmpeg  ← 新增
4. 检查 fyne
5. 打包应用
6. 移动产物
7. 显示信息
```

### build-all.sh（批量）
```bash
for platform in darwin linux windows; do
    ./build/build.sh $platform  # 自动调用，包含所有更新
done
```

---

## 使用示例

### 单平台构建

```bash
# macOS
./build/build.sh darwin

# Linux
./build/build.sh linux

# Windows (在 Windows 上)
build\build.bat
```

### 批量构建所有平台

```bash
./build/build-all.sh
```

**输出**：
```
build/output/
├── VDD.app                          # macOS (包含 yt-dlp + ffmpeg)
├── VDD.tar.xz                       # Linux (包含 yt-dlp + ffmpeg)
├── VDD.exe                          # Windows (包含 yt-dlp + ffmpeg)
├── vdd-0.1.0-macos.zip             # 发布包
├── vdd-0.1.0-linux-x64.tar.xz      # 发布包
└── vdd-0.1.0-windows-x64.zip       # 发布包
```

---

## ffmpeg 下载差异

### macOS/Linux（自动）
- 脚本自动调用 `download-ffmpeg.sh`
- 失败时提示但不中断构建

### Windows（手动）
- 由于 Windows 压缩包较大且结构复杂
- 提供详细的手动下载说明
- 提供 PowerShell 自动下载命令
- 允许跳过（运行时降级到系统 ffmpeg）

---

## 验证同步

所有三个脚本现在都包含：

| 功能 | build.sh | build.bat | build-all.sh |
|------|----------|-----------|--------------|
| 下载 yt-dlp | ✅ | ✅ | ✅（通过调用）|
| 下载 ffmpeg | ✅ | ✅ | ✅（通过调用）|
| 检查 fyne | ✅ | ✅ | ✅（通过调用）|
| 打包应用 | ✅ | ✅ | ✅（通过调用）|
| 创建发布包 | ❌ | ❌ | ✅ |

✅ **所有脚本已同步更新！**
