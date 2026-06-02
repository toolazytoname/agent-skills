# Agent Skills

> A curated collection of 87 agent skills — designed to be portable across agent frameworks (Hermes, Pilotdeck, and others).

中文说明见下。

## Layout

```
agent-skills/
├── universal/      # 78 skills — framework-agnostic, work in any agent
└── hermes-only/    # 9 skills  — tightly coupled to Hermes Agent internals
```

### universal/ (78)

Skills that wrap CLI tools, APIs, or workflows without depending on a specific agent runtime. Safe to load into Pilotdeck, Claude Code, Codex, Hermes, or any framework that can invoke shell commands and read files.

| Category | Count | Examples |
|---|---:|---|
| `apple/` | 5 | apple-notes, apple-reminders, findmy, imessage, macos-computer-use |
| `autonomous-ai-agents/` | 3 | claude-code, codex, opencode (delegate to coding CLIs) |
| `creative/` | 19 | ascii-art, comfyui, manim-video, excalidraw, … |
| `data-science/` | 1 | jupyter-live-kernel |
| `dogfood/` | 1 | dogfood (web-app QA) |
| `email/` | 1 | himalaya (IMAP/SMTP) |
| `gaming/` | 2 | minecraft-modpack-server, pokemon-player |
| `github/` | 6 | github-auth, github-issues, github-pr-workflow, … |
| `mcp/` | 1 | native-mcp (MCP client) |
| `media/` | 5 | gif-search, heartmula, spotify, songsee, youtube-content |
| `mlops/` | 9 | axolotl, unsloth, llama-cpp, vllm, dspy, … |
| `note-taking/` | 1 | obsidian |
| `productivity/` | 9 | airtable, linear, notion, maps, powerpoint, … |
| `red-teaming/` | 1 | godmode |
| `research/` | 5 | arxiv, blogwatcher, llm-wiki, polymarket, research-paper-writing |
| `smart-home/` | 1 | openhue (Philips Hue) |
| `social-media/` | 1 | xurl (X/Twitter) |
| `software-development/` | 7 | node-inspect-debugger, plan, python-debugpy, spike, tdd, … |

### hermes-only/ (9)

Skills that depend on Hermes Agent's internal paths, tools, or transports. Loading them into another agent framework will not work out of the box.

| Category | Skill | Why hermes-only |
|---|---|---|
| `autonomous-ai-agents/` | `hermes-agent` | Configures Hermes itself |
| `autonomous-ai-agents/` | `yuanbao` | Bind to Hermes Feishu gateway |
| `devops/` | `kanban-orchestrator` | Hermes Kanban coordinator |
| `devops/` | `kanban-worker` | Hermes Kanban worker |
| `devops/` | `webhook-subscriptions` | Uses Hermes CLI |
| `software-development/` | `debugging-hermes-tui-commands` | Hermes TUI only |
| `software-development/` | `hermes-agent-skill-authoring` | Hermes skill format |
| `software-development/` | `subagent-driven-development` | Calls `delegate_task` |
| `software-development/` | `writing-plans` | Writes to `.hermes/plans/` |

## Loading into another agent

```python
import os, shutil
from pathlib import Path

REPO = Path("agent-skills")
TARGET = Path("./skills")  # your agent's skill directory

# Load only universal/ — skip hermes-only/
for entry in os.listdir(REPO / "universal"):
    shutil.copytree(REPO / "universal" / entry, TARGET / entry, dirs_exist_ok=True)
```

Each skill directory contains a `SKILL.md` with YAML frontmatter (name, description, platforms, metadata) and a markdown body with usage instructions. Optional `references/`, `templates/`, `scripts/` subdirectories hold supplementary material.

## Origin

Skills were authored/curated by [Hermes Agent](https://github.com/toolazytoname/hermes) and organized here for cross-framework reuse. Pilotdeck is the first non-Hermes consumer.

## License

MIT — see [LICENSE](./LICENSE).

---

# Agent Skills（中文）

> 87 个 agent skill 的精选合集 —— 设计为可在多种 agent 框架间移植（Hermes、Pilotdeck 等）。

## 目录结构

```
agent-skills/
├── universal/      # 78 个 — 框架无关，任何 agent 都可用
└── hermes-only/    # 9 个  — 强绑定 Hermes Agent 内部实现
```

### universal/（78 个）

封装 CLI 工具、API 或工作流，**不依赖特定 agent runtime**。可以安全加载到 Pilotdeck、Claude Code、Codex、Hermes 或任何能调用 shell 命令和读文件的框架。

### hermes-only/（9 个）

依赖 Hermes Agent 的内部路径、工具或传输层。**直接加载到其他 agent 框架开箱即用会失败**。包含 hermes-agent 自身配置、Feishu gateway 客户端、Kanban 多 agent 协调、`.hermes/plans/` 路径写入等。

## 在其他 agent 中加载

```python
import os, shutil
from pathlib import Path

REPO = Path("agent-skills")
TARGET = Path("./skills")  # 你 agent 的 skill 目录

# 只加载 universal/，跳过 hermes-only/
for entry in os.listdir(REPO / "universal"):
    shutil.copytree(REPO / "universal" / entry, TARGET / entry, dirs_exist_ok=True)
```

每个 skill 目录包含一个 `SKILL.md`（YAML frontmatter + markdown 主体），可选的 `references/`、`templates/`、`scripts/` 子目录存放补充材料。

## 来源

Skills 由 [Hermes Agent](https://github.com/toolazytoname/hermes) 编写/整理，在此处重组以便跨框架复用。Pilotdeck 是首个非 Hermes 的使用方。

## 许可证

MIT —— 详见 [LICENSE](./LICENSE)。
