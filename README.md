# Canopy

**A readable map of how your JavaScript / TypeScript code actually works.**

![status](https://img.shields.io/badge/status-beta-orange) ![node](https://img.shields.io/badge/node-18%2B-green) ![runs](https://img.shields.io/badge/runs-locally-blue)

<!-- Add a screenshot: upload it to this repo (for example assets/map.png), then uncomment the next line -->
<!-- ![Canopy map](assets/map.png) -->

Most code tools show you a graph of everything. Canopy shows you the **story**: it starts where things begin (a web route, a socket message, a button click, a command) and follows what happens next, step by step, across files.

It updates itself every time you commit, so the map never goes stale.

> Canopy is in **beta (0.1.0)**. It works, it has rough edges, and your feedback shapes what comes next.

---

## What it looks like

Instead of a tangle of boxes, you get flows like this (illustrative example):

```
POST /signup                      (web route)
 ├─ validateInput                 src/validate.js
 ├─ createUser                    src/users.js
 │   └─ saveToDatabase            src/db.js
 └─ sendWelcomeEmail              src/mail.js
```

Open any step to see where it lives and what it connects to.

## Who it's for

- You just joined a codebase and need to understand it fast
- You're reviewing code you didn't write, including code written with AI
- You built something quickly and want to see what it actually does

## Install

You need **Node.js 18 or newer** (`node --version` to check). Then run:

```
npm install -g https://github.com/gouthamtg7/canopy-engine/releases/download/v0.1.0/canopy-engine-0.1.0.tgz
```

Installing takes well under a minute on a normal connection.

## Run it

Open a terminal in your project folder and type:

```
canopy
```

That one command checks your computer, looks at your project, prepares a `.canopy/` folder (kept out of git automatically), offers to add a commit hook, builds the map and opens it in your browser.

Want to point it at another folder? `canopy C:\path\to\project`

## Your first 5 minutes

1. Run `canopy` on a project you know well.
2. Start a timer when the map opens.
3. Pick a workflow and follow it. Does it match how you think the feature works?
4. After 5 minutes, write down in three sentences what the system does and where it starts.
5. Tell us how close you were. That's the most useful feedback we can get.

## Your code stays on your computer

- Canopy analyses your code **on your machine**.
- The engine makes **no network calls** (we test for this).
- The map is served on `127.0.0.1` only, so other computers on your network can't reach it.
- One honest detail: the map page loads two web fonts from Google when you're online. No code or project information is sent.

## Commands

| Command | What it does |
|---|---|
| `canopy` | Does everything in order and opens the map |
| `canopy sync` | Re-analyse the project (stores a new version if the code changed) |
| `canopy open` | Open the latest map |
| `canopy doctor` | Check that everything is set up correctly and say how to fix problems |
| `canopy history` | List stored versions |
| `canopy diff` | See what changed between two versions |
| `canopy hook install` | Update the map automatically after every commit and merge |
| `canopy hook uninstall` | Turn that off again |

The commit hook runs in the background and never blocks a commit.

## Known limits (beta)

We'd rather tell you than have you find out:

- **JavaScript and TypeScript only.** No Python, Go or other languages yet.
- **Connections between separate services are not linked yet.** For example, a frontend calling a backend over REST or WebSocket shows up as two separate maps, not one flow. This is our top priority.
- Method calls on objects (`thing.method()`) are only resolved in some cases.
- There is no search and no built-in code viewer yet.
- Very large projects (5,000+ files) can take several minutes.
- Flow-typed JavaScript is not supported.
- Tested on **Windows**. macOS and Linux testers are very welcome, but expect surprises.

## Troubleshooting

- **First step: run `canopy doctor`.** It tells you what's wrong and how to fix it.
- **`canopy` is not recognised:** close and reopen your terminal. If it still isn't found, your npm global folder isn't on your PATH (`npm config get prefix` shows where it is).
- **`canopy` runs something else:** there is an unrelated npm package that also installs a `canopy` command. Uninstall it, or run Canopy with `npx --yes <the install URL above>`.
- **Permission error on install (macOS/Linux):** try `npx --yes <the install URL above>` instead of a global install.
- Still stuck? Paste the output of `canopy doctor` into the feedback form or open an issue.

## Update or remove

- **Update:** run the install command again with the newer version from the [Releases](../../releases) page.
- **Remove Canopy:** `npm uninstall -g canopy-engine`
- **Remove it from a project:** run `canopy hook uninstall`, then delete the `.canopy/` folder.

## Feedback and bugs

- **Feedback form (takes 5 minutes):** https://forms.gle/UX17FaE8HXLH8esB9
- **Bugs:** open an [issue](../../issues). Say what you clicked, what you expected, and paste `canopy doctor`.

## About this repo

This repo holds **downloads, documentation and issue tracking**. The source code is not published here.

## Terms

Canopy is proprietary beta software, provided "as is" without warranty. It's free for personal and internal evaluation. Reselling it, redistributing it, offering it as a hosted service, or reverse engineering it is not allowed. See the `LICENSE` file inside the package. All rights reserved. © 2026 gouthamtg7.
