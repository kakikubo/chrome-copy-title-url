# Repository Guidelines

## Project Structure & Module Organization
- `info.plist` holds every Alfred node (hotkey trigger, AppleScript action, clipboard + notification outputs). Edit it with Alfred’s workflow editor or a plist-aware editor to avoid corrupting IDs.
- `Chrome-Copy-Title-URL.alfredworkflow` is the distributable zip bundle; rebuild it whenever `info.plist` changes.
- `README.md` documents usage, install steps, and must stay aligned with the hotkey and workflow behavior.

## Build, Test, and Development Commands
- `plutil -lint info.plist` verifies plist syntax before packaging.
- `zip -r Chrome-Copy-Title-URL.alfredworkflow info.plist README.md` regenerates the workflow file for release testing.
- `osascript -e 'tell application "Google Chrome" ...'` lets you dry-run modified AppleScript logic directly in the terminal (copy the script body from `info.plist`).

## Coding Style & Naming Conventions
- AppleScript blocks use two-space indentation and descriptive variable names (`u` for URL is established; keep it consistent).
- Workflow object UIDs follow the UUID format already present; duplicate a node inside Alfred if you need a new UID instead of hand-editing.
- Markdown uses ATX headings, fenced code blocks, and inline backticks for shortcuts.

## Testing Guidelines
- After packaging, import the workflow in Alfred, ensure Chrome has multiple windows, and confirm the script always returns the active tab from each window.
- Confirm clipboard output equals `Title URL` (single space) and that the “Copied!” notification still fires.
- Manual checks should cover hotkey reassignment (default `Cmd+Ctrl+C`) and Automation permissions under macOS System Settings.

## Commit & Pull Request Guidelines
- Follow the existing history style: concise summary plus context (e.g., `複数ウィンドウに対応するため…`), optionally mention version bumps (`v1.1.0`).
- Reference related issues or release goals in the body, list reproduction steps, include Alfred screenshots if UI wiring changes, and attach the rebuilt `.alfredworkflow` when proposing releases.
- Describe manual test steps (Chrome version, macOS build, Alfred version) so reviewers can reproduce quickly.

## Security & Configuration Tips
- Never commit personal API keys or Alfred license data.
- Remind contributors to re-authorize Alfred → Chrome automation after macOS or Chrome updates to avoid silent AppleScript failures.
