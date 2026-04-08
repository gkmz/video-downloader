# VDD 视频下载工具 - 任务清单

## 规划阶段

- [x] 创建需求文档
- [x] 创建技术设计文档
- [x] 创建开发计划
- [x] 用户评审和确认

## 开发阶段

- [x] 基础框架搭建
  - [x] 初始化 Go 项目结构
  - [x] 引入 Fyne 框架
  - [x] 集成 yt-dlp
  - [x] 集成 ffmpeg
- [x] 核心功能实现
  - [x] 视频链接解析
  - [x] 格式列表展示（响应式表格）
  - [x] 智能推荐算法
  - [x] 下载管理器
  - [x] 进度追踪
- [/] 界面开发
  - [x] 主界面设计
  - [x] Configure Management
  - [x] Create `core/config` module
  - [x] Define Config struct
  - [x] Implement Load/Save
  - [x] 下载历史界面
  - [x] 数据持久化 (SQLite)
    - [x] 初始化 `core/db` 模块
    - [x] 迁移 config 到 SQLite
    - [x] 迁移 history 到 SQLite
- [x] 高级功能
  - [x] 代理设置
  - [x] 字幕下载
  - [x] Cookie 导入
- [x] 开源化调整
  - [x] 移除授权与激活逻辑
  - [x] 移除 License Server
  - [x] 清理打包构建产物与敏感配置

## 验证阶段 (V1.0)

- [x] 功能测试
- [x] 跨平台测试（Windows/Linux/macOS）
- [x] 性能优化
- [x] 打包和分发

## V1.2

- [x] 集成日志框架，记录日志
- [x] 优化youtube视频下载
- [x] 支持4K、8K视频下载
- [x] 支持暂停、继续、取消下载
- [x] 优化解析列表，只显示视频，下载时一并处理音频
- [x] 界面优化，
- [x] 新增任务列表, 支持批量下载
- [x] 界面重构
  - [x] 基础封面显示 (Thumbnail)
  - [x] 启动欢迎页 (Hero Empty State)
  - [x] 增加多种主题风格

## V1.3

- [x] **Cookie 管理优化 (Final Design)**
  - [x] **全局设置**: 增加 "优先使用浏览器 Cookie" 开关 (默认开启)
    - [x] 支持选择浏览器 (Chrome/Edge/Firefox)
  - [x] **主界面交互 (当浏览器模式关闭或需覆盖时)**
    - [x] 解析栏增加 "使用 Cookie 文件" 复选框
    - [x] 勾选后弹出文件选择器 (支持记忆上次使用的文件)
  - [x] **Core**: 解析和下载逻辑适配新的参数传递方式
- [x] 队列管理
  - [x] 下载队列 (加入队列/开始/暂停/删除)
  - [x] 并发任务调度优化

## V1.4

- [x] 批量下载增强
  - [x] 批量下载
  - [x] 播放列表 (Playlist) 解析与下载
  - [x] 频道 (Channel) 解析与下载

## 规划阶段

- [ ] **安全性修复 (Critical)**
  - [ ] 日志脱敏: 防止 `yt-dlp` 输出中的敏感信息写入日志
- [ ] 批量下载增强
  - [ ] 批量链接一次性导入
- [ ] 核心架构重构
  - [ ] 状态机重构: 优化 `Downloader` 状态管理，避免 Race Condition
  - [ ] 错误处理标准化: 统一 Error 类型和 UI 反馈
- [ ] 音频提取与转换
  - [ ] "仅音频 (MP3)" 模式
  - [ ] 自动转换 m4a/webm 为 mp3化
- [ ] 浏览器扩展助手
  - [ ] Chrome/Edge 插件开发
  - [ ] 网页嗅探与一键发送到 VDD
- [ ] 国际化 (i18n)
  - [ ] 多语言支持架构
  - [ ] 英文界面翻译
- [ ] 界面重构 (UI 2.0)
  - [ ] 卡片式布局 (Card Layout 替换表格)
  - [ ] 交互动效 (Fade/Slide)
  - [ ] 自定义字体集成 (如 Inter/Harmony)
