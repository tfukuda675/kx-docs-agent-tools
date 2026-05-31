# VSCode + Clineで生成AIを使う前に知っておきたいツールの違い

対象: AIやITに詳しくないが、普段Linuxを使っている人  
想定環境: Windows PC上のVSCodeからRemote-SSHでLinuxへ接続し、Linux上のファイルをAI支援で編集する

---

## 1. 最初に押さえる全体像

生成AIツールを比べるときは、まず次の3つを分けて考えます。

| 種類 | 役割 | 例 |
|---|---|---|
| AIモデル | 文章やコードを考える頭脳 | GPT、Claude、Gemini、ローカルLLMなど |
| AIを使うための道具 | AIモデルに指示を出し、ファイル編集やコマンド実行を助ける | Cline、Claude Code拡張機能、Codex CLI、Claude Code CLI、OpenCode |
| AIを使う画面 | チャット画面や管理画面を提供する | ChatGPT、Claude.ai、Open WebUI |

重要なのは、ClineやCodex CLIやClaude Code CLIは「AIそのもの」ではないという点です。  
これらは、AIモデルに依頼しながら、コードやファイルを扱いやすくするための道具です。

---

## 2. 今回の説明会で使う構成

今回の想定は次の流れです。

```text
Windows PC
  |
  | VSCode
  | Remote-SSH
  v
Linuxサーバー / Linux環境
  |
  | Linux上のファイル
  | Linux上のターミナル
  v
Clineに依頼して編集・確認
```

参加者はWindows側でVSCodeを開きますが、実際に編集するファイルはLinux側にあります。  
Remote-SSHで接続したVSCodeでは、Linux上のフォルダをVSCodeの画面で開いて操作できます。

---

## 3. Clineとは

Clineは、VSCodeなどのエディタの中で使えるAIコーディング支援ツールです。  
チャットで依頼すると、プロジェクト内のファイルを読み、変更案を作り、必要に応じてターミナルコマンドを実行します。

初心者向けに言うと、Clineは次のような存在です。

```text
VSCodeの横にいる、AIに相談できる作業補助者
```

Clineの特徴:

| 観点 | 内容 |
|---|---|
| 使う場所 | VSCodeの画面内 |
| 操作方法 | チャットで依頼する |
| 得意なこと | ファイル編集、コード修正、説明、コマンド実行の補助 |
| ファイルとの距離 | 開いているプロジェクトのファイルを直接扱いやすい |
| 初心者への向き | 画面で差分を見ながら使えるため説明しやすい |
| 注意点 | 変更やコマンド実行は内容を確認してから承認する |

今回の説明会では、WindowsのVSCodeからRemote-SSHでLinuxへ接続しているため、ClineにはLinux上のファイル編集を手伝わせる、という使い方になります。

---

## 4. Codex CLIとは

Codex CLIは、ターミナル上で使うOpenAIのコーディング支援ツールです。  
コマンドラインで起動し、今いるディレクトリのファイルを読み、編集し、コマンドを実行しながら作業を進めます。

初心者向けに言うと、Codex CLIは次のような存在です。

```text
Linuxのターミナルで動く、AI作業アシスタント
```

Codex CLIの特徴:

| 観点 | 内容 |
|---|---|
| 使う場所 | ターミナル |
| 操作方法 | ターミナル上の対話画面、またはコマンド |
| 得意なこと | リポジトリ調査、コード編集、テスト実行、レビュー |
| ファイルとの距離 | 起動したディレクトリ配下のファイルを扱う |
| 初心者への向き | Linux操作に慣れていれば強力だが、画面の理解はやや難しい |
| 注意点 | どのディレクトリで起動しているか、何のコマンドを実行するかを確認する |

Clineとの大きな違いは、VSCodeの拡張機能ではなく、ターミナルで使う点です。

---

## 5. OpenCodeとは

OpenCodeは、オープンソースのAIコーディング支援ツールです。  
主にターミナルで使う道具として説明できますが、公式にはデスクトップアプリやIDE拡張機能としても利用できる形で提供されています。

初心者向けに言うと、OpenCodeは次のような存在です。

```text
好きなAIモデルを選んで使いやすい、オープンソースのAI作業アシスタント
```

OpenCodeの特徴:

