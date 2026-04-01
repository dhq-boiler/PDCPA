# PDCPA - Plan-Do-Check-Plan-Action

An enhanced PDCA cycle skill for AI agents in [Claude Code](https://claude.com/claude-code).

## What is PDCPA?

PDCPA adds a **Re-Plan** phase between Check and Action in the traditional PDCA cycle:

```
Plan → Do → Check → Re-Plan → Action
```

Traditional PDCA feeds Check results directly into Action, which often leads to superficial fixes. By inserting a Re-Plan phase, AI agents can:

1. **Identify root causes** by organizing insights from Check
2. **Compare multiple options** with pros, cons, and estimated improvement rates
3. **Course-correct** when the original Plan's assumptions were wrong
4. **Collaborate with users** by presenting options via interactive selection

## Key Features

- **Structured 5-phase output** with consistent formatting
- **Interactive Re-Plan**: Uses `AskUserQuestion` to present improvement options with:
  - Recommended option marked with "(Recommended)"
  - Estimated improvement rate for each option
  - Pros and cons comparison
- **Dual-purpose**: Works as both a task management framework and a problem-solving framework
- **Mid-cycle resume**: Can restart from any phase

## Installation

### Claude Code CLI

```bash
claude skill add --from https://github.com/dhq-boiler/PDCPA
```

### Manual Installation

Copy `SKILL.md` to `~/.claude/skills/pdcpa/SKILL.md`.

## Usage

Invoke with `/pdcpa` or mention PDCPA in your prompt:

```
/pdcpa Add dark mode to my web app
```

```
I want to fix the API latency issue. Let's use PDCPA.
```

```
We finished Check — coverage is 60% vs 80% target. Re-Plan from here.
```

---

## 日本語ドキュメント

### PDCPA とは？

PDCPA は、従来の PDCA サイクルに **Re-Plan（再計画）** フェーズを追加した、AIエージェント向けの改良版フレームワークです。

```
Plan → Do → Check → Re-Plan → Action
```

従来の PDCA では Check の結果をそのまま Action に反映しますが、これでは表面的な対処に終わりがちです。Re-Plan フェーズを挟むことで、AIエージェントは：

1. Check で得た気づきを整理し、**根本原因を特定**できる
2. 複数の改善案を**メリット・デメリット・予想改善率付きで比較**できる
3. 最初の Plan の前提が間違っていた場合に**軌道修正**できる
4. `AskUserQuestion` で選択肢を提示し、**ユーザーと一緒に方針を決められる**

### 主な特徴

- **5フェーズの構造化出力**: 一貫したフォーマットで各フェーズを記録
- **インタラクティブな Re-Plan**: 改善案をユーザーに提示し選択してもらう
  - 推奨案に「（推奨）」マークを付与
  - 各案に予想改善率を表示
  - メリット・デメリットを比較表示
- **二つの用途**: タスク管理と問題解決の両方に対応
- **途中再開**: サイクルの任意のフェーズから再開可能

### インストール

#### Claude Code CLI

```bash
claude skill add --from https://github.com/dhq-boiler/PDCPA
```

#### 手動インストール

`SKILL.md` を `~/.claude/skills/pdcpa/SKILL.md` にコピーしてください。

### 使い方

`/pdcpa` コマンドまたはプロンプト内で PDCPA に言及してください：

```
/pdcpa Webアプリにダークモード機能を追加したい
```

```
本番環境でAPIレスポンスが遅くなっている。PDCPAで原因特定と改善をしたい
```

```
前回Checkまで終わった。結果は「テストカバレッジが60%で目標の80%に届かなかった」。ここからRe-Planして
```

## License

MIT
