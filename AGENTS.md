# Repository Guidelines

## Project Structure & Module Organization
This repository is a Brave browser checkout with two important layers:

- Root: build orchestration, docs, and the Chromium checkout entrypoint.
- `src/`: the Chromium source repo.
- `src/brave/`: Brave-specific code, patches, build scripts, branding, and product features.

Most custom product work happens in `src/brave/`. Examples:

- `src/brave/app/`: branded strings, resources, app metadata.
- `src/brave/browser/`: browser UI, features, prefs, WebUI.
- `src/brave/components/`: shared components and feature build flags.
- `src/brave/patches/`: Chromium patch overlays.

## Build, Test, and Development Commands
Run commands from `src/brave` unless noted otherwise.

- `npm install`: install Node dependencies.
- `npm run init`: initial sync of Chromium, DEPS, and Brave dependencies.
- `npm run build`: build the default component configuration.
- `npm run build Release`: build the release configuration.
- `npm start [Release|Component|Debug]`: launch the built browser.
- `npm run sync`: refresh Brave/Chromium dependencies after pulling changes.
- `npm run apply_patches`: reapply patch files when patch-only changes were made.
- `npm run test-unit`: run Jest unit tests.
- `npm run eslint`: run JavaScript/TypeScript linting.
- `npm run format`: run the repo formatting script.

## Coding Style & Naming Conventions
Follow existing file conventions before introducing new patterns.

- C++ uses Chromium/Brave style: 2-space indentation, descriptive `CamelCase` types, `kConstantName` constants.
- JS/TS/React code should match the local file style; prefer existing naming and directory structure over inventing new abstractions.
- Keep branding/resource edits localized to `src/brave/app/` and feature gating in `src/brave/components/**/buildflags`.

## Testing Guidelines
Add or update targeted tests when behavior changes.

- Web/UI and TypeScript logic: `npm run test-unit`
- Lint and script validation: `npm run eslint`, `npm run test-python-scripts`
- Large browser changes should be smoke-tested by building and launching locally.

Name tests after the behavior under test, and keep new test files adjacent to the affected subsystem.

## Commit & Pull Request Guidelines
This checkout mixes a root repo and the nested `src` repo. Commit in the repo that actually owns the changed files.

- Prefer short, imperative commit messages, for example: `Disable desktop Rewards/Talk/VPN` or `Rebrand desktop UI to BrowseX`.
- Keep commits scoped to one task.
- PRs should summarize user-visible changes, touched platforms, validation performed, and any known gaps (for example, untranslated strings or unchanged internal identifiers).