| 観点 | 内容 |
|---|---|
| 使う場所 | 主にターミナル。デスクトップアプリやIDE拡張機能もある |
| 操作方法 | ターミナル上の対話画面など |
| 得意なこと | コードベースの説明、機能追加、ファイル修正、変更の取り消し |
| ファイルとの距離 | 起動したプロジェクトのファイルを扱う |
| 初心者への向き | Linuxやターミナルに慣れている人には分かりやすいが、初回説明では画面構造の説明が必要 |
| 注意点 | 利用するAIモデル提供元のAPIキーや設定が必要になることがある |

Codex CLIやClaude Code CLIと同じく、OpenCodeも「ターミナルからAIに開発作業を頼む道具」と考えると理解しやすいです。  
ただし、特定のAIモデルだけに固定されているのではなく、複数のLLMプロバイダを選んで使う設計です。

---

## 6. Claude Code CLIとは

Claude Code CLIは、AnthropicのClaudeを使ったコーディング支援ツールです。  
こちらもターミナルから使い、コードベースを読み、ファイル編集やコマンド実行を支援します。

初心者向けに言うと、Claude Code CLIは次のような存在です。

```text
Claudeにターミナルから作業を頼むための道具
```

Claude Code CLIの特徴:

| 観点 | 内容 |
|---|---|
| 使う場所 | 主にターミナル |
| 操作方法 | 主にターミナル上の対話 |
| 得意なこと | コード理解、複数ファイルの修正、開発作業の自動化 |
| ファイルとの距離 | プロジェクトのファイルを直接扱う |
| 初心者への向き | Claudeに慣れている人には分かりやすいが、CLIの理解が必要 |
| 注意点 | アカウント、権限、実行するコマンドの確認が必要 |

Codex CLIとの違いは、主に提供元と使うAIモデルの系統です。  
Codex CLIはOpenAI系、Claude Code CLIはAnthropicのClaude系です。

---

## 7. Claude CodeのVSCode拡張機能とは

Claude Codeには、ターミナルで使うCLIだけでなく、VSCodeの中で使える公式拡張機能もあります。  
この拡張機能を使うと、Claude CodeをVSCodeのパネルから開き、ファイルや選択範囲を参照しながら相談できます。

初心者向けに言うと、Claude CodeのVSCode拡張機能は次のような存在です。

```text
VSCodeの中でClaude Codeを使うための公式画面
```

Claude Code VSCode拡張機能の特徴:

| 観点 | 内容 |
|---|---|
| 使う場所 | VSCodeの画面内 |
| 操作方法 | VSCode内のClaude Codeパネル、コマンドパレット、ショートカット |
| 得意なこと | ファイル説明、コード修正、差分確認、選択範囲の参照、会話履歴の利用 |
| ファイルとの距離 | VSCodeで開いているワークスペースを扱いやすい |
| 初心者への向き | Clineと同じくVSCode上で見えるため説明しやすい |
| 注意点 | Anthropicアカウントや組織のClaude利用設定が必要。CLIにしかない機能もある |

Clineとの違いは、主に使うAIモデルと提供元です。  
Clineは複数のAIプロバイダを選びやすい道具です。Claude Code拡張機能は、Claude CodeをVSCodeで使うためのAnthropic公式の道具です。

今回のようにRemote-SSHでLinux上のフォルダをVSCodeから開く場合、どちらも「VSCode上で差分を確認しながらAIに編集を頼む」道具として説明できます。  
初回説明では、組織でどちらを標準にするかを決めてから紹介した方が混乱しにくいです。

---

## 8. Open WebUIとは

Open WebUIは、ブラウザから使うAIチャット画面を自分たちで用意するためのWebサービスです。  
OllamaやOpenAI互換APIなど、複数のAIモデル提供元につなげられます。

初心者向けに言うと、Open WebUIは次のような存在です。

```text
自分たちで用意できる、ブラウザ版AIチャット画面
```

Open WebUIの特徴:

| 観点 | 内容 |
|---|---|
| 使う場所 | Webブラウザ |
| 操作方法 | チャット画面 |
| 得意なこと | AIとの会話、文章作成、質問回答、モデル切り替え |
| ファイルとの距離 | 通常はエディタほど直接的には編集しない |
| 初心者への向き | チャット画面なので入りやすい |
| 注意点 | Linux上のファイルを直接安全に編集する用途ではClineなどの方が説明しやすい |

Open WebUIは「コード編集専用の作業道具」というより、「AIチャットをWebで使うための土台」です。  
そのため、VSCodeでLinux上のファイルを編集する今回の用途では、主役はClineになります。

---

## 9. 画面の種類とOSS区分

ツールを整理するときは、「どの画面で使うか」と「OSSかどうか」を分けると理解しやすくなります。

