---
layout: page
title: "From Zero to Plugins Admin: How to Ship a Notepad++ Plugin"
date: 2026-11-09
permalink: /npp-plugin-zero-to-plugins-admin/
---

# From Zero to Plugins Admin: How to Ship a Notepad++ Plugin

Notepad++ has over 100 plugins in its official Plugins Admin list, and every one of them got there the same way: a DLL with six exports, a GitHub release, and a pull request to the plugin list repository. There is no submission form, no review queue you can pay to skip, and no shortcut around the checklist. Here is the whole path, including the two mistakes that send most first-time submissions back.

## What a plugin actually is

A Notepad++ plugin is a Windows DLL that exports six functions Notepad++ looks up when it loads:

- `setInfo`, `getName`, `getFuncsArray`, `beNotified`, `messageProc`, `isUnicode`

`getName` returns the display name. `getFuncsArray` returns the menu items — each one a label plus a function pointer. `beNotified` receives editor events (file opened, text changed, selection changed). The rest is plumbing. If any export is missing or misspelled, Notepad++ silently ignores the DLL. No error message, no log entry — it just does not appear in the menu. That silence is the first trap: when your plugin does not show up, check the exports first, with a tool like `dumpbin /exports` or Dependencies, before touching anything else.

You also need a version resource (`.rc` file) with the same version number you will put in your submission. A mismatch between the DLL version and the submitted version is one of the standard reasons a pull request gets sent back.

## Building it without a Visual Studio project

You do not need a `.vcxproj` or a full Visual Studio install. The free Visual Studio 2022 Build Tools (C++ workload) plus one command is enough:

```powershell
cl /LD /O2 PluginMain.cpp /link /OUT:MyPlugin.dll
```

Build both architectures — Notepad++ ships x86 and x64, and Plugins Admin requires both. Ship the two DLLs in one zip per architecture, or one zip containing both; the list entry points at a release zip per architecture. Tag the release in GitHub (e.g. `v1.0.0`), let CI build both architectures, and attach the zips to the release. A GitHub Actions workflow that builds on tag push and creates the release with SHA-256 hashes is the reliable way to do this — doing it by hand on your own machine is how the wrong file ends up in the release.

One real-world gotcha: automation that writes files into `.github/workflows/` does not always land — the file can report success and still not be there. If you use a bot or API to create the workflow file, verify it exists in the repository afterwards, and if in doubt commit it through the GitHub web UI.

## Testing before you submit

Before you write the submission, prove the DLL loads:

1. **Export check** — all six exports present, `getName` returns the right string, `getFuncsArray` returns your menu items.
2. **Load test** — a small test program loads the DLL, calls the exports, and checks the counts. You can test editor logic without opening Notepad++ at all by stubbing the Scintilla interface with a fake header — the real plugin this guide is based on caught a hand-copied header bug exactly this way (the test passed against the same wrong header, so the test alone was not enough; the values had to be checked against the official headers).
3. **Real-machine test** — install the DLL into a real Notepad++ (`%ProgramFiles%\Notepad++\plugins\MyPlugin\MyPlugin.dll`), restart, and click every menu item. A plugin that only ever ran in a test harness has not been tested.

## The submission: a pull request to nppPluginList

The official list lives in the `notepad-plus-plus/nppPluginList` repository. You fork it, add one JSON entry to `src/plist/x64.json` (and `x86.json` if you ship 32-bit), and open a pull request. The entry looks like this:

```json
{
  "folder-name": "MyPlugin",
  "display-name": "My Plugin",
  "version": "1.0.0",
  "id": "<sha-256 of the release zip>",
  "repository": "https://github.com/<you>/my-plugin",
  "description": "One line, what it does.",
  "author": "Your Name",
  "homepage": "https://github.com/<you>/my-plugin"
}
```

Two details that send PRs back:

- **`id` is the SHA-256 hash of the zip file, not the DLL.** Hash the exact file attached to the GitHub release. Hashing the DLL inside the zip gives a different value and the automated check fails.
- **The version in the JSON must match the DLL's version resource and the release tag.** All three must agree, or the checks fail.

When the three automated checks go green, a maintainer merges it, and your plugin appears in Plugins Admin on the next Notepad++ release cycle. From pull request to listed is usually days, not weeks — if the checks are green.

## A checklist before you submit

- [ ] All six exports present and spelled exactly right
- [ ] Both x86 and x64 DLLs built from the same source, same version
- [ ] Version resource matches the release tag matches the JSON entry
- [ ] `id` is the SHA-256 of the release zip, not the DLL
- [ ] Release zips attached to the GitHub release, not just built locally
- [ ] DLL load-tested and clicked through on a real Notepad++ install
- [ ] `repository` and `homepage` links actually open
- [ ] Description is one honest line — no "best", no "fastest", no claims you cannot prove

## The shortcut: the skeleton, build, and checklist ready to go

If you would rather not assemble all of this from forum posts and a half-remembered wiki page, I packaged the exact setup from a plugin that actually made it into Plugins Admin: a hello-world plugin with all six exports, the minimal headers with values verified against the official ones, a one-command build for x86 and x64, the DLL load test, the fake-Scintilla test pattern, the tag-to-release GitHub Actions workflow, a step-by-step walkthrough including the gotchas above, and a printable pre-submission checklist.

It does not contain anyone else's plugin — the guide's example plugin is free and open source, and you download it free if you want the feature. You are buying the guide and the skeleton for building your own.

**Notepad++ Plugin Starter Kit — $29:** https://zhgaleaf.gumroad.com/l/tbpdkw

Shipping a plugin is mostly checklist work. Get the exports right, get the hash right, test it on a real machine, and the list takes care of the rest.
