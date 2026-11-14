# Vibo

**看懂 AI 编程项目的进展。**

[English](README.md) · [下载最新体验版](https://github.com/Bryce12322/vibo/releases/tag/v0.9.1)

Vibo 把 Agent 上报的进展整理成可视化看板：项目要达成什么、还有哪些工作、检查结果如何，以及现在需要你处理什么。继续在 Codex 对话里开发，需要了解全貌时打开看板。

## 开始使用

**当前支持 macOS + Codex，需要 Node.js 22.13 或更新版本。**

1. [下载 vibo-local-v0.9.1.zip](https://github.com/Bryce12322/vibo/releases/download/v0.9.1/vibo-local-v0.9.1.zip)，解压。
2. 打开 **Install Vibo.command**；也可以把解压后的文件夹交给 Codex，让它安装其中的 Vibo Skill。当前安装文件尚未经过 Apple 签名或公证。
3. 在实际项目中开启一个新的 Codex 对话，说：

> 用 Vibo 跟踪这个项目，并打开看板。

接下来正常描述开发需求即可。启用后，Agent 会按规则在计划变化、开始工作、实现结束、检查结果或需要你操作时上报，不需要单独发送“同步进展”。如果未发现 Skill，开启新对话或重启 Codex，再用 `$track-project` 明确调用。

增加其他项目时，在那个项目自己的对话中启用 Vibo，左侧项目栏就会出现它。

## 能看到什么

- 按交付目标组织的工作，包括功能开发、部署、域名和上线准备。
- 待推进事项优先，已实现事项默认折叠。
- 只有明确需要你处理的事项才提醒，执行状态与关注原因分开。
- 检查证据和变更记录；AI 自检不会冒充人工验收。
- 同一台设备上的多个项目，以及中文、英文界面。

## 数据保存在本机

不需要 Vibo 账号、域名或云服务。本地服务仅监听 `127.0.0.1`，数据留在你的电脑。看板实时展示 Agent 已上报的变化，不扫描代码，也不监听所有聊天；自动上报依赖宿主正确加载和调用 Skill。

为兼容旧版，Skill 名称仍为 `track-project`，数据目录仍为 `~/Library/Application Support/Qingzhou/`。请勿公开其中的连接文件、数据库或备份。重新安装更新会保留项目记录。

## 遇到问题

在 Codex 中说“帮我检查 Vibo 是否正常”，或“帮我备份 Vibo 数据”。[反馈问题](https://github.com/Bryce12322/vibo/issues)时，请提供系统、Node.js 版本和可见报错，不要上传私人项目数据或连接文件。

当前是本地体验版，暂不包含 Windows 安装器、云同步、团队账号和 Token 用量统计。Release 安装包包含完整运行文件及 Skill，本仓库提供分发和使用说明。
