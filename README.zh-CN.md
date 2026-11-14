# Vibo

**看懂 AI 编程项目的进展。**

[English](README.md) · [打开线上版](https://vibo.bryceyufeng.workers.dev) · [接入指南](CONNECT.md) · [本地版 0.9.1](https://github.com/Bryce12322/vibo/releases/tag/v0.9.1)

Vibo 将 Agent 上报的真实进展整理成可视化看板：项目要达成什么、还有哪些工作、现在需要你处理什么。继续在熟悉的编码工具里开发，需要了解全貌时打开看板。

## 用一句话开始

在实际项目的 Agent 对话中发送：

> 请按照 https://github.com/Bryce12322/vibo 的接入指南，为当前编码工具连接 Vibo 并加载持续汇报规则，引导我完成必要授权，然后跟踪当前项目、同步已有计划并打开看板，后续开发有实际进展时主动更新。

线上版无需安装本地 Vibo 服务或 Node.js。AI 会根据宿主能力完成接入，并引导你操作必要的授权；部分工具可能需要手动添加 MCP、开启新对话或重启，不能保证所有宿主都能完全自动安装。[给 Agent 的完整接入步骤](CONNECT.md)。

## 使用流程

1. 连接 Vibo 远程 MCP，并在浏览器确认授权；无需注册也能使用。
2. Agent 关联当前项目，根据已有上下文同步目标和事项。
3. 打开线上看板，查看待推进、已实现和需要你处理的内容。
4. 正常开发，Agent 按已加载的规则汇报实际进展，无需每次另发同步指令。

MCP 地址：`https://vibo.bryceyufeng.workers.dev/mcp`，使用 Streamable HTTP 与浏览器 OAuth 授权。宿主接入和持续汇报规则见 [CONNECT.md](CONNECT.md)。

## 能看到什么

- 按交付目标组织的功能开发、部署、域名、支付接入等工作。
- 待推进事项优先，已实现事项默认折叠。
- 明确需要你处理的事项，执行状态与关注原因分开。
- 检查证据和变更记录；AI 自检不会冒充人工验收。
- 多个项目，以及中文、英文界面。

## 数据与登录

可以免登录开始。线上版将进展记录保存在 Cloudflare；GitHub 登录可将体验项目关联到账号，在其他浏览器或设备继续访问。登录仅读取 GitHub 公开身份，不申请仓库权限。

访客访问依赖当前浏览器或仍有效的 Agent 连接。更换设备前可登录关联账号；未关联账号且有效连接也丢失时，无法保证找回记录。原有本地记录只有在你主动选择导出文件并导入时才会上传。

Vibo 展示 Agent 实际上报的信息，不扫描源代码，也不监听其他对话。持续汇报依赖编码工具正确加载和执行规则。

## 当前验证范围

线上版为 **0.10.0-preview**。已验证：

- 正式 HTTPS 服务的浏览器授权和官方 MCP 客户端全部 7 个工具的发现。
- 项目、目标、任务创建，进展上报与页面无刷新更新。
- 真实 GitHub 登录后保留访客项目编号、事项状态及历史。
- 两个独立浏览器会话登录后恢复同一项目；该测试在同一电脑上进行。
- 52 项自动检查通过。

**仍待验证：** Codex、Cursor、Claude Code 各宿主的原生接入、跨对话规则加载和持续自动汇报；线上负载与备份恢复演练。接入指南提供操作约定，不表示所有工具已经通过完整验收。当前适合小范围试用，不宣称正式稳定版。

## 本地版：macOS + Codex

需要 Node.js 22.13 或更新版本。希望数据留在本机的用户可以继续使用 **0.9.1 本地版**。

<details>
<summary>让 Codex 安装本地版</summary>

在 Codex 中发送：

> 请按 https://github.com/Bryce12322/vibo/blob/main/INSTALL.md 的本地版步骤，帮我下载、校验、解压并安装 Vibo 0.9.1 本地 Skill。

完整发行包：[vibo-local-v0.9.1.zip](https://github.com/Bryce12322/vibo/releases/download/v0.9.1/vibo-local-v0.9.1.zip)。不要选择 GitHub 自动生成的 Source code ZIP，也不要把本仓库根目录当作 Skill 安装。[完整安装步骤与校验信息](INSTALL.md)。

安装后，在实际项目对话中说“用 Vibo 跟踪这个项目，并打开看板”。宿主尚未发现 Skill 时，开启新对话或重启后再试，也可以明确调用 `$track-project`。

为兼容旧版，Skill 名称为 `track-project`，数据目录仍为 `~/Library/Application Support/Qingzhou/`。本地服务仅监听 `127.0.0.1`；安装更新会保留项目记录。安装器尚未经过 Apple 签名或公证。

</details>

## 反馈问题

[提交反馈](https://github.com/Bryce12322/vibo/issues)时，注明线上版或本地版、编码工具及版本、系统和可见报错；使用本地版时补充 Node.js 版本。不要公开验证码、连接凭据、私人项目记录或完整对话。

本仓库提供接入、分发及使用说明；本地 Release 包含完整运行文件与 Skill。团队协作和 Token 用量统计暂未提供。
