# Repository Guidelines

## Project Structure & Module Organization
This checkout has two repos layered together:

- Root: docs, workspace metadata, and the `src/` entrypoint.
- `src/`: the Chromium source repo.
- `src/brave/`: Brave-specific build scripts, branding, browser code, and patches.

Most BrowseX customization work belongs in `src/brave/`. Common paths:

- `src/brave/app/`: strings, icons, branding resources, packaging metadata.
- `src/brave/browser/`: browser UI, WebUI, omnibox, prefs, commands.
- `src/brave/components/`: shared features and build flags.
- `src/chrome/`: Chromium-side files overridden or patched by Brave.

## Build, Test, and Development Commands
Run commands from `src/brave` unless noted otherwise.

- `npm install`: install Node dependencies.
- `npm run init`: one-time bootstrap; syncs Chromium/DEPS and can take a long time.
- `npm run build`: build the default component/dev configuration.
- `npm run build Release`: build the optimized release configuration.
- `npm start` or `npm start Release`: launch the built app.
- `npm run create_dist -- Release --skip_signing`: create a local macOS package without signing.
- `npm run sync`: refresh dependencies after pulling upstream changes.
- `npm run test-unit`: run Jest tests.
- `npm run eslint`: lint JS/TS code.

## Coding Style & Naming Conventions
Follow existing file conventions before introducing new patterns.

- C++ uses Chromium/Brave style: 2-space indentation, descriptive `CamelCase` types, `kConstantName` constants.
- JS/TS/React should follow the local file style; prefer edits within existing components over broad rewrites.
- Keep user-facing branding/resource changes in `src/brave/app/` and feature gating in `src/brave/components/**/buildflags`.
- Do not rename internal Brave identifiers or `brave://` plumbing unless the task explicitly requires it.

## Testing Guidelines
Add or update targeted tests when behavior changes.

- Web/UI and TypeScript logic: `npm run test-unit`
- Scripts and Python helpers: `npm run test-python-scripts`
- Browser/UI changes: build and launch locally with `npm run build && npm start`

Name tests after the behavior under test, and keep new test files adjacent to the affected subsystem.

## Commit & Pull Request Guidelines
This checkout mixes a root repo and the nested `src` repo. Commit in the repo that actually owns the changed files.

- Prefer short, imperative commit messages, for example: `Disable desktop Rewards/Talk/VPN`.
- Keep commits scoped to one task and avoid mixing generated files with source edits.
- `src/` is often on detached `HEAD`; verify repo state before committing or pushing.
- PRs should summarize user-visible changes, touched platforms, validation performed, and remaining gaps.
