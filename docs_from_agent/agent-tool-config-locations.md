# エージェントツール設定ファイル配置まとめ

確認日: 2026-06-14

この文書は、Cline、VS Code Chat、Claude Code、OpenCode、Codexで共有・管理しやすい設定ファイル、`AGENTS.md`相当の指示ファイル、skillファイルの配置場所を整理したものです。`~` はユーザーのホームディレクトリ、`$REPO_ROOT` はリポジトリルートを表します。

## 一覧

| ツール | 設定ファイル | `AGENTS.md`相当の指示ファイル | skillのglobal配置 | skillのproject配置 |
|---|---|---|---|---|
| Cline | Global: `~/.cline/data/settings/global-settings.json`、provider/MCPは `~/.cline/data/settings/` 配下。Project: `$REPO_ROOT/.cline/` 配下 | Project: `$REPO_ROOT/.clinerules/`、`$REPO_ROOT/AGENTS.md`。Global: `~/Documents/Cline/Rules`、補助的に `~/.agents/AGENTS.md` | `~/.cline/skills/` | `$REPO_ROOT/.cline/skills/`、`$REPO_ROOT/.clinerules/skills/`、`$REPO_ROOT/.claude/skills/` |
| VS Code Chat / Copilot Chat | User: VS CodeのUser `settings.json`。Linux例: `~/.config/Code/User/settings.json`。Workspace: `$REPO_ROOT/.vscode/settings.json` | Always-on: `$REPO_ROOT/.github/copilot-instructions.md`、`$REPO_ROOT/AGENTS.md`、`$REPO_ROOT/CLAUDE.md`、`$REPO_ROOT/.claude/CLAUDE.md`。File-based: `$REPO_ROOT/.github/instructions/*.instructions.md`、`$REPO_ROOT/.claude/rules/*`。User: `~/.copilot/instructions`、`~/.claude/rules`、`~/.claude/CLAUDE.md` | `~/.copilot/skills/`、`~/.claude/skills/`、`~/.agents/skills/` | `$REPO_ROOT/.github/skills/`、`$REPO_ROOT/.claude/skills/`、`$REPO_ROOT/.agents/skills/` |
| Claude Code CLI | User: `~/.claude/settings.json`。Project: `$REPO_ROOT/.claude/settings.json`。Local: `$REPO_ROOT/.claude/settings.local.json`。MCP/状態: `~/.claude.json`、project MCPは `$REPO_ROOT/.mcp.json` | User: `~/.claude/CLAUDE.md`。Project: `$REPO_ROOT/CLAUDE.md` または `$REPO_ROOT/.claude/CLAUDE.md`。Local: `$REPO_ROOT/CLAUDE.local.md` | `~/.claude/skills/<skill-name>/SKILL.md` | `$REPO_ROOT/.claude/skills/<skill-name>/SKILL.md` |
| OpenCode | Global: `~/.config/opencode/opencode.json`、TUIは `~/.config/opencode/tui.json`。Project: `$REPO_ROOT/opencode.json`、TUIは `$REPO_ROOT/tui.json`。ディレクトリ型設定: `~/.config/opencode/` と `$REPO_ROOT/.opencode/` | Global: `~/.config/opencode/AGENTS.md`。Project: `$REPO_ROOT/AGENTS.md`。Claude互換フォールバック: `$REPO_ROOT/CLAUDE.md`、`~/.claude/CLAUDE.md` | `~/.config/opencode/skills/<name>/SKILL.md`、`~/.claude/skills/<name>/SKILL.md`、`~/.agents/skills/<name>/SKILL.md` | `$REPO_ROOT/.opencode/skills/<name>/SKILL.md`、`$REPO_ROOT/.claude/skills/<name>/SKILL.md`、`$REPO_ROOT/.agents/skills/<name>/SKILL.md` |
| Codex CLI / IDE | User: `~/.codex/config.toml`。Project: `$REPO_ROOT/.codex/config.toml`。Profile: `~/.codex/<profile-name>.config.toml`。System: `/etc/codex/config.toml` | Global: `~/.codex/AGENTS.override.md` または `~/.codex/AGENTS.md`。Project: `$REPO_ROOT/AGENTS.override.md` または `$REPO_ROOT/AGENTS.md`。`project_doc_fallback_filenames` で別名を追加可能 | `$HOME/.agents/skills/<skill-name>/SKILL.md`。Admin: `/etc/codex/skills/<skill-name>/SKILL.md` | `$CWD/.agents/skills/<skill-name>/SKILL.md` から `$REPO_ROOT/.agents/skills/<skill-name>/SKILL.md` までの親ディレクトリを走査 |

