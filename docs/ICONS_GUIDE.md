# Fyne 图标库集成指南

本指南介绍如何在 Fyne 应用中引入流行图标库的图标。

## 推荐的图标库

### 1. **Material Icons** (Google)
- 网站: https://fonts.google.com/icons
- 格式: SVG, PNG
- 特点: 图标丰富，风格统一
- 下载: 点击图标 → 下载 SVG

### 2. **Heroicons** (Tailwind)
- 网站: https://heroicons.com/
- 格式: SVG (Outline/Solid)
- 特点: 简洁现代，适合 UI
- 下载: 点击图标 → Copy SVG → 保存为 .svg 文件

### 3. **Lucide Icons**
- 网站: https://lucide.dev/
- 格式: SVG
- 特点: 开源，图标精美
- 下载: 点击图标 → Download SVG

### 4. **Font Awesome** (需要转换)
- 网站: https://fontawesome.com/
- 格式: 字体文件，需要转换为 SVG
- 工具: https://fontawesome.com/icons (搜索图标 → 下载 SVG)

## 集成步骤

### 步骤 1: 下载图标

1. 访问图标库网站
2. 搜索需要的图标（如 "trash", "filter", "refresh"）
3. 下载 SVG 格式（推荐）或 PNG 格式

### 步骤 2: 放置图标文件

将下载的图标文件放入 `assets/icons/` 目录：

```
assets/
  icons/
    trash.svg
    filter.svg
    refresh.svg
    clear-all.svg
```

### 步骤 3: 嵌入图标

在 `assets/icons.go` 中使用 `//go:embed` 嵌入图标：

```go
package assets

import (
    _ "embed"
    "fyne.io/fyne/v2"
    "fyne.io/fyne/v2/theme"
)

//go:embed icons/trash.svg
var trashIconSVG []byte

var TrashIcon = fyne.NewStaticResource("trash.svg", trashIconSVG)

// 支持主题变色（仅 SVG）
var ThemedTrashIcon = theme.NewThemedResource(TrashIcon)
```

### 步骤 4: 在代码中使用

```go
import "github.com/hankmor/vdd/assets"

// 使用支持主题的图标
clearBtn := widgets.NewButtonWithTooltip("", assets.ThemedTrashIcon, func() {
    // ...
}, "清除")
```

## SVG vs PNG

### SVG 图标（推荐）
- ✅ 支持主题自动变色（亮色/暗色）
- ✅ 矢量图，任意缩放不失真
- ✅ 文件小
- ❌ 需要确保 SVG 格式正确

### PNG 图标
- ✅ 简单直接
- ✅ 兼容性好
- ❌ 不支持主题变色
- ❌ 需要准备多个尺寸

## 图标命名建议

根据功能命名图标：
- `trash.svg` - 删除/清除
- `filter.svg` - 筛选/过滤
- `refresh.svg` - 刷新/重置
- `clear-all.svg` - 清除所有
- `delete.svg` - 删除
- `cancel.svg` - 取消

## 完整示例

### 1. 下载图标
从 Heroicons 下载 "trash" 图标，保存为 `assets/icons/trash.svg`

### 2. 嵌入资源
```go
// assets/icons.go
package assets

import (
    _ "embed"
    "fyne.io/fyne/v2"
    "fyne.io/fyne/v2/theme"
)

//go:embed icons/trash.svg
var trashIconSVG []byte

var TrashIcon = fyne.NewStaticResource("trash.svg", trashIconSVG)
var ThemedTrashIcon = theme.NewThemedResource(TrashIcon)
```

### 3. 使用图标
```go
// ui/views/history.go
import "github.com/hankmor/vdd/assets"

clearBtn := widgets.NewButtonWithTooltip("", assets.ThemedTrashIcon, func() {
    // 清除逻辑
}, "清除所有")
```

## 注意事项

1. **SVG 格式**: 确保 SVG 文件格式正确，Fyne 支持标准 SVG
2. **文件大小**: 建议图标文件 < 50KB
3. **主题支持**: 只有 SVG 图标可以使用 `theme.NewThemedResource` 支持主题变色
4. **图标尺寸**: Fyne 会自动缩放图标，建议使用 24x24 或 48x48 的图标

## 快速获取图标

### 使用命令行工具（可选）

```bash
# 安装 iconify-cli (需要 Node.js)
npm install -g @iconify/cli

# 下载 Material Icons
iconify download material-symbols:delete --output assets/icons/ --format svg
iconify download material-symbols:filter --output assets/icons/ --format svg
```

## 参考资源

- [Fyne 资源文档](https://developer.fyne.io/tutorial/bundling)
- [Material Icons](https://fonts.google.com/icons)
- [Heroicons](https://heroicons.com/)
- [Lucide Icons](https://lucide.dev/)

