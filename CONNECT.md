# Vibo 接入指南 / Setup

默认采用本地 Skill＋CLI。先按 [INSTALL.md](INSTALL.md)安装完整 0.9.3 包，读取返回的 Skill，用现有命令执行能力保存计划并打开看板。

本地首次体验无需添加远程 MCP、信任连接器或 OAuth 授权。命令权限按宿主提示处理。已有 .vibo/project.json 的 mode 为 cloud 时保留原关联，用户明确选择迁移后再处理，不自动切换或双写。

## 本地标准流程

1. 检查已有安装和项目关联。
2. 读取安装后的 SKILL.md，context 恢复记录，再 connect 建立工作会话。
3. submit 一次保存目标、事项与实际事件，核对返回记录。
4. open --open-link 后优先内置浏览器开页。
5. 正常开发中增量汇报，新对话恢复相同项目。

出错执行一次 doctor，根据明确错误处理，避免反复授权或重启。首次先显示当前计划，历史按需迁移。

<a id="online"></a>
## 按需使用线上版 / Optional online

以下仅用于明确选择线上版的项目。已有线上关联继续保留，本地与云端没有自动双向同步。

WorkBuddy 线上接入目前在 OAuth 客户端注册阶段遇到回调兼容错误，授权页可能无法打开。该问题仍待修复，请用本地入口进行首次试用。

### Online configuration

This guide is for coding agents acting on the user's request to connect Vibo. This section applies only to explicit online use. Local 0.9.3 is the default onboarding route.

本指南供编码 Agent 执行用户的 Vibo 接入请求。此节只用于明确选择线上版时。默认体验请执行 [本地安装步骤](INSTALL.md)。不要将添加连接、加载规则和启用项目跟踪混为同一件事。

## Service / 服务信息

- Dashboard: https://vibo.bryceyufeng.workers.dev
- Remote MCP: https://vibo.bryceyufeng.workers.dev/mcp
- Transport: Streamable HTTP
- Authentication: browser OAuth with PKCE; a Vibo account is optional.
- Reporting rules: https://vibo.bryceyufeng.workers.dev/skill/SKILL.md

The online service does not require a local Vibo server, local database, Node.js, a GitHub repository clone, or the local ZIP package. The host's own requirements still apply. Do not ask the user to copy long-lived tokens into chat or project files.

线上版不要求本地 Vibo 服务、数据库、Node.js、克隆本仓库或下载旧版 ZIP。编码工具自身的运行要求仍需满足。长期凭据由宿主安全保管，不让用户发到对话，也不写入项目文件。

## Agent procedure / Agent 执行流程

1. **Identify the host and existing setup.** Check the current coding tool, supported configuration mechanism, and whether Vibo is already connected. Preserve other MCP servers and existing project records. Do not silently replace an existing local Vibo connection or migrate its records. If local and online versions coexist, explain which one this project will use.

   **识别宿主和已有配置。** 使用当前宿主支持的连接工具、设置或命令入口。保留其他 MCP 配置；发现已有本地版时，不擅自覆盖或上传旧记录，说明此次连接的是线上版。

2. **Add or reuse the remote connection.** Configure a server named `vibo` with the MCP URL and Streamable HTTP transport above, using the host's supported mechanism. Request required permissions. If the host does not let an agent modify the connection, provide its exact settings entry and the minimum manual steps; do not claim completion or fall back to installing an unrelated local runtime.

   **连接远程服务。** 优先自动完成宿主允许的配置；必须由用户操作的授权、设置步骤，明确引导。如果当前宿主无法在对话中完成配置，如实说明，不宣称“一句话已经全部安装成功”。

3. **Complete browser authorization.** The user may authorize a guest space without signing up. GitHub login is optional and links projects to an account for other devices. If the user has existing guest records, authorize in that browser or sign in to the intended account. Do not bypass authorization or overwrite another space's browser session.

   **完成浏览器授权。** 无需注册也能使用核心功能。GitHub 登录用于跨端找回项目。已有记录时使用对应浏览器或账号，避免连接到另一个空空间。

4. **Verify the actual tools immediately, before project setup or history work.** Confirm these tools are discoverable and callable: `get_project_context`, `read_updates`, `connect_project`, `sync_plan`, `report_event`, `session_heartbeat`, `open_dashboard`, and `submit_progress`. Read the server's initialization instructions. A saved config alone is not a working connection. Some hosts require reloading the connection or a new conversation. If the tools are missing, stop onboarding immediately and give that precise next step. Reuse valid authorization; do not repeatedly authorize, install the local runtime, update a local project, or open localhost as a substitute.

   **验证实际可用性。** 配置已保存不等于连接已生效。若宿主尚未加载工具，引导重新开启对话或重启后继续，不捏造工具调用结果。