## Cline

Clineは、共通設定を `~/.cline/` に置き、プロジェクト共有の設定をリポジトリ内の `.cline/` に置く構成です。Cline公式ドキュメントでは、global設定の主要ルートは `~/.cline/`、構造化された状態は `~/.cline/data/`、project設定は `$REPO_ROOT/.cline/` とされています。

管理対象:

| 種別 | Global | Project |
|---|---|---|
| 設定 | `~/.cline/data/settings/global-settings.json`、`~/.cline/data/settings/providers.json`、`~/.cline/data/settings/cline_mcp_settings.json` | `$REPO_ROOT/.cline/` 配下 |
| Rules | `~/.cline/rules/`、互換パス `~/Documents/Cline/Rules`、クロスツール用 `~/.agents/AGENTS.md` | `$REPO_ROOT/.clinerules/`、`$REPO_ROOT/AGENTS.md` |
| Skills | `~/.cline/skills/` | `$REPO_ROOT/.cline/skills/`、`$REPO_ROOT/.clinerules/skills/`、`$REPO_ROOT/.claude/skills/` |

注意点:

- ClineのRulesは `.md` と `.txt` を読みます。
- `.clinerules/` はClineの主形式です。
- `AGENTS.md` はクロスツール互換の標準形式として扱われます。
- Skillは実験的機能で、`Settings -> Features -> Enable Skills` が必要です。
- ClineのSkillは `SKILL.md` を含むディレクトリで、`name` はディレクトリ名と一致させます。

## VS Code Chat / Copilot Chat

VS Code Chatは、VS Codeの通常設定に加えて、Copilot/Agent用の指示、prompt、skill、custom agentをファイルとして扱います。Workspace設定は通常 `$REPO_ROOT/.vscode/settings.json`、User設定はVS CodeのUser `settings.json` です。

管理対象:

| 種別 | User / Global | Project / Workspace |
|---|---|---|
| VS Code設定 | User `settings.json`。Linuxの標準例: `~/.config/Code/User/settings.json` | `$REPO_ROOT/.vscode/settings.json` |
| Always-on instructions | `~/.claude/CLAUDE.md`、GitHub organization instructions、個人プロファイルのinstructions | `$REPO_ROOT/.github/copilot-instructions.md`、`$REPO_ROOT/AGENTS.md`、`$REPO_ROOT/CLAUDE.md`、`$REPO_ROOT/.claude/CLAUDE.md` |
| File-based instructions | `~/.copilot/instructions`、`~/.claude/rules`、VS Code user data | `$REPO_ROOT/.github/instructions/*.instructions.md`、`$REPO_ROOT/.claude/rules/*` |
| Prompt files | VS Code user profile内 | `$REPO_ROOT/.github/prompts/*.prompt.md` |
| Agent Skills | `~/.copilot/skills/`、`~/.claude/skills/`、`~/.agents/skills/` | `$REPO_ROOT/.github/skills/`、`$REPO_ROOT/.claude/skills/`、`$REPO_ROOT/.agents/skills/` |

関連するVS Code設定:

