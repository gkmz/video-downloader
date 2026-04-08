# 通知点击行为说明

## 问题描述
在 macOS 上，点击下载完成通知后，会打开"脚本编辑器"的对话框，而不是返回到应用程序。

## 原因分析

这是 Fyne 框架在 macOS 上的已知限制，原因是：

1. **应用未正确打包/签名**
   - macOS 通知系统要求应用必须是正确打包的 `.app` bundle
   - 直接运行编译的二进制文件（如 `./vdd`）不会被视为正式应用
   - macOS 会将未打包的可执行文件当作 "script" 处理

2. **Fyne 框架限制**
   - Fyne 的 `SendNotification()` API 目前不支持通知点击回调
   - 无法自定义点击通知后的行为
   - 这是 Fyne 团队正在讨论的功能增强

## 解决方案

### 方案1：正式打包应用（推荐生产环境）

```bash
# 使用 fyne-cross 打包 macOS 应用
fyne package -os darwin -icon assets/icon.png

# 或使用 fyne install 安装到系统
fyne install

# 从 Applications 文件夹启动
open /Applications/VDD.app
```

打包后的应用需要：
- Apple Developer Account 签名（可选，但推荐）
- 公证（Notarization）以避免 Gatekeeper 警告

### 方案2：开发环境下禁用通知点击（当前采用）

对于开发阶段，保持当前通知方式，接受点击通知会打开脚本编辑器的行为。

### 方案3：等待 Fyne 框架支持

Fyne 社区正在讨论添加通知回调功能，未来可能支持：
- 点击通知时的自定义回调
- Deep linking 支持
- 通知 Action 按钮

## 当前状态

**开发环境：**
- ✅ 通知正常显示
- ❌ 点击通知会打开脚本编辑器（Fyne 框架限制）

**生产环境（打包后）：**
- ✅ 通知正常显示
- ⚠️ 点击通知行为取决于是否签名
  - 已签名：正常激活应用窗口
  - 未签名：可能仍显示脚本编辑器

## 建议

对于正式发布：
1. 使用 `fyne package` 打包应用
2. 申请 Apple Developer Program 并签名应用
3. 进行 Notarization 公证
4. 通过 DMG/PKG 分发应用

对于开发调试：
- 接受当前行为
- 通知主要用于提醒，不依赖点击交互