| ツール | 画面の種類 | OSS / それ以外 | 補足 |
|---|---|---|---|
| Cline | VSCode拡張機能 | OSS | Cline本体はGitHubで公開されている。使うAIモデルは別途選ぶ |
| Claude Code VSCode拡張機能 | VSCode拡張機能 | それ以外 | Anthropic公式のClaude Code用拡張機能。Claude利用契約やアカウントに依存する |
| Codex CLI | TUI / CLI | OSS | OpenAIのターミナル向けコーディングエージェント。リポジトリはApache-2.0ライセンス |
| Claude Code CLI | TUI / CLI | それ以外 | Anthropic公式のClaude Code CLI。Claude利用契約やアカウントに依存する |
| OpenCode | TUI / CLI | OSS | オープンソースのAI coding agent。複数のAIプロバイダを選べる |
| Open WebUI | WebUI | OSS相当 / ソース公開 | WebブラウザでAIチャットを使うためのUI。独自ライセンスのため、厳密なOSS判定は利用前に確認する |

この表では、参加者向けの説明として次のように単純化しています。

```text
VSCode拡張機能 = VSCodeの中で使う
TUI / CLI = ターミナルで使う
WebUI = ブラウザで使う

OSS = ソースコードが公開され、再利用できるライセンスがあるもの
それ以外 = 提供元のサービス、契約、アカウントに強く依存するもの
```

注意点として、OSSのツールを使っていても、接続先のAIモデルやAPIは別料金・別契約になることがあります。  
「ツールがOSSであること」と「AIモデルを無料で自由に使えること」は別です。

---

## 10. ツールの比較

| 項目 | Cline | Claude Code VSCode拡張機能 | Codex CLI | Claude Code CLI | OpenCode | Open WebUI |
|---|---|---|---|---|---|---|
| 分類 | VSCode拡張機能 / IDE内AIエージェント | VSCode拡張機能 / IDE内AIエージェント | TUI / CLI型AIエージェント | TUI / CLI型AIエージェント | TUI / CLI型AIエージェント、IDE拡張、デスクトップアプリ | Web UI |
| 主な画面 | VSCode | VSCode | ターミナル | ターミナル | 主にターミナル | ブラウザ |
| 主な用途 | エディタ上でファイル編集をAIに手伝わせる | VSCode上でClaude Codeに編集や説明を頼む | ターミナルから開発作業をAIに任せる | ターミナルからClaudeに開発作業を任せる | ターミナルから複数モデル対応のAIエージェントに作業を頼む | AIチャット環境を提供する |
| Linuxファイル編集 | Remote-SSH先のワークスペースを扱いやすい | Remote-SSH先のワークスペースを扱いやすい | Linux上で起動すれば直接扱いやすい | Linux上で起動すれば直接扱いやすい | Linux上で起動すれば直接扱いやすい | 直接編集には向かないことが多い |
| 初心者への説明しやすさ | 高い。VSCode上で見える | 高い。VSCode上で見える | 中。CLIに慣れが必要 | 中。CLIに慣れが必要 | 中。CLIに慣れが必要 | 高い。ただしコード編集の説明とは別物 |
| AIモデル | 複数プロバイダを選べる | Claude / Anthropic系が中心 | OpenAI / ChatGPTアカウントまたはAPIキー | Claude / Anthropic系が中心 | 複数プロバイダを選べる | 接続先のモデル次第 |
| 承認の考え方 | 変更やコマンドを確認して進める | 差分や実行内容を確認して進める | 承認モードや権限設定を確認して使う | 権限モードを確認して使う | 権限設定や実行内容を確認して使う | 管理者設定や接続先の権限に依存 |

---

## 11. 参加者に伝える一言まとめ

| ツール | 一言で言うと |
|---|---|
| Cline | VSCodeの中で、AIにLinux上のファイル編集を手伝わせる道具 |
| Claude Code VSCode拡張機能 | VSCodeの中で、Claude CodeにLinux上のファイル編集を手伝わせる道具 |
| Codex CLI | ターミナルからOpenAI系のAIに開発作業を頼む道具 |
| Claude Code CLI | ターミナルからClaudeに開発作業を頼む道具 |
| OpenCode | ターミナルから複数モデル対応のAIエージェントに開発作業を頼む道具 |
| Open WebUI | ブラウザでAIチャットを使うためのWeb画面 |

今回の説明会では、次のように覚えてもらうと混乱しにくくなります。

```text
Cline / Claude Code VSCode拡張機能 = VSCodeで使う
Codex CLI / Claude Code CLI / OpenCode = ターミナルで使う
Open WebUI = ブラウザで使う
```

