# VDD 版本发布指南

本文档描述了 VDD 项目的版本发布流程。

## 核心原则

**Single Source of Truth (唯一真实数据源)**:  
`ui/about_window.go` 中的 `AppVersion` 常量是项目的唯一版本号来源。

```go
// ui/about_window.go
const (
	AppVersion = "v1.0.1" // 修改这里来更新版本
    // ...
)
```

构建脚本会自动读取该值来命名构建产物。

## 发布流程

### 1. 更新版本号

在发布新版本前，修改 `ui/about_window.go`:

1. 打开 `ui/about_window.go`
2. 修改 `AppVersion` 为新版本号 (例如 `v1.0.2`)
3. 提交代码: `git commit -am "chore: bump version to v1.0.2"`

### 2. 本地构建 (可选验证)

运行构建脚本以验证构建是否正常，并生成发布包。

```bash
# 构建所有平台
./build/build-cross.sh all
```

产物位于 `build/dist/` 目录下，例如：

- `vdd-v1.0.2-windows-amd64.zip`
- `vdd-v1.0.2-linux-amd64.tar.xz`
- `vdd-v1.0.2-macos.zip`

### 3. 创建 GitHub Release

项目的更新检测机制依赖 GitHub Releases。

1. **Push 代码**: 确保本地修改已推送。
2. **打 Tag**: git tag 必须与 `AppVersion` 完全一致。
   ```bash
   git tag v1.0.2
   git push origin v1.0.2
   ```
3. **Draft Release**: 在 GitHub 仓库页面创建新 Release。
   - **Tag version**: 选择 `v1.0.2`
   - **Title**: `v1.0.2` (或带有代号的标题)
   - **Description**: 填写更新日志。
4. **上传附件**: 将 `build/dist/` 下的构建产物上传到 Release Assets。
5. **Publish**: 发布 Release。

## 注意事项

- **Tag 一致性**: 必须确保 `ui/about_window.go` 中的版本号与 git tag 一致，否则自动更新检测可能会报告版本不匹配或混淆。
- **更新检测**: 客户端会对比本地 `AppVersion` 和 GitHub Latest Release 的 tag。如果不一致 (且 latest 不是更旧的版本)，就会提示更新。
