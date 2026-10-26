# Workspace Guidelines for Gemini in Antigravity

This workspace is configured with four key engineering superpowers:

## 1. Ponytail (Lazy Senior Developer & Anti-Overengineering)
- **Mindset**: The best code is the code you never wrote. Solve the task with the smallest complete change.
- **Rules**:
  1. Does it need to exist at all? (YAGNI).
  2. Already in codebase? Reuse existing helpers, patterns, and conventions.
  3. Platform/standard library provides it? Use native features before adding dependencies.
  4. Installed dependency solves it? Reuse it. Never add a dependency for a few lines.
  5. Shortest readable diff wins.
- **Accountability**: End code changes by stating what was skipped, edge cases checked, and any residual risks.
- *Active skill*: `ponytail`, `ponytail-review`, `ponytail-debt`.

## 2. Superpowers Engineering System
- **Investigation First**: Follow `systematic-debugging` before fixing bugs. Never guess.
- **Test-Driven Development**: Use `test-driven-development` (write test, watch fail, make pass, refactor).
- **Planning & Verification**: Follow `writing-plans` and `executing-plans` for non-trivial changes, followed by `verification-before-completion`.
- **Subagents**: Use `invoke_subagent` for parallel independent tasks and exploratory research.
- *Reference*: See `.agents/skills/using-superpowers/` and `.agents/rules/superpowers.md`.

## 3. Safe Chain (Dependency & Supply-Chain Security)
- **Zero Blind Installs**: Always check and install packages through Safe Chain (`npx safe-chain npm install <pkg>`).
- **Malware & Typosquat Protection**: Protect against compromised packages and unvetted packages < 48h old.
- *Active skill*: `safe-chain`.

## 4. UI/UX Pro Max (Design Intelligence & Front-End Excellence)
- **Mindset**: Interfaces must be beautiful, accessible, responsive, and grounded in design systems.
- **Search Tool**:
  ```powershell
  python .agents/skills/ui-ux-pro-max/scripts/search.py "<query>" --domain <domain>
  python .agents/skills/ui-ux-pro-max/scripts/search.py "<product_type>" --design-system
  ```
- **Domains**: `style`, `color`, `typography`, `ux`, `icons`, `chart`, `landing`, `web`.
- **Pre-delivery**: Check WCAG 4.5:1 contrast, keyboard focus rings, no emoji as icons, responsive viewports, and reduced motion.
- *Active skills*: `ui-ux-pro-max`, `ui-styling`, `design-system`, `design`, `brand`, `banner-design`, `slides`.
- *Rule*: `.agents/rules/ui-ux.md`.
