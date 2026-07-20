# WebSplit

**One window for every web app, tool, and note you juggle.**

WebSplit is a cross‑platform desktop app that lets you run many live web pages side‑by‑side on a single zoomable, pannable canvas — alongside built‑in productivity widgets (notes, todos, kanban, whiteboard, timers, Git, an API tester, and more). Instead of drowning in browser tabs and separate apps, you arrange everything you need for a task in one **workspace**, switch between workspaces instantly, and pick up exactly where you left off.

It's **local‑first**: your workspaces, bookmarks, and widget content live on your machine, not in the cloud.

> This repository hosts packaged **releases** of WebSplit (macOS `.dmg` / `.zip`). Updates are delivered automatically in‑app.

---

## Highlights

- **Infinite canvas** — Drag, resize, and freely position widgets. Zoom and pan across a large workspace, snap widgets to halves/full‑screen, or run **Auto Tidy** to lay them out cleanly.
- **Live web widgets** — Embed any URL as a resizable webview. Run several web apps at once (docs, dashboards, chat, email) without tab clutter.
- **Multiple workspaces** — Group widgets by project or context and jump between them with `Cmd/Ctrl + 1–9` or the command palette.
- **Built‑in productivity widgets** — Notes, Todos, Kanban, Whiteboard, Focus/Pomodoro timer, Read‑Later clips, Image, Git, API Tester, iframe Compare, AI Chat, and fully Custom widgets.
- **Command palette** (`Cmd/Ctrl + K`) — Fuzzy‑search every action: create widgets, switch workspaces, toggle tools, run layout commands.
- **Bookmarks panel** — Organize pages into folders and spawn them as widgets in one click.
- **Design tools** — On‑screen **ruler**, **color picker** (copies to clipboard), and an **element inspector** for measuring and probing embedded pages.
- **Undo / redo** for workspace changes, plus one‑click **Undo** toasts for closed workspaces and removed widgets.
- **Memory Mode** — Soft‑delete workspaces into a restorable Trash instead of losing them.
- **AI automation (MCP)** — A built‑in Model Context Protocol server lets AI agents read and drive your workspaces, widgets, and embedded pages, gated by a policy you control.
- **Import / Export** — Save a workspace to a JSON file and load it on another machine.
- **Accessibility & performance** — High‑contrast mode, adjustable font scale, and a performance mode for heavier canvases.
- **Auto‑update** — New versions download and install in the background.

---

## Widgets

| Widget | What it does |
| --- | --- |
| **Web** | Embed any URL as a live, interactive webview. |
| **Notes** | Free‑form notes with backlinks to clipped web content. |
| **Todo** | Simple task list; convertible into a Kanban board. |
| **Kanban** | Columns and cards for tracking work. |
| **Whiteboard** | Sticky notes, shapes, and connecting arrows/lines for brainstorming. |
| **Focus Timer / Pomodoro** | Time‑boxed focus sessions. |
| **Read Later** | Clip selections from web widgets and turn them into notes. |
| **Image** | Pin images from a URL, file, or paste — cached locally for fast, offline display. |
| **Git** | View status, branches, and commits, and stage/commit for a local repository. |
| **API Tester** | Send HTTP requests (method, headers, body) and inspect responses. |
| **iframe Compare** | Load two URLs side‑by‑side for visual comparison. |
| **AI Chat** | Chat with an LLM (OpenAI, Anthropic, Ollama, OpenRouter, or a custom endpoint). |
| **Custom** | Build your own text / HTML / URL widget with custom title, icon, and fields. |

---

## Keyboard Shortcuts

**Workspaces**
- `Cmd/Ctrl + T` — New workspace
- `Cmd/Ctrl + W` — Close workspace
- `Cmd/Ctrl + 1–9` — Switch workspace

**Widgets**
- `Cmd/Ctrl + N` — New web widget
- `Cmd/Ctrl + Shift + N` — New notes widget
- `Cmd/Ctrl + Alt + K` — New kanban widget
- `Cmd/Ctrl + Alt + W` — New whiteboard widget
- `Cmd/Ctrl + Alt + G` — New git widget

