# Security Policy

## Supported Scope

VDD 当前维护分支为 `main`。安全修复优先在该分支处理。

## Report a Vulnerability

如果你发现了安全问题，请不要在公开 Issue 中直接披露细节。

请通过以下方式私下联系：
- Email: hankmo.x@gmail.com
- 主题建议：`[VDD Security] <简短问题描述>`

请尽量提供：
- 影响版本或 commit
- 复现步骤
- 预期影响范围
- 可能的修复建议（可选）

## Response Process

收到报告后，我们会尽快完成以下流程：

1. 确认报告是否可复现
2. 评估影响等级与受影响范围
3. 制定并验证修复方案
4. 发布修复与必要说明

## Disclosure Policy

- 在修复发布前，请避免公开披露可利用细节。
- 修复发布后，我们会根据实际情况发布安全说明。

## Out of Scope

以下通常不视为安全漏洞：
- 纯 UI 文案问题
- 不影响安全边界的崩溃
- 对第三方站点策略变化导致的解析失败

## Dependency Security

VDD 依赖 `yt-dlp`、`ffmpeg` 等外部组件。

建议使用者：
- 使用可信来源安装依赖
- 及时更新依赖版本
- 在受控环境中运行与验证