- `chat.useAgentsMdFile`: `AGENTS.md` を使うか。
- `chat.useNestedAgentsMdFiles`: サブフォルダの `AGENTS.md` を使うか。
- `chat.useClaudeMdFile`: `CLAUDE.md` を使うか。
- `chat.instructionsFilesLocations`: instructionファイルの場所を追加・制限する。
- `chat.promptFilesLocations`: promptファイルの場所を追加する。
- `chat.agentSkillsLocations`: project skillの場所を追加する。
- `chat.useCustomizationsInParentRepositories`: monorepoで親リポジトリのcustomizationを探索する。

## Claude Code CLI

Claude Codeは、`~/.claude/` をユーザー設定、リポジトリ内 `.claude/` をプロジェクト設定として使います。`settings.json` は階層的な公式設定ファイルです。

管理対象:

| 種別 | User / Global | Project | Local |
|---|---|---|---|
| 設定 | `~/.claude/settings.json` | `$REPO_ROOT/.claude/settings.json` | `$REPO_ROOT/.claude/settings.local.json` |
| MCP | `~/.claude.json` | `$REPO_ROOT/.mcp.json` | `~/.claude.json` のproject別状態 |
| Subagents | `~/.claude/agents/` | `$REPO_ROOT/.claude/agents/` | なし |
| CLAUDE.md | `~/.claude/CLAUDE.md` | `$REPO_ROOT/CLAUDE.md` または `$REPO_ROOT/.claude/CLAUDE.md` | `$REPO_ROOT/CLAUDE.local.md` |
| Skills | `~/.claude/skills/<skill-name>/SKILL.md` | `$REPO_ROOT/.claude/skills/<skill-name>/SKILL.md` | なし |

注意点:

- 設定の優先順は Managed、CLI引数、Local、Project、User、の順です。
- Skillは `SKILL.md` を含むディレクトリです。
- Project skillは、起動ディレクトリからリポジトリルートまでの `.claude/skills/` と、作業対象のネストした `.claude/skills/` が探索されます。
- 既存の `.claude/commands/*.md` は引き続き動作しますが、同名のskillがある場合はskillが優先されます。

## OpenCode

OpenCodeはJSON/JSONCの `opencode.json` と、`.opencode/` ディレクトリ配下のMarkdown定義を併用します。標準設定はmergeされ、後から読み込まれたものが競合キーを上書きします。

管理対象:

| 種別 | Global | Project |
|---|---|---|
| 設定 | `~/.config/opencode/opencode.json` | `$REPO_ROOT/opencode.json` |
| TUI設定 | `~/.config/opencode/tui.json` | `$REPO_ROOT/tui.json` |
| Agents | `~/.config/opencode/agents/*.md` | `$REPO_ROOT/.opencode/agents/*.md` |
| Commands | `~/.config/opencode/commands/*.md` | `$REPO_ROOT/.opencode/commands/*.md` |
| AGENTS.md | `~/.config/opencode/AGENTS.md` | `$REPO_ROOT/AGENTS.md` |
| Claude互換rules | `~/.claude/CLAUDE.md` | `$REPO_ROOT/CLAUDE.md` |
| Skills | `~/.config/opencode/skills/<name>/SKILL.md`、`~/.claude/skills/<name>/SKILL.md`、`~/.agents/skills/<name>/SKILL.md` | `$REPO_ROOT/.opencode/skills/<name>/SKILL.md`、`$REPO_ROOT/.claude/skills/<name>/SKILL.md`、`$REPO_ROOT/.agents/skills/<name>/SKILL.md` |

注意点:

- Project configは `opencode.json` をプロジェクトルートに置きます。
- `.opencode/` と `~/.config/opencode/` のサブディレクトリ名は、標準では `agents/`、`commands/`、`plugins/`、`skills/` など複数形です。
- OpenCodeは `AGENTS.md` を主なcustom instructionとして扱い、`CLAUDE.md` は互換フォールバックです。
- `instructions` キーで既存のルールファイルを追加できますが、remote URLは外部通信を伴うため、組織方針に合わせて制御してください。

## Codex CLI / IDE

CodexはCLIとIDE extensionで `~/.codex/config.toml` を共有します。Project側は信頼済みプロジェクトの場合のみ `.codex/` レイヤーを読みます。

