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

## License

MIT