---

## 12. 今回Clineを中心にする理由

今回の参加者は、Windows PCのVSCodeからRemote-SSHでLinuxへ接続します。  
この構成では、Clineを使うと次の流れを画面で見せながら説明できます。

1. VSCodeでLinux上のフォルダを開く
2. Clineに「このファイルを説明して」と依頼する
3. Clineに「この部分を修正して」と依頼する
4. 変更差分を確認する
5. 問題なければ承認する
6. 必要ならターミナルコマンドの実行も確認して承認する

CLI型ツールは強力ですが、初心者向け説明会では「今どのファイルを触っているのか」「何が変わったのか」が画面で見えることが重要です。  
そのため、最初の入口としてはClineが扱いやすいです。

補足すると、Claude CodeのVSCode拡張機能も同じ理由で初心者に説明しやすい候補です。  
ただし、今回の主目的が「Clineを使えるようにすること」であれば、Claude Code拡張機能は「似た種類の公式Claude向けツール」として紹介する程度に留めると混乱を避けられます。

---

## 13. 安全に使うための共通ルール

どのツールを使う場合でも、次のルールを守ります。

| ルール | 理由 |
|---|---|
| AIの出力をそのまま信じない | AIは間違えることがある |
| ファイル変更は差分を確認する | 予想外の変更を防ぐ |
| コマンド実行前に内容を読む | 削除や外部通信を防ぐ |
| APIキーやパスワードを貼らない | 機密情報の漏えいを防ぐ |
| 作業前にGitの状態を確認する | 元に戻せる状態にする |
| 分からない指示は小さく分ける | AIへの依頼が明確になる |

初心者には、特に次の一文を強調します。

```text
AIは作業を速くする道具ですが、最終確認をするのは人間です。
```

---

## 14. 説明会での導入トーク例

今日は「AIに全部任せる方法」ではなく、「自分が確認しながらAIに手伝ってもらう方法」を扱います。  

みなさんは普段Linuxを使っていますが、今回はWindowsのVSCodeからRemote-SSHでLinuxに接続し、Linux上のファイルをVSCodeの画面で開きます。そこにClineという拡張機能を組み合わせると、AIに「このファイルを説明して」「この設定を直して」「変更点を確認して」と頼めるようになります。

似た道具として、Claude CodeのVSCode拡張機能もあります。これはClineと同じくVSCode上で使う道具ですが、Claude CodeをAnthropic公式の形で使うためのものです。

また、Codex CLI、Claude Code CLI、OpenCodeのようにターミナルで使う道具もあります。Linuxに慣れている人には便利ですが、初回説明では画面上で変更が見えるClineの方が理解しやすいです。

Open WebUIはブラウザでAIと会話するための画面です。文章作成や質問には便利ですが、VSCode上でLinuxのファイルを編集する今回の用途とは少し役割が違います。

---

## 15. まとめ

この資料で一番伝えたいことは、ツールを名前で覚えるのではなく、使う場所で整理することです。

| 使う場所 | ツール | 目的 |
|---|---|---|
| VSCode | Cline / Claude Code VSCode拡張機能 | 開いているファイルやプロジェクトをAIに手伝わせる |
| ターミナル | Codex CLI / Claude Code CLI / OpenCode | コマンドラインから開発作業をAIに手伝わせる |
| ブラウザ | Open WebUI | AIチャットをWeb画面で使う |

今回の主役は、VSCode + Remote-SSH + Clineです。  
Linux上のファイルを、VSCodeの画面で確認しながら、AIに少しずつ手伝ってもらう使い方を練習します。

---

## 参考資料

確認日: 2026-05-31

- Cline Documentation: https://docs.cline.bot/
- Cline GitHub Repository: https://github.com/cline/cline
- OpenAI Codex CLI GitHub Repository: https://github.com/openai/codex
- OpenAI Codex CLI Documentation: https://developers.openai.com/codex/cli/
- Claude Code Documentation: https://code.claude.com/docs/en/overview
- Claude Code VSCode Extension Documentation: https://code.claude.com/docs/en/ide-integrations
- OpenCode Documentation: https://opencode.ai/docs
- OpenCode GitHub Repository: https://github.com/sst/opencode
- Open WebUI Documentation: https://docs.openwebui.com/
- Open WebUI License: https://docs.openwebui.com/license/
- VSCode Remote-SSH Documentation: https://code.visualstudio.com/docs/remote/ssh
