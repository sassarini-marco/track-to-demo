# track-to-demo

**From a challenge to a working prototype and a pitch deck, in one day, with Claude doing the heavy lifting.**

You get a challenge (a hackathon "track", a brief, a spec). By the end of the day your team has:

- a short shared plan everyone agrees on (`BRIEF.md`);
- a few design ideas, and one final design picked by the team;
- a working prototype inside your own code repository, tested;
- a slide deck for the demo, on your company template if you have one.

You don't need to know how to write prompts. You type a few short commands and Claude asks you only what it can't figure out by itself.

---

## What you need before starting

| What | Why | How to check |
|---|---|---|
| **Claude Code** (terminal or the Code tab of the Claude Desktop app) | The plugin runs inside it | Type `claude` in a terminal |
| **A claude.ai account**, logged in | Design boards and the slide deck live on claude.ai | Inside Claude Code, type `/login` |
| **Your team in the same claude.ai organization** | So you can share boards with each other | Ask whoever manages your claude.ai account |
| **A folder with your project** (it can be empty) | The prototype is built there | Open the folder in a terminal |
| **Google Chrome** (optional but recommended) | Claude checks the app in the browser | Start Claude with `claude --chrome` |

No claude.ai login? It still works: the design ideas become pages of your app instead of boards, and the deck stops at the outline and script.

---

## Setup (once per person, ~5 minutes)

Copy and paste each block, one at a time, in order. When a step says *"inside Claude Code"*, paste it where you chat with Claude. When it says *"in a terminal"*, paste it in a normal terminal window.

### Step 1: start Claude Code with the browser enabled

In a terminal, inside your project folder:

```
claude --chrome
```

Then, inside Claude Code, log in to claude.ai (skip it if you are already logged in):

```
/login
```

### Step 2: install the plugin (required)

Inside Claude Code:

```
/plugin marketplace add sassarini-marco/track-to-demo
```

```
/plugin install track-to-demo@track-to-demo
```

### Step 3: install the recommended helpers

These are optional, but the results are much better with them. Inside Claude Code, one line at a time:

```
/plugin install frontend-design@claude-plugins-official
```

```
/plugin marketplace add pbakaus/impeccable
```

```
/plugin install impeccable@impeccable
```

```
/plugin marketplace add anthropics/skills
```

```
/plugin install document-skills@anthropic-agent-skills
```

What they do:

- **frontend-design**: better-looking interfaces;
- **impeccable**: polishes designs and checks the UI for the typical "made by AI" look;
- **document-skills**: exports the final deck as a `.pptx` on your company template.

### Step 4: shadcn helper (only if your app uses React with shadcn/ui)

That's the default for new projects. In a terminal, inside your project folder:

```
npx skills add shadcn/ui --skill shadcn
```

If your project uses `pnpm`, `yarn` or `bun`, use `pnpm dlx`, `yarn dlx` or `bunx` instead of `npx`.

### Step 5: restart and check

Close Claude Code (`/exit`), start it again with `claude --chrome`, and type:

```
/plugin
```

You should see `track-to-demo`, `frontend-design`, `impeccable` and `document-skills` in the list. If one is missing, run its step again. `kickoff` also checks the helpers and tells you if anything is missing.

---

## The day, step by step

Everyone opens Claude Code in the project folder. Each step is one command.

### 1. Kickoff (one person, ~15 minutes)

Have a company slide template (`.pptx` or `.potx`)? Before starting, create a folder called `templates` in your project and put the file there. Claude keeps that folder out of git, so company files are never uploaded by mistake. No template? Skip this: the deck can still be downloaded as `.pptx`.

Did the challenge come with data files (spreadsheets, CSV, JSON…)? Put them in a folder called `data` in your project. Claude keeps them out of git too.

```
/track-to-demo:kickoff
```

Paste the challenge text (or give a file path or link). Claude:

- summarises goals, judging criteria and deadlines, and asks you to confirm;
- looks at your code to understand the technology already in use. If the folder is empty, it proposes **TypeScript + React with shadcn/ui** and asks you to confirm;
- asks, all at once, only what's missing: who's in the team, the schedule, the idea, the design system, the slide template;
- lists the data the prototype will use and, for whatever is missing, creates realistic **made-up (synthetic) data** in `data/`, so designs, app and slides all show the same numbers;
- writes everything in **`BRIEF.md`**, the shared plan every later step reads.

Then **each person who explores a design** puts 2-3 images they like (screenshots of apps, websites, anything) in `explorations/references/<their-name>/`.

### 2. Explore designs (each explorer, in parallel)

```
/track-to-demo:explore anna
```

(use your own name). Claude creates a design board on claude.ai from your reference images, with the main screen and the empty and error states. Share the board with the team (**Share → edit access**).

### 3. Pick the final design (team)

Look at the boards together and say what you like from each one, for example *"layout from Anna, colours from Luca"*. Then:

```
/track-to-demo:explore compose
```

Claude builds the **"Final direction"** board from your choices. Not sure what to pick? Run it anyway: Claude compares the boards and recommends a mix, then asks before building it.

### 4. Build (developers)

```
/track-to-demo:build handoff
```

Run it once. Claude splits the work into small tasks, each with one owner, and writes them in **`WORK.md`**.

```
/track-to-demo:build next
```

Each developer runs this to do their next task. Claude writes the code, adds tests, runs them and commits. Repeat until your tasks are done.

```
/track-to-demo:build verify
```

Run this before each checkpoint and before the final freeze. Claude checks the prototype against the challenge's criteria and adds any problem it finds as a new task.

### 5. Present (presenter)

```
/track-to-demo:present
```

Claude proposes the slide outline, builds the deck with real screenshots, waits for the team's comments and approval, then exports the `.pptx` on your template. It also writes **`PRESENTATION.md`** with the script and likely questions from the judges.

---

## Files that appear in your project

Claude creates and fills these in. The only things you add yourself are your slide template in `templates/` and any data files that came with the challenge in `data/`.

| File | What's in it |
|---|---|
| `BRIEF.md` | The plan: challenge, goals, team, schedule, technology, rules |
| `explorations/` | Reference images and links to everyone's design boards |
| `WORK.md` | The task list: who does what, status, test evidence |
| `PRESENTATION.md` | Demo script, speaker notes, Q&A |
| `data/` | The data the prototype uses. Synthetic data is saved in git so the whole team has it; files from the challenge stay out of git |
| `templates/` | Your slide template and the final `.pptx`. You create it; it stays out of git |

---

## Words you might not know

- **Track**: the challenge you received.
- **Board**: a canvas on claude.ai where Claude draws screen designs.
- **Design system**: a set of colours, fonts and components, so everything looks consistent.
- **Contract freeze**: the moment the team stops changing how the pieces talk to each other, so everyone can work in parallel safely.
- **Feature freeze**: the moment you stop adding things and only fix and rehearse.
- **Commit / push**: saving your work in git / sending it to GitHub.

---

## Good to know

- Claude replies in your language.
- Claude never invents numbers or results, and labels mock-ups as mock-ups.
- Claude doesn't install things or handle passwords for you: when something is missing, it tells you the command to run.
- Boards and decks need an interactive session. They don't work with `claude -p`.
- To read someone else's board you need **edit** access. With view access Claude only gets a summary.
- Checking the app in the browser is useful, but it doesn't replace your tests.

---

## For plugin developers

```sh
claude plugin validate .
claude --plugin-dir .
```

## License

MIT
