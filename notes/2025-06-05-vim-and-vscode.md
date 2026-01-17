---
slug: vim-and-vscode-2025-06-05
title: Vim and VSCode – Reflection of a Lifelong Vim User
date: 2025-06-05
tags: [note, vim, vscode, productivity, reflection]
status: draft
---

## Context

I've been using Vim for most of my life — it's muscle memory, an extension of my hands,
and deeply woven into how I think and write code.

But over the last few months, I gave `VSCode` a real chance. It’s a modern,
popular editor built with technologies I actually like: Electron, JS, and the Node ecosystem.
I wanted to see if it could genuinely improve or simplify my workflow without sacrificing
the things I care about.

This note specifically reflects on using VSCode with the **VSCodeVim** extension installed,
trying to recreate my Vim habits within the VSCode environment.

<!-- truncate -->

---

## Why I Used VSCode

- The integration: Git, Docker, debugging, extensions — all in one place.
- Native support for Markdown preview, REST clients, DevContainers, etc.
- Great for multi-language projects and modern stack tooling.
- Easier onboarding for teammates, clients, and future collaborators.

---

## What I Appreciated in VSCode

- Command pallete, moder and powerful.
- Built-in terminal, file tree.
- Extensions that just work out of the box (Copilot, Prettier, ESLint).
- Workspace and project-based setup makes context switching smoother.

---

## Difficulties and Friction

### cmd mode

One of the most jarring differences is **command-line mode**.  
In `Vim` it shows an **interactive list of matching files and directories** — like a shell.
This is essential when navigating large projects with deeply nested structures.

In **VSCodeVim**, `<Tab>` still completes filenames, but only one by one —
**it does not show a list of available completions**. There's no `wildmenu`, no dropdown,
no visual overview.  The underlying reason is that VSCode doesn’t expose a real terminal-backed
command-line UI to extensions, so the Vim emulation layer has no way to present completions like
native Vim does.

**Relative path issue**  
The lack of true cmd mode brings a problem with paths as well.  
`Vim` searches using :pwd (the working directory). This is usually the root of project.
`VSCodeVim` paths are resolved relative to the currently open file's path.

In `Vim` in order to open file relatively i use custom `abbreviatures` like `:ee`, `:spp`,
`:vss`, `tabee`.

#### Workaround

The most effective workaround is to **avoid `:e` altogether** and use VSCode’s native `Ctrl+P`
file picker. It offers fuzzy matching, instant preview, and integrates cleanly with the project root.
Once a file is selected, it can be opened in a split using `Ctrl+\` (vertical) or
`Ctrl+Enter` (preserve current tab). It’s fast, visual, and more in line with how modern editors 
are expected to behave.

### Ctrl-P and :find

WIP...