管理対象:

| 種別 | User / Global | Project | System / Admin |
|---|---|---|---|
| 設定 | `~/.codex/config.toml` | `$REPO_ROOT/.codex/config.toml` | `/etc/codex/config.toml` |
| Profile設定 | `~/.codex/<profile-name>.config.toml` | なし | なし |
| AGENTS.md | `~/.codex/AGENTS.override.md` または `~/.codex/AGENTS.md` | `$REPO_ROOT/AGENTS.override.md` または `$REPO_ROOT/AGENTS.md`。サブディレクトリにも配置可能 | なし |
| Skills | `$HOME/.agents/skills/<skill-name>/SKILL.md` | `$CWD/.agents/skills/<skill-name>/SKILL.md` から `$REPO_ROOT/.agents/skills/<skill-name>/SKILL.md` まで | `/etc/codex/skills/<skill-name>/SKILL.md` |

注意点:

- 設定の優先順は、CLI flags / `--config`、project `.codex/config.toml`、profile、user、system、built-in defaultsです。
- `CODEX_HOME` で `~/.codex` 相当の場所を切り替えられます。
- `AGENTS.override.md` がある場合、同じスコープの `AGENTS.md` より優先されます。
- Project instructionの代替ファイル名は `project_doc_fallback_filenames` で追加できます。
- SkillはOpenAIのCodex組み込み、user、repo、admin/systemの各スコープから読み込まれます。
- この環境では実際のCodex homeは `/root/.codex` で、`AGENTS.md`、`config.toml`、`skills` がシンボリックリンクとして存在していました。

## 共通管理のおすすめ

複数ツールで共有したい場合は、次の置き方が衝突が少なくなります。

1. プロジェクト共通の最上位指示は `$REPO_ROOT/AGENTS.md` に集約する。
2. Claude Codeとの互換性が重要なリポジトリは、`$REPO_ROOT/CLAUDE.md` または `$REPO_ROOT/.claude/CLAUDE.md` を追加する。
3. クロスツールskillは `$REPO_ROOT/.agents/skills/<skill-name>/SKILL.md` を第一候補にする。
4. Claude Code専用のskillは `$REPO_ROOT/.claude/skills/<skill-name>/SKILL.md` に置く。
5. Cline専用のskillは `$REPO_ROOT/.cline/skills/<skill-name>/SKILL.md` に置く。
6. VS Code Copilot専用のpromptやinstructionsは `.github/` 配下に置く。
7. 個人ルールはglobal領域に置き、リポジトリにはチームで共有してよい内容だけを置く。
8. APIキー、トークン、個人の認証情報はリポジトリ配下の設定・skill・rulesに含めない。

## 参考ソース

- Cline Config: https://docs.cline.bot/getting-started/config
- Cline Rules: https://docs.cline.bot/customization/cline-rules
- Cline Skills: https://docs.cline.bot/customization/skills
- VS Code Custom Instructions: https://code.visualstudio.com/docs/agent-customization/custom-instructions
- VS Code Agent Skills: https://code.visualstudio.com/docs/agent-customization/agent-skills
- VS Code Prompt Files: https://code.visualstudio.com/docs/agent-customization/prompt-files
- VS Code Settings: https://code.visualstudio.com/docs/configure/settings
- Claude Code Settings: https://code.claude.com/docs/en/settings
- Claude Code Skills: https://code.claude.com/docs/en/skills
- OpenCode Config: https://opencode.ai/docs/config
- OpenCode Rules: https://opencode.ai/docs/rules
- OpenCode Skills: https://opencode.ai/docs/skills/
- OpenCode Commands: https://opencode.ai/docs/commands
- Codex Config Basics: https://developers.openai.com/codex/config-basic
- Codex AGENTS.md: https://developers.openai.com/codex/guides/agents-md
- Codex Skills: https://developers.openai.com/codex/skills
- Codex IDE Settings: https://developers.openai.com/codex/ide/settings
