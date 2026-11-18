# 安装 Vibo / Install Vibo

默认安装 **0.9.2 本地体验版**，使用 Skill＋CLI。macOS，需要 Node.js 22.13+。无需配置 MCP 连接器或 OAuth。明确选择线上版或已有 mode:cloud 关联时，按 [线上说明](CONNECT.md#online)处理。

> 请根据本指南自动下载、校验、解压并安装 Vibo 本地版，按当前宿主选择技能目录，读取规则后跟踪当前项目，优先在内置浏览器打开看板。

## Agent 执行步骤

1. 识别实际宿主、项目目录和已有 .vibo/project.json。已有 cloud 关联继续保留，不能自动重复创建本地项目。
2. 检查 macOS 和 Node.js 22.13+。WorkBuddy 的自带版本由 ~/.workbuddy/binaries/node/versions/current 文件指定，实际 Node 位于该版本目录的 bin/node。核对后使用。缺少运行环境时给出具体原因。
3. 下载下面两个文件到临时目录。按固定 SHA256 和校验文件检查包，通过后解压。仓库根目录及自动 Source code ZIP 不含完整运行包。
4. 解压目录为 qingzhou-local。Codex 执行 bash "qingzhou-local/Install Vibo.command" --host codex，WorkBuddy 传 --host workbuddy。也可用已确认的 Node 执行同目录 install.mjs --host <宿主>。
5. 安装器返回 skill_path、cli_path、node_path。默认 Codex ~/.agents/skills/track-project，WorkBuddy ~/.workbuddy/skills/track-project。仅在确认宿主实际目录不同时用 FLOW_SKILL_DIR 覆盖。升级备份旧 Skill。
6. 立即读取安装后的 SKILL.md 并使用同一 CLI。仅安装时 --help 即可验证。用户已要求跟踪时，context → connect → submit 保存当前计划 → open --open-link → 内置浏览器。
7. 核对每步结果。首次先展示当前计划，不要求扫描整个仓库、导入全部历史或运行项目测试。宿主未发现 Skill 时可直接读取其完整路径执行当前流程，后续自动触发仍需宿主加载规则。
8. 启用后通过宿主支持的项目规则引用 Skill，限定当前项目。持续报告在正常开发中主动进行，新对话恢复同一项目。

## 下载与校验 / Downloads

- [vibo-local-v0.9.2.zip](https://github.com/Bryce12322/vibo/releases/download/v0.9.2/vibo-local-v0.9.2.zip)
- [SHA256SUMS.txt](https://github.com/Bryce12322/vibo/releases/download/v0.9.2/SHA256SUMS.txt)

Expected SHA256
`45eeeefd8c1d6b6244253e3cf42ca9b162f6fc6839fa9540681694e5a7a5a491`

校验失败时停止。安装器未做 Apple 签名或公证，按系统正常权限流程操作。

## 验证范围

59 项自动测试通过，包括安装升级、稳定项目、批量提交、回滚、多项目隔离、检查和恢复。WorkBuddy 5.11.3 已在已安装技能页面实际发现并启用 track-project。多轮开发、跨对话报告及内置开页仍待真实宿主完整验收。

数据位于 ~/Library/Application Support/Qingzhou/，安装更新不需要读取或上传长期凭据。
