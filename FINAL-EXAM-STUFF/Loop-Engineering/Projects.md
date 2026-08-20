# Loop Engineering — Practice Projects Guide

A complete, beginner-friendly, hands-on record of everything practiced in the "Hands-on mentor for agentfactory-labs repository" session. This guide follows the **Loop Engineering Crash Course** (`panaversity/agentfactory-labs`) and documents **8 projects total**: 5 core "loop heartbeat" projects + 3 supporting concept mini-projects, in the order they were actually built (easy → hard).

> **Source repo used throughout:** `https://github.com/panaversity/agentfactory-labs` (folder: `crash-course/loop-eng`)
> **Course page:** `https://agentfactory.panaversity.org/docs/loop-engineering-crash-course`
> **Final personal repo (example from the session):** `https://github.com/ISMAIL-AHMED-SHAH/Loop-Eng-Practice`
> **Tool used throughout:** Claude Code (the CLI, invoked as `claude` in a terminal)

---

## Table of Contents

1. [Big-Picture Overview: What Is "Loop Engineering"?](#big-picture-overview)
2. [Global Prerequisites](#global-prerequisites)
3. [Project 1 — iss-loop (In-session loop)](#project-1--iss-loop)
4. [Project 2 — portfolio-starter (Conditional loop / `/goal`)](#project-2--portfolio-starter)
5. [Project 3 — sky-watch (Scheduled loop)](#project-3--sky-watch)
6. [Project 4 — doorbell (Event-driven loop)](#project-4--doorbell)
7. [Project 5 — paper-watch (The Spine / memory)](#project-5--paper-watch)
8. [Project 6 — worktree-practice (Isolation)](#project-6--worktree-practice)
9. [Project 7 — subagent-practice (Maker–checker split)](#project-7--subagent-practice)
10. [Project 8 — connector-practice (Action / external API)](#project-8--connector-practice)
11. [Combining Everything Into One Repo](#combining-everything-into-one-repo)
12. [Master Table — All 8 Projects at a Glance](#master-table)
13. [Global Common Errors & Fixes](#global-common-errors--fixes)
14. [Overall Key Takeaways](#overall-key-takeaways)
15. [Practice Challenges / Next Steps](#practice-challenges--next-steps)

---

<a name="big-picture-overview"></a>
## 1. Big-Picture Overview: What Is "Loop Engineering"?

An AI agent (Claude Code) becomes far more useful when it doesn't just answer one question and stop — it **loops**: repeats an action, checks a condition, and continues (or stops) based on real feedback. This course teaches the different "heartbeats" that can drive a loop, plus supporting concepts needed to build safe, working agent loops.

| Heartbeat / Concept | What starts each repeat | Project that teaches it |
|---|---|---|
| In-session loop | A timer, while you watch | `iss-loop` |
| Conditional loop (run-until-done) | A goal / check script | `portfolio-starter` |
| Scheduled loop | A calendar/cron schedule | `sky-watch` |
| Event-driven loop | An external event (e.g. a pull request) | `doorbell` |
| The Spine (memory) | A memory file read every run | `paper-watch` |
| Isolation | Parallel work without collisions | `worktree-practice` |
| Maker–checker split | A separate reviewing agent | `subagent-practice` |
| Action / connectors | Reaching outside the local files | `connector-practice` |

`Needs Verification`: The exact numbered "concept" labels (4, 5, 6, 7, 12) referenced against each project came from the session's own README summary table and correspond to sections of the crash-course docs page — the underlying course text itself was not fully retrieved, so treat these numbers as the session's own labels, not independently confirmed section numbers.

---

<a name="global-prerequisites"></a>
## 2. Global Prerequisites

These applied across **all 8 projects**:

| Requirement | Why | How to check |
|---|---|---|
| Git installed | Cloning the course repo, version control | `git --version` |
| Claude Code CLI installed | Running `/loop`, `/goal`, subagents, etc. | `claude --version` |
| A terminal (PowerShell used throughout in this session — Windows environment) | Running all commands | N/A |
| A GitHub account | Pushing your own practice repo; needed for `doorbell` | N/A |
| Python 3 installed correctly on PATH | `portfolio-starter` and `sky-watch` scripts | `python --version` |

**Environment-specific note:** This entire session was carried out on **Windows** using **PowerShell**, with the practice repo cloned to a local drive (e.g. `D:\Loop-Engineering\...`). Commands shown below are PowerShell/Windows-flavored. Mac/Linux users will need to translate `type` → `cat`, `notepad` → any text editor, `xcopy` → `cp -r`, `.bat` scripts → shell scripts, and Task Scheduler → `cron`.

### Step 0 — Clone the course repo

```powershell
cd Desktop
git clone https://github.com/panaversity/agentfactory-labs.git
cd agentfactory-labs/crash-course/loop-eng
```

Inside `loop-eng/` you'll find one subfolder per core project: `iss-loop`, `portfolio-starter`, `sky-watch`, `doorbell`, `paper-watch`.

### Difficulty ladder (as confirmed from the repo's own project structure)

| Level | Project |
|---|---|
| 🟢 Easy | `iss-loop` |
| 🟡 Medium | `portfolio-starter` |
| 🟡 Medium | `sky-watch` |
| 🔴 Hard | `doorbell` |
| 🔴 Hard | `paper-watch` |

---

<a name="project-1--iss-loop"></a>
## 3. Project 1 — `iss-loop` (In-session loop)

### 1. Project Name & Purpose
Track the **real**, live position of the International Space Station using a simple `/loop` command in Claude Code. Teaches the simplest kind of loop: one that runs only **while your session/terminal is open**.

### 2. Concepts Learned
- **In-session loops**: they run on a timer inside your live terminal session and die the instant the session/terminal closes.
- Loops can have a **built-in stopping condition** (a "goal"), not just a timer — turning a simple loop into a conditional one.
- Real vs simulated data: the ISS is a genuine satellite; the script calls a live public API, not fake/dummy data.

### 3. Tools/Technologies Used
- Claude Code CLI (`/loop` slash command)
- Public API: `api.wheretheiss.at` (real-time ISS telemetry)
- A pre-built Claude Code **Skill** already shipped in the repo: `.claude/skills/iss-position/` (containing `SKILL.md` and `scripts/iss.py`)

### 4. Prerequisites
- `git` and `claude` installed and working (`git --version`, `claude --version`)
- No GitHub account, API key, or token needed — the simplest project in the set

### 5. Project Structure
```
iss-loop/
├── .claude/
│   ├── settings.json
│   └── skills/
│       └── iss-position/
│           ├── SKILL.md
│           └── scripts/
│               └── iss.py
├── .gitignore
├── AGENTS.md
├── CLAUDE.md
└── README.md
```

### 6. Step-by-Step Implementation

**Step 1 — Check prerequisites**
```powershell
git --version
claude --version
```

**Step 2 — Clone and enter the folder**
```powershell
cd Desktop
git clone https://github.com/panaversity/agentfactory-labs.git
cd agentfactory-labs/crash-course/loop-eng/iss-loop
```

**Step 3 — Start Claude Code inside the folder**
```powershell
claude
```

**Step 4 — Run the basic in-session loop**
```
/loop
```
(Confirmed in the session to fetch the ISS's real position every minute and print it live.)

**Step 5 — Let it run for 2–3 update cycles (do not type anything)**, then press `Esc` to stop the loop.

### 7. All Important Commands and Configurations
| Command | Purpose |
|---|---|
| `git --version` / `claude --version` | Verify prerequisites |
| `git clone https://github.com/panaversity/agentfactory-labs.git` | Get the course repo |
| `claude` | Launch Claude Code in the project folder |
| `/loop` | Start the basic in-session loop |
| `/loop 1m show me where the ISS is and what country or ocean it is flying over` | Loop with a richer per-tick instruction |
| `/loop 1m track the ISS and shout ARRIVED when it has travelled 20 degrees from where it started` | Loop with a **stopping condition** (conditional-loop-style) |
| `Esc` | Manually stop a running loop |

### 8. How to Run and Test
Run `/loop`, watch at least 2–3 live updates print automatically (roughly once a minute), then press `Esc`.

To test the conditional version, run the 20-degree challenge command and watch it work **without you touching anything** until it self-reports `ARRIVED` and cancels its own scheduled job.

### 9. Expected Output/Result
A live-updating panel showing something like:
```
🛰  INTERNATIONAL SPACE STATION            live · 12:28:29 UTC
──────────────────────────────────────────────────────────
   Position    51.7° N      44.3° W
   Altitude    421 km       Speed       27,601 km/h   (7.67 km/s)
   Sunlight    in sunlight
──────────────────────────────────────────────────────────
Deep in the North Atlantic, roughly halfway between Newfoundland and Ireland.
```
For the 20° challenge, it eventually prints an `ARRIVED` message and automatically cancels its own scheduled job (e.g. `CronDelete(...)` → `Cancelled`).

### 10. Common Errors & Fixes
| Error | Cause | Fix |
|---|---|---|
| `claude` fails to connect / times out | A local `settings.json` had been silently rerouted through a local proxy (`ANTHROPIC_BASE_URL` pointing at `http://localhost:20128/v1` with a Gemini model override, e.g. `gc/gemini-3-pro-preview`) | Open `%USERPROFILE%\.claude\settings.json`, delete the proxy override keys (`ANTHROPIC_BASE_URL`, `ANTHROPIC_AUTH_TOKEN`, `ANTHROPIC_DEFAULT_*_MODEL`), keep only harmless keys like `"skipDangerousModePermissionPrompt": true`. **JSON files do not support `//` comments** — lines must be fully deleted, not commented out. |

### 11. Key Takeaways
- Closing the terminal **kills the loop** — that's the whole lesson of an in-session loop.
- A loop can have either a **timer-based** stop (manual `Esc`) or a **condition-based** stop (a goal it checks each tick).
- Real live public APIs can be wired into a loop just as easily as fake data.

### 12. Practice Challenges / Next Steps
- Try changing the interval (`/loop 5m ...`) and observe the difference.
- Try a different real public API of your choice as a loop target.
- Move on to a loop that must satisfy a **checklist**, not just a single condition — see Project 2.

---

<a name="project-2--portfolio-starter"></a>
## 4. Project 2 — `portfolio-starter` (Conditional loop / `/goal`)

### 1. Project Name & Purpose
Generate a full personal portfolio **website** from your real CV/résumé, using Claude Code's `/goal` command. Instead of manual turn-by-turn prompting, you hand Claude a goal and a **pass/fail checklist**, and it writes → checks → fixes → re-checks **on its own**, in a loop, until the goal is genuinely true (or a retry cap is hit).

### 2. Concepts Learned
- **Conditional loops (run-until-done)**: stop when a condition is true, not when a timer expires.
- Automated checking (`check.py`) combined with a **separate reviewer agent** for subjective/judgment criteria — an early preview of the maker–checker pattern used more explicitly in Project 7.
- Setting **retry caps** (e.g. "stop after 15 check attempts or 3 review rounds") so a goal-driven loop can't run forever.
- Privacy-consciousness: deliberately excluding sensitive personal data (NIC number, father's name, full home address) from a *public* deliverable even though it was present in the *private* source CV.

### 3. Tools/Technologies Used
- Claude Code CLI (`/goal` slash command)
- Python 3 (`check.py`, an automated checklist script provided by the repo)
- A CV/résumé file (PDF recommended and easiest — Claude Code can read PDFs directly; `.docx`/`.txt`/`.md` also work)

### 4. Prerequisites
- Working Python 3 installation **on PATH** (this tripped up the session — see Common Errors)
- A CV/résumé file to feed in
- `spec.md` and `check.py` already present in the repo's `portfolio-starter/` folder

### 5. Project Structure
```
portfolio-starter/
├── check.py
├── spec.md
├── resume.pdf          # <- you add this
├── site/                # <- generated output goes here
│   ├── index.html
│   └── style.css
├── content.md
├── design.md
├── profile.md
└── progress.md          # written if the retry cap is hit
```

### 6. Step-by-Step Implementation

**Step 1 — Run the checker first (expected to fail — proves the checklist works)**
```powershell
cd ..\portfolio-starter
python3 check.py site
```
(If `python3` isn't recognized on Windows, try `python check.py site`.)

**Step 2 — Add your résumé file**
Place your CV as `resume.pdf` (or similar) directly inside the `portfolio-starter/` folder using File Explorer (drag-and-drop into a terminal only pastes the *path*, not the file).

**Step 3 — Launch Claude Code in the folder**
```powershell
claude
```

**Step 4 — Give it the goal (adjust the filename and privacy instructions to match your own CV)**
```
/goal Build my portfolio in site/ from resume.pdf, following spec.md. Do not include my NIC number, father's name, or full home address anywhere on the site. Done when `python check.py site` prints 20/20 and the reviewer agent replies PASS on all six judgment promises — show me both. Stop after 15 check attempts or 3 review rounds and write what is still failing to progress.md.
```

**Step 5 — Let it run.** Claude reads the résumé, decides on content/design, builds the page, runs the checker, fixes issues, and repeats until it passes or hits the cap.

### 7. All Important Commands and Configurations
| Command | Purpose |
|---|---|
| `python3 check.py site` / `python check.py site` | Run the automated 20-point checklist against the generated site |
| `claude` | Launch Claude Code |
| `/goal ...` | Hand Claude a goal + stopping condition; it loops internally until satisfied |

### 8. How to Run and Test
After the `/goal` run finishes, confirm both success signals are shown:
1. `python check.py site` prints **20/20**
2. The separate reviewer agent replies **PASS** on all **6 judgment criteria**

### 9. Expected Output/Result
A complete, working personal portfolio website in `site/` (HTML + CSS), built entirely from your résumé content, passing all 20 automated checks and all 6 reviewer judgment criteria — with sensitive personal identifiers deliberately excluded.

### 10. Common Errors & Fixes
| Error | Cause | Fix |
|---|---|---|
| `Python was not found; run without arguments to install from the Microsoft Store...` | Windows has a stub `python` command that redirects to the Microsoft Store instead of running real Python | Check for an alternate command: `python --version`, `py --version`; install a real Python if neither works |
| Dragging résumé into VS Code terminal doesn't add the file | Dragging into a terminal pastes the file **path** as text, not the actual file | Use File Explorer to physically copy/drag the file into the `portfolio-starter` folder |

### 11. Key Takeaways
- A loop's "done" condition can combine an **objective script check** and a **subjective agent review** — this is a lightweight preview of maker–checker separation.
- Setting explicit retry caps (attempts/rounds) prevents a goal-driven agent from looping forever.
- Always think about what personal data should *not* end up in a public deliverable, even if it's present in your private source material.

### 12. Practice Challenges / Next Steps
- Re-run `/goal` with a stricter checklist (add your own custom checks to `check.py`).
- Try feeding in a `.docx` or `.txt` résumé instead of a PDF.
- Try lowering the retry cap and observe what `progress.md` records when the cap is hit before success.

---

<a name="project-3--sky-watch"></a>
## 5. Project 3 — `sky-watch` (Scheduled loop)

### 1. Project Name & Purpose
Build a **daily automatic asteroid-forecast** notifier using NASA's real near-Earth-object data — a loop that is started by a **schedule** (a clock), not by you sitting at the terminal.

### 2. Concepts Learned
- **Scheduled loops**: a calendar-based trigger (cloud "Routine" or a local OS scheduler) starts the loop instead of a human or a live session.
- **Cloud vs local execution trade-offs**: cloud schedules run even if your laptop is off, but may be restricted by a sandboxed network allowlist; local schedules have full network access but only run while your machine is on.
- **"No false all-clear" safety design**: if the data source is unreachable, the script must report failure honestly (e.g. by email) instead of silently pretending everything is fine.

### 3. Tools/Technologies Used
- Claude Code **Routines** (cloud-based scheduled trigger) — attempted first
- Gmail connector (for the cloud Routine's email delivery)
- **Windows Task Scheduler** (final, working solution)
- Python script: `.claude/skills/sky-watch/scripts/skywatch.py`
- Public API: NASA's near-Earth-object / asteroid feed (`api.nasa.gov`)

### 4. Prerequisites
- Working Python 3 on PATH
- (For the cloud Routine attempt) a connected Gmail account
- Windows Task Scheduler available (Windows only — Linux/Mac users would use `cron` instead — `Needs Verification` for exact Mac/Linux equivalent commands, not covered in the session)

### 5. Project Structure
```
sky-watch/
├── .claude/
│   └── skills/
│       └── sky-watch/
│           └── scripts/
│               └── skywatch.py
├── run-skywatch.bat        # <- created during this session
├── skywatch-log.txt        # <- created by scheduled runs
└── README.md
```

### 6. Step-by-Step Implementation

**Step 1 — Attempt a cloud Routine first**
Inside Claude Code, ask it to set up a daily scheduled Routine (e.g. "create a daily routine that checks NASA's asteroid feed and emails me the forecast"). In this session it was created successfully as a scheduled trigger running daily at local midnight, delivering by email via the Gmail connector.

**Step 2 — Test the Routine immediately (don't wait 24 hours)**
```
run the Daily Sky Watch routine now
```

**Result in this session:** the cloud Routine correctly **failed safely** — it emailed *"Sky Watch could not run today — NASA's asteroid feed was unreachable (network fetch failed after 3 tries)"* rather than a false all-clear.

**Step 3 — Diagnose the cloud failure**
Confirmed via research: Claude Code cloud Routines run in a sandbox with a **preset domain allowlist** that does not currently support arbitrary external domains like `api.nasa.gov`, with no self-serve way to add it. `Needs Verification`: this is a platform limitation as understood in this session (Aug 2026); it may change over time — check current Anthropic documentation.

**Step 4 — Delete the broken cloud Routine** (via the Routines web page trash icon) and fall back to local scheduling.

**Step 5 — Test the script directly, locally, first**
```powershell
cd D:\Loop-Engineering\agentfactory-labs\crash-course\loop-eng\sky-watch
$env:PYTHONIOENCODING="utf-8"
python .claude\skills\sky-watch\scripts\skywatch.py --days 1
```

**Step 6 — Create a `.bat` wrapper script**
```powershell
notepad run-skywatch.bat
```
Paste:
```bat
@echo off
cd /d D:\Loop-Engineering\agentfactory-labs\crash-course\loop-eng\sky-watch
set PYTHONIOENCODING=utf-8
python .claude\skills\sky-watch\scripts\skywatch.py --days 1 >> skywatch-log.txt 2>&1
```

**Step 7 — Create a Windows Task Scheduler task**
1. Press **Win** key → type `Task Scheduler` → open it
2. **Create Basic Task** (or **Create Task** for the advanced tabbed version) → name it `Daily Sky Watch`
3. **Trigger:** Daily, start time `12:00:00 AM`
4. **Action:** Start a program → Browse to `run-skywatch.bat`
5. Save

**Step 8 — Test it manually**
Right-click the task in Task Scheduler → **Run**, then check `skywatch-log.txt` for output.

### 7. All Important Commands and Configurations
| Command | Purpose |
|---|---|
| `run the Daily Sky Watch routine now` | Manually trigger a cloud Routine test run (doesn't count against daily limit) |
| `$env:PYTHONIOENCODING="utf-8"` | Fix encoding issues before running the Python script directly |
| `python .claude\skills\sky-watch\scripts\skywatch.py --days 1` | Run the forecast script directly for N days ahead (1–7 valid) |
| Windows Task Scheduler GUI steps (see above) | Set up the local daily schedule |

### 8. How to Run and Test
Right-click the created Task Scheduler task → **Run**, then open `skywatch-log.txt` to confirm fresh output was appended.

### 9. Expected Output/Result
```
☄  SKY WATCH — today, 2026-08-15
──────────────────────────────────────────────────────────────
   ✓  Nothing flagged hazardous in the window.
   Closest pass:  2017 AV3  on 2026-08-15
      42,346,250 km  =  110.2× the Moon
      ~308–689 m across, 89,666 km/h
   3 close approaches today.
──────────────────────────────────────────────────────────────
```

### 10. Common Errors & Fixes
| Error | Cause | Fix |
|---|---|---|
| `--days needs a number from 1 to 7.` | Stray extra character typed after the number (e.g. `--days 1j`) | Re-type the command carefully, e.g. `--days 1` |
| Cloud Routine emails "watch could not run" / NASA feed unreachable | Anthropic's cloud sandbox network allowlist doesn't (yet) support arbitrary domains like `api.nasa.gov` | Delete the cloud Routine; use a **local** scheduler (Task Scheduler / cron) instead, which has full network access |
| Garbled/encoding-related console output | Windows console encoding mismatch | Set `$env:PYTHONIOENCODING="utf-8"` before running the script (make permanent in shell profile if desired) |

### 11. Key Takeaways
- A "scheduled loop" just means: **something other than you** (a clock) starts each run.
- Cloud-hosted schedules run even when your machine is off, but may be **sandboxed** — always verify network reachability rather than assuming.
- A well-designed scheduled job should **fail loudly and honestly**, never silently pretend success.

### 12. Practice Challenges / Next Steps
- Try scheduling a different time of day and confirm via the log file.
- Add a second `.bat`/scheduled task with a different `--days` value.
- (Linux/Mac users) Replicate this using `cron` instead of Task Scheduler — `Needs Verification`, not tested in this session.

---

<a name="project-4--doorbell"></a>
## 6. Project 4 — `doorbell` (Event-driven loop)

### 1. Project Name & Purpose
Automatically review every **pull request** in a GitHub repo using Claude, running entirely on **GitHub's own servers** — a loop triggered by an external *event* (a PR being opened/updated), with zero manual triggering and zero involvement of your local machine.

### 2. Concepts Learned
- **Event-driven loops**: an external event (not a timer, not you) starts each run.
- GitHub Actions + `anthropics/claude-code-action` integration.
- **"A green checkmark does not mean it worked"** — you must actually check that the review *comment* was posted, not just that the workflow *ran*.
- Using `claude setup-token` to generate a Claude Code OAuth token specifically for use in CI/CD, kept as a GitHub Actions secret (never shared).

### 3. Tools/Technologies Used
- GitHub Actions (`.github/workflows/doorbell.yml`)
- `anthropics/claude-code-action@v1` (the official GitHub Action)
- Claude Code CLI's `claude setup-token` command
- Git branches and pull requests

### 4. Prerequisites
- A GitHub account and a repo you control (pushed from your local clone)
- `claude setup-token` run successfully once
- A repo-level GitHub Actions secret configured

### 5. Project Structure
```
your-repo/
├── .github/
│   └── workflows/
│       └── doorbell.yml     # must stay at repo root, NOT inside a subfolder
├── readings.py               # example file used to introduce a bug
└── README.md
```

**Important note from this session:** the `.github` folder **must remain at the repository root**. Moving it into a subfolder (e.g. `doorbell/.github/`) makes GitHub Actions stop seeing it — PR reviews would silently stop firing.

### 6. Step-by-Step Implementation

**Step 1 — Confirm the workflow file's contents**
```powershell
notepad .github\workflows\doorbell.yml
```
Confirmed working configuration from this session:
```yaml
name: Doorbell
on:
  pull_request:
    types: [opened, synchronize]
jobs:
  review:
    runs-on: ubuntu-latest
    permissions:
      contents: read
      pull-requests: write
      id-token: write
      actions: read
    steps:
      - uses: actions/checkout@v6
        with:
          fetch-depth: 1
      - uses: anthropics/claude-code-action@v1
        with:
          claude_code_oauth_token: ${{ secrets.CLAUDE_CODE_OAUTH_TOKEN }}
          github_token: ${{ secrets.GITHUB_TOKEN }}
          track_progress: true
          prompt: |
            Review the changes in this pull request for bugs. Be brief:
            name the bug, say why it is wrong, and stop.
            Refer to the specific commits in this PR by their short hash when
            explaining what changed.
```

**Step 2 — Generate a Claude Code OAuth token for CI**
```powershell
claude setup-token
```
This opens a browser to authorize, then prints a token. **Keep this token private** — never paste it into chat or commit it to the repo.

**Step 3 — Add the token as a GitHub repo secret**
1. Go to your repo on GitHub → **Settings**
2. **Secrets and variables** → **Actions**
3. **New repository secret**
4. Name: `CLAUDE_CODE_OAUTH_TOKEN`
5. Value: paste the token
6. **Add secret**

**Step 4 — Introduce a real, deliberate bug to trigger a review**

Example bug used in this session — original `readings.py`:
```python
"""Altitude readings from the International Space Station, in kilometres."""
READINGS = [421.4, 423.1, 419.8, 424.6, 422.0]

def highest(readings):
    """The highest altitude in the list."""
    return max(readings)

def lowest(readings):
    """The lowest altitude in the list."""
    return min(readings)
```
Introduce the bug by changing `lowest()`'s `return min(readings)` to `return max(readings)` (makes `lowest()` incorrectly identical to `highest()`).

**Step 5 — Create a branch, commit, push**
```powershell
git checkout -b fix-lowest-bug
notepad readings.py     # make the min -> max edit
git add .
git commit -m "Fix lowest reading calculation"
git push -u origin fix-lowest-bug
```

**Step 6 — Open the pull request**
Click the URL GitHub prints after the push (e.g. `.../pull/new/fix-lowest-bug`), give it a title, click **Create pull request**.

**Step 7 — Wait ~1 minute, then verify the actual review comment posted** (not just a green checkmark) — scroll up on the PR page to find a comment from the GitHub Actions bot.

**Step 8 — (Optional) Merge the PR** to close it out.

### 7. All Important Commands and Configurations
| Command | Purpose |
|---|---|
| `claude setup-token` | Generate a Claude Code OAuth token for CI use |
| `git checkout -b <branch>` | Create a branch to introduce the test bug |
| `git push -u origin <branch>` | Push the branch and trigger a PR link |
| GitHub web UI: Settings → Secrets and variables → Actions | Store `CLAUDE_CODE_OAUTH_TOKEN` securely |

### 8. How to Run and Test
Open a real pull request with a real bug and confirm, within about a minute, that a bot-authored review comment appears (not just a passing check).

### 9. Expected Output/Result
A PR comment from `github-actions (Bot)` that names the exact bug, references the exact short commit hash (e.g. `fdc71fc`), and explains why it's wrong — e.g. correctly identifying that swapping `min`→`max` makes `lowest()` behave identically to `highest()`.

### 10. Common Errors & Fixes
| Error | Cause | Fix |
|---|---|---|
| Workflow shows "Successful" but no review comment appears | A passing/green Action run only confirms the workflow *executed*, not that it *did the right thing* | Always scroll up/check the PR conversation for an actual bot comment, don't trust the checkmark alone |
| PR review never fires at all | `.github/workflows/doorbell.yml` was moved into a subfolder instead of staying at repo root | Move `.github` back to the repository root with `git mv <subfolder>\.github .github` |

### 11. Key Takeaways
- An event-driven loop is triggered by something happening in the world (a PR), with **zero manual prompting**.
- CI-based agent reviews run on **remote servers**, completely independent of your local machine being on.
- Passing status checks are not proof of correct behavior — always verify the actual output/artifact.

### 12. Practice Challenges / Next Steps
- Introduce a different class of bug (off-by-one, wrong comparison operator) and see if the review catches it.
- Extend the workflow to trigger on `pull_request.closed` as well and post a summary.
- Have someone else (a classmate) open a PR against your repo to prove the doorbell works without you at all.

---

<a name="project-5--paper-watch"></a>
## 7. Project 5 — `paper-watch` (The Spine — memory between runs)

### 1. Project Name & Purpose
Watch arXiv for new papers on a topic (e.g. "LLM agents"), but **remember** what's already been shown — so a second run on the same topic reports "nothing new" instead of repeating itself. This teaches "the spine": a persistent memory file that survives between separate runs of a loop.

### 2. Concepts Learned
- **The Spine**: a loop is only as good as its memory. Without a persisted record of prior results, every run looks like the first run.
- "No spine, no loop": deleting the memory file makes every item look new again — proving the memory *is* the mechanism, not just a nice-to-have.
- Diagnosing and permanently fixing an SSL certificate verification issue in Python.

### 3. Tools/Technologies Used
- Claude Code CLI
- Python's `urllib.request.urlopen` (used directly by the script — notably **not** routed through the `requests`/`certifi` stack automatically)
- `certifi` (Python package providing a trusted CA bundle)
- arXiv's public listing/API
- `progress.md` (the "spine" file)

### 4. Prerequisites
- Python 3 installed
- `certifi` installed (`pip install certifi` if missing) — `Needs Verification`: exact install command not explicitly shown in the session, but referenced as the source of the CA bundle used

### 5. Project Structure
```
paper-watch/
├── .claude/
│   └── skills/
│       └── paper-watch/ (script location referenced, exact path not fully captured)
├── progress.md     # the SPINE — the loop's memory
└── README.md
```

### 6. Step-by-Step Implementation

**Step 1 — Run the paper-watch script/skill for the first time.** In this session it initially failed with an SSL error.

**Step 2 — Diagnose the SSL error**
Root cause identified: the script uses plain `urllib.request.urlopen(...)`, which does **not** automatically use `certifi`'s CA bundle (unlike some HTTP libraries). Simply upgrading `certifi` alone did not fix it.

**Step 3 — Fix for the current session (temporary)**
Point the environment variable at certifi's bundle for the current session only:
```
SSL_CERT_FILE = <path to certifi's CA bundle>
```
(In this session, Claude Code set this directly; the equivalent PowerShell command would be `$env:SSL_CERT_FILE = (python -m certifi)` — `Needs Verification`, the literal command used inside the Claude Code session wasn't shown verbatim.)

**Step 4 — Make the fix permanent**
Tell Claude Code:
```
yes, set SSL_CERT_FILE in my user environment permanently
```
This sets `SSL_CERT_FILE` in the **user environment** (takes effect in new terminals/apps after restart or re-login).

**Step 5 — Run the watcher successfully**
Confirmed output: a full list of ~20 new papers (titles, dates, categories, arXiv links) printed and saved to `progress.md`.

**Step 6 — Prove the spine by re-running immediately**
Run the exact same query again. Expected/confirmed result: **"nothing new since last run."**

**Step 7 — Inspect the spine file directly**
```powershell
cat progress.md
```
Confirmed contents begin with an explanatory header:
```
# progress.md — the SPINE (this loop's memory)
# The papers below have already been shown to you. paper-watch reads this
# file first, so each run shows only what is NEW. Delete it and every paper
# looks new again — that is "no spine, no loop".
```

**Step 8 (optional/destructive test) — Delete `progress.md` and re-run** to observe every paper appearing "new" again — this is the core lesson made tangible.

### 7. All Important Commands and Configurations
| Command | Purpose |
|---|---|
| `cat progress.md` (or `type progress.md` on Windows) | Inspect the spine/memory file |
| Setting `SSL_CERT_FILE` (session and permanent) | Fix `CERTIFICATE_VERIFY_FAILED` errors |

### 8. How to Run and Test
Run the watcher twice in a row on the same topic. First run: prints new papers and writes `progress.md`. Second run: reports nothing new. Delete `progress.md` and run a third time: everything looks new again.

### 9. Expected Output/Result
First run — a formatted list of papers, e.g.:
```
Title: LLMs Are Not Good Strategists, Yet Memory-Enhanced Agency Boosts Reasoning
Date: 2026-08-12
Category: cs.CL
Link: arxiv.org/abs/2608.12626
────────────────────────────────────────
```
Second run (same query) — a short "nothing new since last run" message.

### 10. Common Errors & Fixes
| Error | Cause | Fix |
|---|---|---|
| `CERTIFICATE_VERIFY_FAILED` | The script's `urllib.request.urlopen` call doesn't automatically trust `certifi`'s CA bundle | Point `SSL_CERT_FILE` explicitly at certifi's bundle path; make permanent via user environment variables so it doesn't need re-setting every session |
| Upgrading `certifi` alone doesn't fix the SSL error | `certifi` upgrade only updates the bundle *file* — nothing wires `urllib` to use it automatically | Explicitly set `SSL_CERT_FILE`, or patch the script to reference certifi's bundle directly |

### 11. Key Takeaways
- A loop without memory repeats itself forever — memory is what turns repetition into genuine *progress*.
- Memory can be as simple as a plain Markdown/text file read at the start of every run.
- Deleting the memory file is a fast, safe way to *prove* that memory is doing real work, not just decoration.

### 12. Practice Challenges / Next Steps
- Point `paper-watch` at a different topic/query and confirm a separate, independent memory trail.
- Try corrupting (not deleting) `progress.md` and see how the script behaves.
- Combine this with a scheduled loop (Project 3's pattern) to build a fully automatic, memory-aware daily paper digest.

---

<a name="project-6--worktree-practice"></a>
## 8. Project 6 — `worktree-practice` (Isolation)

### 1. Project Name & Purpose
Prove that **two agents (or two Claude Code sessions) can safely edit the same repository at the same time** without stepping on each other, using Git's `worktree` feature — separate working folders, same underlying `.git` history.

### 2. Concepts Learned
- **Isolation**: `git worktree` lets multiple branches be checked out into separate folders simultaneously, from one shared repo.
- Worktrees prevent *accidental overwrites while working*, but **merging is still a separate, deliberate step** where real conflicts can (and should) surface.
- Git only tracks **commits**, not just saved files — edits sitting uncommitted in a worktree won't show up in a merge.
- Claude Code itself can automatically create worktrees/branches for isolated task work (observed as a related, separate phenomenon in another part of the overall practice).

### 3. Tools/Technologies Used
- Git (`git worktree`, `git branch`, `git merge`)
- Two parallel Claude Code sessions (one per worktree)

### 4. Prerequisites
- Git installed
- Comfort running two terminal sessions/tabs at once

### 5. Project Structure
```
Loop-Eng-Practice/
├── worktree-practice/      # original repo + main worktree
│   └── shared.py
├── worktree-a/               # separate worktree, branch feature-a
└── worktree-b/               # separate worktree, branch feature-b
```

### 6. Step-by-Step Implementation

**Step 1 — Create the exercise folder and initial commit**
```powershell
cd D:\Loop-Engineering\Loop-Eng-Practice
mkdir worktree-practice
cd worktree-practice
git init
echo "# Shared file both agents will try to edit" > shared.py
echo "def greet(): return 'hello'" >> shared.py
git add .
git commit -m "Initial commit for worktree practice"
```

**Step 2 — Create two branches and two worktrees**
```powershell
git branch feature-a
git branch feature-b
git worktree add ..\worktree-a feature-a
git worktree add ..\worktree-b feature-b
```

**Step 3 — Verify the shared file has real content**
```powershell
type shared.py
```

**Step 4 — Open two separate Claude Code sessions**, one inside `worktree-a` and one inside `worktree-b`. Have each session add a **different** function to `shared.py` (e.g. one agent adds `add_numbers`, the other adds `subtract_numbers`) — working simultaneously, with zero interference.

**Step 5 — Commit each worktree's changes on its own branch**

Terminal 1 (`worktree-a`):
```powershell
git add .
git commit -m "Add add_numbers function"
```
Terminal 2 (`worktree-b`):
```powershell
git add .
git commit -m "Add subtract_numbers function"
```

**Step 6 — Merge both branches back into the main worktree**
```powershell
cd D:\Loop-Engineering\Loop-Eng-Practice\worktree-practice
git merge feature-a
git merge feature-b
type shared.py
```

**Step 7 — If a real conflict occurs** (both branches touched the same lines, or the file was flagged as binary due to an encoding quirk from PowerShell's `echo`):
```powershell
git status
notepad shared.py
```
Manually edit the file to include **all** contributions, then:
```powershell
git add shared.py
git commit -m "Merge feature-a and feature-b"
type shared.py
```

**Step 8 — Clean up the worktrees**
```powershell
cd D:\Loop-Engineering\Loop-Eng-Practice\worktree-practice
git worktree remove ..\worktree-a
git worktree remove ..\worktree-b
```

### 7. All Important Commands and Configurations
| Command | Purpose |
|---|---|
| `git worktree add <path> <branch>` | Create a new isolated working folder on a given branch |
| `git worktree list` | List all active worktrees |
| `git worktree remove <path>` | Remove a worktree when done |
| `git merge <branch>` | Merge a branch's committed changes |
| `git status` | Inspect unresolved merge conflicts |

### 8. How to Run and Test
After both branches are committed and merged, `type shared.py` (or `cat shared.py`) should show **all** functions written by both parallel sessions.

### 9. Expected Output/Result
```python
# Shared file both agents will try to edit
def greet(): return 'hello'
def add_numbers(a, b): return a + b
def subtract_numbers(a, b): return a - b
```

### 10. Common Errors & Fixes
| Error | Cause | Fix |
|---|---|---|
| Merge reports "Already up to date" but new functions are missing | Changes were saved to disk in the worktree but never actually **committed** on that branch | Run `git add . && git commit -m "..."` inside each worktree before merging |
| `Cannot merge binary files: shared.py` / conflict markers don't show in the file | PowerShell's `echo` wrote the file in an encoding (e.g. UTF-16) that Git misreads as binary | Run `git status` to confirm the real unmerged-paths conflict, then manually rewrite the file's final correct content and `git add` it |
| Accidentally ran `git init` a second time inside an already-tracked folder (nested repo mistake) | Created a stray inner `.git` folder | Remove the inner `.git` directory and re-track the files normally in the outer repo |
| A stray/extra Claude Code worktree appears unexpectedly (e.g. `.claude/worktrees/...`) | Claude Code itself can auto-create an isolated worktree for a task, or a second session got triggered accidentally | Close the stray session, then `git worktree remove --force <path>`; explicitly tell Claude Code "work directly on master, don't create a new worktree" going forward |

### 11. Key Takeaways
- Worktrees give true **parallel, non-interfering** editing of the same repository.
- The payoff/complexity of isolation shows up at **merge time**, not while working — plan for real conflict resolution.
- Only committed work is visible to `git merge` — uncommitted edits are invisible to it.

### 12. Practice Challenges / Next Steps
- Deliberately make both branches edit the **same line** to force a text-based conflict and practice resolving it with conflict markers (`<<<<<<<`, `=======`, `>>>>>>>`).
- Try three simultaneous worktrees/branches instead of two.
- Explore Claude Code's own automatic worktree behavior for isolated task execution and when it helps vs. adds confusion for a single-session workflow.

---

<a name="project-7--subagent-practice"></a>
## 9. Project 7 — `subagent-practice` (Maker–checker split)

### 1. Project Name & Purpose
Build a custom, **read-only** subagent ("checker") that reviews code written by the main agent ("maker") — without ever being able to edit anything itself. This is the maker–checker pattern in its purest, hand-built form.

### 2. Concepts Learned
- **Subagents**: Claude Code supports defining custom, purpose-scoped agents with restricted tool access.
- **Maker–checker separation**: one agent builds/writes, a **separate**, more restricted agent reviews — never the same agent grading its own work.
- Custom subagent definitions (`.claude/agents/*.md`) only load **at session start** — a Claude Code restart is required before a newly created subagent becomes callable.
- Restricting an agent's `tools:` list (e.g. `Read, Grep, Glob` only, no `Edit`/`Write`) is what actually enforces "read-only" — not just an instruction in prose.

### 3. Tools/Technologies Used
- Claude Code CLI, custom **subagent** definitions
- Markdown-based agent definition file (`.claude/agents/checker.md`)
- A simple Python file (`calculator.py`) as the reviewed artifact

### 4. Prerequisites
- Claude Code installed and working
- Comfort restarting a Claude Code session when instructed

### 5. Project Structure
```
subagent-practice/
├── .claude/
│   └── agents/
│       └── checker.md
└── calculator.py
```

### 6. Step-by-Step Implementation

**Step 1 — Create the project folder and start Claude Code**
```powershell
cd D:\Loop-Engineering\Loop-Eng-Practice
mkdir subagent-practice
cd subagent-practice
claude
```

**Step 2 — Define the checker subagent**
Type into Claude Code:
```
Create a subagent called "checker" whose only job is to review Python code for bugs and style issues. It should NOT be allowed to edit files — only read and report problems. Save it properly as a subagent definition in this project.
```
Confirmed result — a file created at `.claude/agents/checker.md` with front-matter restricting it to:
```yaml
---
name: checker
tools: Read, Grep, Glob
---
```
(Description text specified it should only activate for explicit Python review requests, checking for correctness bugs, mutable default args, unclosed resources, etc.)

**Step 3 — Create the "maker" task with a deliberate bug**
```
Write a Python file called calculator.py with a function divide(a, b) that returns a / b. Deliberately don't handle division by zero — I want a real bug for the checker to catch.
```
Result:
```python
def divide(a, b):
    return a / b
```

**Step 4 — Call the checker subagent**
```
Use the checker subagent to review calculator.py
```
**Note:** if the subagent was just created in this same session, you may need to **restart Claude Code** first — subagent definitions only load at session start.

**Step 5 — Review the checker's findings** (confirmed in this session):
1. No division-by-zero handling — unhandled `ZeroDivisionError`
2. Missing type hints
3. Missing docstring
The checker explicitly confirmed it made **no changes**, being read-only.

**Step 6 — Hand the fix back to the main agent (the maker)**
```
yes, fix these issues
```
Confirmed resulting fix:
```python
def divide(a: float, b: float) -> float:
    """Divide a by b, raising ValueError if b is zero."""
    if b == 0:
        raise ValueError("Cannot divide by zero")
    return a / b
```

**Step 7 — Re-run the checker to verify the fix**
```
Use the checker subagent to review calculator.py again
```
Expected: a clean report, no remaining issues.

### 7. All Important Commands and Configurations
| Command | Purpose |
|---|---|
| `Create a subagent called "checker" ... only read and report ...` | Natural-language instruction that generates `.claude/agents/checker.md` |
| `Use the checker subagent to review calculator.py` | Invoke the named subagent on a specific file |
| Subagent YAML front-matter `tools: Read, Grep, Glob` | Enforces the read-only restriction at the tool-permission level |

### 8. How to Run and Test
Write a file with a deliberate bug, have the checker subagent review it (expect it to flag the bug and make zero edits), have the maker fix it, then re-run the checker to confirm a clean pass.

### 9. Expected Output/Result
- First checker run: a findings list citing the exact bug + 2 style improvements, explicitly stating no changes were made.
- After the fix: a second checker run reporting no remaining issues.

### 10. Common Errors & Fixes
| Error | Cause | Fix |
|---|---|---|
| "checker" subagent not recognized/callable right after creation | Custom subagent definitions (`.claude/agents/*.md`) only load at **session start** | Restart the Claude Code session, then retry `Use the checker subagent to review ...` |

### 11. Key Takeaways
- True maker–checker separation is enforced by **restricting the checker's available tools**, not just by prompting it to "only read."
- A subagent should always explicitly confirm it made no unauthorized changes.
- This exact pattern (a restricted reviewer agent + automated checks) is what `portfolio-starter` used internally in Project 2 — here it was built from scratch by hand.

### 12. Practice Challenges / Next Steps
- Create a second subagent (e.g. "security-checker") scoped to a different concern.
- Try giving the checker `Edit` access by mistake and observe whether/how it changes behavior — then correct it back.
- Chain checker → maker → checker into an automated loop (combining this with Project 2's conditional-loop pattern).

---

<a name="project-8--connector-practice"></a>
## 10. Project 8 — `connector-practice` (Action / connectors)

### 1. Project Name & Purpose
Give Claude Code real "hands" — the ability to **act** outside the local filesystem by reaching out to a live external API (GitHub's), rather than only reading/writing local files. This is the "action" layer of an agent loop.

### 2. Concepts Learned
- The distinction between a true **MCP connector** (OAuth-based, like the Gmail/GitHub App connectors used in Projects 3 and 4) and a simpler fallback like **WebFetch** hitting a public REST API.
- **Agent adaptability**: when the "ideal" tool (`gh` CLI) isn't installed, a well-built agent finds another working path instead of just failing.
- The importance of **saving a record** of an exercise, even a purely conversational one, so it's reflected in a submittable repo.

### 3. Tools/Technologies Used
- Claude Code CLI, **WebFetch** tool (built-in)
- GitHub's public REST API (used as a fallback, since `gh` CLI / a dedicated GitHub MCP connector wasn't available in this environment)

### 4. Prerequisites
- Claude Code installed
- (Ideally) GitHub CLI (`gh`) or a GitHub MCP connector — **not required**, since this session demonstrated the fallback path when neither was available

### 5. Project Structure
```
connector-practice/
└── result.md      # summary written after the exercise, since nothing else was saved to disk
```

### 6. Step-by-Step Implementation

**Step 1 — Create the project folder and start Claude Code**
```powershell
cd D:\Loop-Engineering\Loop-Eng-Practice
mkdir connector-practice
cd connector-practice
claude
```

**Step 2 — Ask Claude to take a real external action**
```
Using GitHub, list my 5 most recently updated repositories with their last commit date.
```
Result in this session: `gh --version` was checked and not found on PATH, and no GitHub-specific connector tool was available — Claude Code **fell back to GitHub's public REST API via WebFetch** and successfully listed real repositories with real timestamps.

**Step 3 — Save a written record of the exercise** (since the task was purely conversational and produced no file on its own):
```
Save a summary of this GitHub API exercise into a file called result.md — include the command used, the note about no gh CLI/connector being available, and the table of 5 repos you found.
```

**Step 4 — Commit and push**
```powershell
cd D:\Loop-Engineering\Loop-Eng-Practice
git add connector-practice
git commit -m "Add connector/action practice project (WebFetch to GitHub API)"
git push
```

### 7. All Important Commands and Configurations
| Command | Purpose |
|---|---|
| `gh --version` | Check whether the GitHub CLI is available |
| `Using GitHub, list my 5 most recently updated repositories...` | Natural-language instruction triggering an external "action" |
| `Save a summary of this ... into a file called result.md` | Persist a conversational-only exercise into the repo |

### 8. How to Run and Test
Confirm the agent successfully returns real, current repository data (names + real last-updated timestamps) rather than an error or fabricated data, and that `result.md` accurately documents the fallback path taken.

### 9. Expected Output/Result
A `result.md` file documenting:
- The task
- A note that no `gh` CLI or GitHub MCP connector was available
- The exact command/approach used (WebFetch → GitHub public API)
- A table of the 5 most recently updated repositories with real commit dates

### 10. Common Errors & Fixes
| Error | Cause | Fix |
|---|---|---|
| `connector-practice` folder empty when trying to commit | The exercise was purely conversational — nothing was written to disk automatically | Explicitly ask Claude to write a summary file (e.g. `result.md`) before committing |
| `gh` CLI unavailable / no GitHub MCP connector configured | Environment didn't have these installed/connected | Accept the WebFetch-based fallback as a valid proxy for the "action" concept; document the caveat honestly rather than treating it as a full MCP connector |

### 11. Key Takeaways
- "Action" simply means the agent does something **beyond the local filesystem** — the specific mechanism (true MCP connector vs. a REST fallback via WebFetch) can vary based on what's available.
- Good agents adapt gracefully when a preferred tool is missing, rather than failing outright.
- If an exercise doesn't naturally produce a file, deliberately ask for one so your work is captured and reproducible.

### 12. Practice Challenges / Next Steps
- If you have `gh` CLI or a real GitHub MCP connector available, redo this exercise and compare the experience/output to the WebFetch fallback.
- Try a different external API (e.g. weather, a public dataset) as the "action" target.
- Combine this with Project 4 (`doorbell`) to have an event-driven loop that also takes an external action (e.g. posting to a different service) after a review.

---

<a name="combining-everything-into-one-repo"></a>
## 11. Combining Everything Into One Repo

Once all 8 projects were individually completed (in separate locations under the cloned course repo and separate practice folders), they were combined into a single personal submission repo.

### Steps used in this session

**Step 1 — Create subfolders in the target repo**
```powershell
cd D:\Loop-Engineering\Loop-Eng-Practice
mkdir iss-loop, portfolio-starter, sky-watch, paper-watch
```

**Step 2 — Copy each finished project's files in**
```powershell
xcopy /E /I /Y ..\agentfactory-labs\crash-course\loop-eng\iss-loop iss-loop
xcopy /E /I /Y ..\agentfactory-labs\crash-course\loop-eng\portfolio-starter portfolio-starter
xcopy /E /I /Y ..\agentfactory-labs\crash-course\loop-eng\sky-watch sky-watch
xcopy /E /I /Y ..\agentfactory-labs\crash-course\loop-eng\paper-watch paper-watch
```
(`doorbell` was already in the target repo from earlier steps, since its GitHub Actions workflow had to live there from the start.)

**Step 3 — Commit and push everything**
```powershell
git add .
git commit -m "Add all 5 loop engineering practice projects"
git push
```

**Step 4 — Add a top-level `README.md`** summarizing all 8 projects (core + concept mini-projects), including a "Notable debugging along the way" section and a privacy note about the portfolio site — see the [Master Table](#master-table) below for the equivalent content.

**Note on Windows line endings:** Git may print warnings like `LF will be replaced by CRLF the next time Git touches it` when adding files — this is informational, not an error, and doesn't block the commit.

---

<a name="master-table"></a>
## 12. Master Table — All 8 Projects at a Glance

| # | Project | Heartbeat / Concept | What It Proves |
|---|---|---|---|
| 1 | `iss-loop` | In-session loop | `/loop` fetches the real ISS position every minute, live, while the terminal stays open; closing the terminal kills the loop. |
| 2 | `portfolio-starter` | Conditional loop (`/goal`) | Builds a full portfolio site from a CV, checks it against 20 automated checks + a separate reviewer agent (6 judgment criteria), and retries until both pass. |
| 3 | `sky-watch` | Scheduled loop | A daily asteroid-forecast loop; tried as a cloud Routine (blocked by sandbox network limits), then set up as a local Task Scheduler job hitting NASA's real API. |
| 4 | `doorbell` | Event-driven loop | A GitHub Actions workflow reviews every pull request automatically; proven with a real bug (`min`→`max` swap), caught and correctly explained, citing the exact commit hash. |
| 5 | `paper-watch` | The Spine (memory) | An arXiv paper watcher backed by `progress.md`; second run on the same topic returns "nothing new"; deleting `progress.md` makes every paper look new again — "no spine, no loop." |
| 6 | `worktree-practice` | Isolation | Two Claude Code sessions edit the same repo, same file, at the same time, on separate `git worktree`s and branches, then merge (surfacing and resolving a real conflict). |
| 7 | `subagent-practice` | Maker–checker split | A custom read-only `checker` subagent (`Read`, `Grep`, `Glob` only) reviews code, catches a deliberate bug, and confirms the fix afterward without ever editing the file itself. |
| 8 | `connector-practice` | Action / connectors | Claude reaches outside the local filesystem to a live external API (GitHub's) and takes real action, adapting when the ideal tool (`gh` CLI) wasn't installed. |

---

<a name="global-common-errors--fixes"></a>
## 13. Global Common Errors & Fixes

| Symptom | Root Cause | Fix |
|---|---|---|
| Claude Code fails to connect / behaves oddly across projects | `%USERPROFILE%\.claude\settings.json` had been silently rerouted through a local proxy to a non-Anthropic model (`gc/gemini-3-pro-preview`) via `ANTHROPIC_BASE_URL` | Remove the proxy override keys from `settings.json`, keep only intended settings |
| `CERTIFICATE_VERIFY_FAILED` in Python scripts | `urllib.request.urlopen` doesn't automatically use `certifi`'s CA bundle | Set `SSL_CERT_FILE` to point at certifi's bundle (temporarily, then permanently in the user environment) |
| Cloud-based scheduled automation (Routines) can't reach a needed external API | Cloud sandbox has a fixed domain allowlist with no self-serve way to add new domains | Fall back to a local scheduler (Task Scheduler / cron) which has unrestricted network access |
| A GitHub Actions-based automation silently stops working after reorganizing files | `.github/workflows/` was accidentally moved out of the repository root | Keep `.github` at the repo root always; use `git mv` to move it back if needed |
| A newly created custom subagent isn't recognized | Subagent definitions only load at Claude Code session start | Restart the Claude Code session before invoking a newly created subagent |
| `python`/`python3` "not found" on Windows | Windows Store stub intercepting the command instead of a real Python install | Try `python --version` / `py --version`; install a genuine Python distribution if neither resolves |
| Git reports odd "0 insertions" or binary-file merge conflicts on simple text files | PowerShell's `echo`/redirection can write files in an unexpected encoding (e.g. UTF-16) | Verify actual content with `type`/`cat`; resolve conflicts by manually rewriting the file's final content when markers don't render properly |

---

<a name="overall-key-takeaways"></a>
## 14. Overall Key Takeaways

- **A "loop" is defined by what starts each repeat**: you (in-session), a goal/check (conditional), a clock (scheduled), or an external event (event-driven) — and its usefulness over time depends on whether it has **memory** (the spine).
- **Safety and honesty matter as much as functionality**: a good loop fails loudly and informatively (e.g. sky-watch's "could not run" email) rather than silently pretending success.
- **Maker–checker separation** (a restricted, read-only reviewer) is a recurring pattern across multiple projects (`portfolio-starter`'s reviewer agent, `subagent-practice`'s `checker`, `doorbell`'s automated PR review) — it shows up in different forms but is the same underlying idea.
- **Isolation (worktrees) and action (connectors)** round out the picture: agents can work in parallel without collisions, and can reach beyond the local filesystem to actually *do* things in the world.
- **Debugging is part of the curriculum**: proxy misconfiguration, SSL errors, sandbox network limits, encoding quirks, and subagent load timing were all real obstacles solved during these projects, not hypothetical edge cases.

---

<a name="practice-challenges--next-steps"></a>
## 15. Practice Challenges / Next Steps

1. **Combine heartbeats**: build a scheduled loop (like `sky-watch`) that also has a memory spine (like `paper-watch`), so it only alerts you about genuinely new hazardous asteroids, not repeats.
2. **Combine maker–checker with event-driven**: extend `doorbell` so that after the automated review, a second job attempts an automatic fix and opens a follow-up PR (maker step after the checker step).
3. **Multi-agent worktrees**: try three or more parallel Claude Code sessions on three worktrees/branches of the same repo, each building an independent feature, then merge all three.
4. **Real MCP connector**: if available, redo `connector-practice` with an actual OAuth-based MCP connector (not just WebFetch) and compare the experience.
5. **Package and present**: write your own top-level `README.md` summarizing all 8 projects (see the [Master Table](#master-table) as a template) for a portfolio or classroom submission.
6. **Explore beyond this course**: the crash-course page lists additional short conceptual exercises beyond the 8 built here — revisit `https://agentfactory.panaversity.org/docs/loop-engineering-crash-course#practice-projects` for anything further. `Needs Verification`: the full text of that "Practice projects" section was not completely retrievable during this session due to page length, so treat it as a starting point for further exploration, not a complete task list.

---
