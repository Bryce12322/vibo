# Install Vibo with Codex / 让 Codex 安装 Vibo

Users can ask / 用户可以直接说：

> Install Vibo for me from https://github.com/Bryce12322/vibo — download, verify, unzip and install its Codex skill.

> 帮我安装 Vibo：https://github.com/Bryce12322/vibo，请自动完成下载、校验、解压和 Skill 安装。

## For coding agents / 给 Codex 的安装步骤

When a user asks to install Vibo, perform the steps below using available tools and the user's granted permissions. Complete the download and extraction yourself rather than asking the user to do them manually. If the host requires network or local-file installation approval, request it and continue after approval.

用户要求安装后，按以下步骤执行下载、校验、解压、安装和检查。宿主需要授权时，说明原因并等待用户批准；不要求用户先手动下载或解压。

1. Check macOS and Node.js **22.13 or newer**. If the platform is unsupported or Node.js is missing/outdated, explain the requirement; do not silently install or replace system software. / 先检查系统与 Node.js 环境，缺少依赖时说明，不擅自更换系统环境。
2. Download the complete **vibo-local-v0.9.1.zip** and **SHA256SUMS.txt** from the fixed release URLs below into a temporary directory. No GitHub login is needed. / 下载完整发行包与校验文件，不需要 GitHub 登录。
3. Verify SHA256 before extracting or executing the installer. Stop on download or checksum failure. / 先校验，再解压执行；下载或校验失败时停止。
4. Extract using macOS `ditto`, then run `bash "<extracted>/vibo-local/Install Vibo.command"`. This installs the complete `track-project` skill and bundled runtime into `~/.agents/skills/track-project` by default, backing up an existing installation. / 安装器包含完整运行文件，会备份旧版安装。
5. Verify the installed CLI with `--help`; optionally run `doctor` to inspect installation. A first installation can report “no project yet” or “service not running”; those do not mean the skill installation failed. Do not create a project or start tracking unless the user also requested it. / 检查安装入口；首次没有项目或服务尚未启动是正常情况，不擅自开始跟踪。
6. Tell the user installation succeeded, where the skill was installed and how to enable it in their project. It should become available on a subsequent turn; if their Codex session has not discovered it, suggest a new chat or restart and `$track-project`. / 告知安装结果和启用方法；如未被宿主发现，再开启新对话或重启。

Vibo is distributed as a **Codex skill**, rather than a marketplace extension. The repository root and GitHub-generated “Source code” archives contain distribution documentation, not the complete runtime. Do not install the repository root as a skill or download only `SKILL.md`.

本仓库根目录及自动生成的 Source code 包是说明文件；完整 Skill 和运行文件在下面的发行安装包中。

## Download URLs / 下载地址

- Package: https://github.com/Bryce12322/vibo/releases/download/v0.9.1/vibo-local-v0.9.1.zip
- Checksum: https://github.com/Bryce12322/vibo/releases/download/v0.9.1/SHA256SUMS.txt
- Expected package SHA256: `7c64cd65f563211666fe89e43176258d1087066ba0b9d848e1cd10fd14258731`

## Reference commands / 可执行步骤

Run after checking macOS and Node.js. The installer is not Apple-signed or notarized. This does not require disabling macOS security settings.

确认 macOS 和 Node.js 环境后执行。当前安装器未做 Apple 签名或公证；无须关闭 macOS 安全设置。

```bash
(
  set -e
  node -e 'const [a,b]=process.versions.node.split(".").map(Number); if(a<22||(a===22&&b<13)) { console.error("Vibo requires Node.js 22.13+"); process.exit(1); }'
  vibo_install_dir=$(mktemp -d "${TMPDIR:-/tmp}/vibo-install.XXXXXX")
  trap 'rm -rf -- "$vibo_install_dir"' EXIT
  cd "$vibo_install_dir"
  vibo_release_url='https://github.com/Bryce12322/vibo/releases/download/v0.9.1'
  curl --fail --location --silent --show-error --connect-timeout 10 --max-time 60 "$vibo_release_url/vibo-local-v0.9.1.zip" --output vibo-local-v0.9.1.zip
  curl --fail --location --silent --show-error --connect-timeout 10 --max-time 60 "$vibo_release_url/SHA256SUMS.txt" --output SHA256SUMS.txt
  shasum -a 256 -c SHA256SUMS.txt
  ditto -x -k vibo-local-v0.9.1.zip unpacked
  bash "unpacked/vibo-local/Install Vibo.command"
  node --disable-warning=ExperimentalWarning "${FLOW_SKILL_DIR:-$HOME/.agents/skills}/track-project/scripts/flow.mjs" --help
)
```

`FLOW_SKILL_DIR` can select the host's actual skill directory when required. Keep one active installation; do not create duplicate copies in several skill-discovery roots. Installing or updating Vibo does not require reading, exporting or deleting the user's existing project database or connection files.

如宿主需要其他 Skill 安装目录，可用 `FLOW_SKILL_DIR` 指定；不要在多个发现目录重复安装。安装或更新无须读取、导出或删除已有项目数据库及连接文件。

## Verification / 已验证的范围

The public 0.9.1 package was downloaded without authentication and tested on macOS with Node.js 22.17.1 in isolated install/data directories. Checksum, extraction, installer, packaged CLI, local service and diagnostics passed. Reinstalling preserved the sample project. Existing user installations and private records were untouched.

公开包已在 macOS、Node.js 22.17.1 的隔离目录完成下载到启动的验证，重复安装保留测试项目。验证的是 Codex 可执行的安装流程，不保证每个 Codex 版本都会自动加载 Skill，也不承诺省略宿主的授权提示。