**View & Navigation**
- `Cmd/Ctrl + K` — Command palette
- `Cmd/Ctrl + B` — Toggle bookmarks
- `Cmd/Ctrl + R` — Toggle ruler
- `Cmd/Ctrl + P` — Toggle color picker
- `Cmd/Ctrl + +` / `-` / `0` — Zoom in / out / reset
- `Cmd/Ctrl + Scroll` — Zoom at cursor
- `Shift + Drag` — Pan canvas
- `Cmd/Ctrl + /` — Show all shortcuts

**Layout snapping**
- `Cmd/Ctrl + Shift + ← / → / ↑ / ↓` — Snap to left / right / full / bottom

**History & files**
- `Cmd/Ctrl + Z` / `Cmd/Ctrl + Shift + Z` — Undo / redo
- `Cmd/Ctrl + Shift + E` / `Cmd/Ctrl + Shift + I` — Export / import workspace

**Accessibility**
- `Cmd/Ctrl + Alt + H` — High contrast
- `Cmd/Ctrl + Alt + +/-/0` — Font size up / down / reset
- `Cmd/Ctrl + Alt + M` — Performance mode

*(Move selected widgets with the arrow keys; hold `Shift` for larger steps.)*

---

## Installation (macOS)

1. Download the latest `WebSplit-<arch>.dmg` from the [Releases](../../releases) page — `arm64` for Apple Silicon, `x64` for Intel.
2. Open the `.dmg` and drag **WebSplit** into **Applications**.
3. Launch it. Builds are signed and notarized, so no Gatekeeper override is needed.

After the first launch, WebSplit checks for updates automatically and installs them in the background, so you stay on the latest version.

---

## Memory Mode

By default, closing a workspace removes it (with an instant **Undo** toast). Turn on **Memory Mode** (Options panel) to make deletions non‑destructive:

- Closed workspaces are **soft‑deleted into a durable Trash** instead of being discarded.
- Open the **Trash panel** to **restore** any workspace — its widgets and layout come back intact — or **purge** entries you no longer want (one at a time, or all at once).
- Trash lives locally, so it survives restarts.

Memory Mode also governs AI automation: when it's on, the MCP `delete_workspace` tool soft‑deletes to Trash rather than removing a workspace outright, so an agent can never permanently destroy your work without a separate purge.

---

## AI Automation (MCP)

WebSplit embeds a local **Model Context Protocol (MCP)** server, so AI agents and LLM tools can inspect and operate your workspace programmatically. It runs on loopback only (`127.0.0.1:4310` by default) and speaks JSON‑RPC over HTTP.

Two ways to use it, both from the **MCP Control panel**:

- **Agent mode** — Give a high‑level task in plain language (e.g. *"open the docs and screenshot the pricing table"*) and let the agent plan the tool calls.
- **Manual mode** — Invoke a single tool directly; the panel can copy a ready‑to‑run `cURL` for any tool.

The **AI Chat** widget can also call these tools directly when *Enable MCP tools* is turned on.

### Tool surface

| Area | Tools (examples) |
| --- | --- |
| **State** | `get_state`, `list_workspaces`, `list_widgets` |
| **Workspaces** | `create_workspace`, `rename_workspace`, `focus_workspace`, `delete_workspace` |
| **Trash (Memory Mode)** | `list_trash`, `restore_workspace`, `purge_trash` |
| **Widgets** | `create_widget_by_type`, `add_widget`, `update_widget`, `delete_widget` |
| **Notes / Todo / Kanban** | `notes.set_text`, `todo.add_task`, `kanban.add_card`, `kanban.move_card`, … |
| **Whiteboard / Read Later / API Tester / Image** | `whiteboard.add_item`, `readlater.add_clip`, `apitester.set_request`, `image.set_source`, … |
| **Browser control** | `web.open`, `web.click`, `web.type`, `web.read_snapshot`, `web.extract_links`, `web.screenshot`, … |

### Policy & safety

Every tool call passes through a policy **you configure** in the MCP Control panel:

- **Read‑only mode** — Blocks all state‑ and browser‑mutating tools. This is the **default in packaged builds**.
- **Browser control** — Off by default; enable to allow `web.*` tools to drive embedded pages.
- **Allowed origins** — An allow‑list restricting which sites browser tools may touch.
- **Destructive tools** — Disabled by default, with an option to require an explicit `confirm` flag when enabled.
- **Mutations are idempotent** (via idempotency keys) and versioned, and live UI updates stay in sync with disk.
- **Full audit log** — Every tool call is recorded locally (tool, status, timestamp, errors) and viewable in the panel.

---

## Licensing