5. **Load persistent reporting rules.** Read the reporting-rules URL above. If the host supports skills or project rules, put the rules in the entry it actually loads; preserve existing instructions. Limit automatic tracking to the project the user enabled. Do not silently enable all projects globally. A downloaded file that the host never loads is not a completed setup.

   **加载持续汇报规范。** 使用宿主真正会读取的 Skill 或项目规则入口，保留已有规则，并限定为用户授权的项目。不要只下载文件却没有加载，也不要把所有项目默认开启。

6. **Associate the right project.** Call `get_project_context` first. Reuse `workspace` and `project_id` from `.vibo/project.json` when present. Otherwise generate an opaque workspace UUID once, call `connect_project`, and save the returned project ID. Store only service URL and opaque IDs there, never credentials or absolute local paths. When continuing an existing online project from another tool, confirm the intended project and pass its existing ID; names alone are not enough to merge projects.

   **关联正确项目。** 跨对话复用稳定标识，不因新对话或切换工具重复建项目。没有实际项目上下文时先确认项目，不创建虚假的示例冒充用户项目。

7. **Sync real context incrementally.** Organize delivery goals, modules and tasks from the current project's actual context. Preserve existing IDs, ordering, implementation status, checks and history. Prefer `submit_progress` to submit goals, modules, tasks and real events atomically in one call. Use unique `client_id` values for new records and reference them in `module_id`, `goal_id`, `depends_on` and event `task_id`; use existing `id` values for updates. Supply `project_id`, `session_id`, `base_revision` and a UUID `request_id`. Reuse the same request ID and content on retries. The result returns the saved project, revision and ID map. Legacy `sync_plan` remains compatible. Do not mark historical work complete without evidence, invent dependencies, or upload source code and full conversations.

   **同步真实计划。** 复用已有上下文并增量更新；无法确定的内容保持待归类或未知。实现、检查和人工验收是不同维度。

8. **Open the dashboard in-app first.** Call `open_dashboard` and follow `browser_preference` / `opening_instructions`. Prefer the coding tool's built-in browser beside the conversation, reusing the current project tab when possible. In Codex, if `open_in_codex` is available, use `placement:"right"` with `target:{type:"browser",url:open_url}`; otherwise use its supported in-app browser tool. Do not default to shell `open`, `xdg-open`, Python `webbrowser`, Chrome or the system browser. Use an external browser only if the user requests it, the host has no built-in browser, or a real in-app opening attempt fails. If the host cannot open any page, supply the normal dashboard link.

   OAuth authorization may happen in an external browser; keep the dashboard preference in-app. Browser sessions are separate. If needed, sign in to the same Vibo account in-app; do not copy browser cookies or create a duplicate project. Open `open_url` privately once; if consumed or expired, request a new link before changing browsers. Only share `dashboard_url` in the final reply. Verify the page when possible; requesting a tab does not prove it opened.

   **优先在 Agent 内置浏览器打开看板。** 在支持的宿主中与对话并排展示；Codex 优先使用可用的 `open_in_codex` 右侧网页面板或内置浏览器工具。尽量复用当前项目标签，不默认调用系统浏览器。仅在用户指定、宿主不支持或实际开页失败时回退。登录授权可以由宿主打开到外部，但看板仍优先内置；必要时在内置浏览器登录同一账号，不复制 Cookie、不重建项目。一次性链接过期或已消费后需重新获取，不在多个浏览器反复使用。

9. **Continue reporting during normal work.** Follow the service rules for plan changes, task start, implementation, checks actually performed, user-action blockers and session completion. No separate “sync progress” request should be required after tracking is enabled. Reuse event IDs on retries; reread and compare on revision conflicts. Heartbeats indicate actual work, never simulated activity. Model compliance still depends on the host loading the rules; do not promise a background monitor.

   **正常开发时主动汇报。** 不需要用户反复提醒同步；但服务不会自动监听所有对话，不能承诺模型永远不会漏报。

10. **Report the outcome accurately.** State which host was configured, whether tools are actually available, whether rules are loaded, and which project was connected. Provide the dashboard link and any remaining user action. Only say setup is complete after a real remote submission returns the intended saved project and task content, and the opened dashboard uses the online service origin. Authorization success and local updates are not online project success.

    **完成门槛：** 实际线上提交成功、返回的项目与事项核对一致、打开的看板属于线上服务，才算接入完成。工具未加载时立即说明，不回退本地，不重复授权。旧本地记录迁移与新项目接入单独处理。

    **如实交付结果。** 区分“已配置”“已连接”“已加载规则”“已开始跟踪”，未完成的步骤明确说明。

## Verified scope / 已验证范围

The deployed service has passed browser PKCE authorization, official MCP client tool discovery and progress reports, live dashboard updates, real GitHub login, guest-project retention and recovery across two independent browser sessions. Native Codex, Cursor and Claude Code onboarding and ongoing reporting still require separate host-specific testing. Do not advertise them all as verified.

正式服务已实测上述协议与网页流程；两个独立浏览器会话在同一电脑上验证，不等同于两台物理设备。各编码宿主的原生接入、规则发现和持续自动汇报仍待分别实测。
