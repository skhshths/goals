# Goals

A calm, minimal goal manager that runs from a single HTML file. You can track goals as **milestones** (a checklist) or as a **number** you're working toward. The app tells you whether each goal is on pace for its due date, and it celebrates when you finish one.

It has no build step, no account and no server. Open `index.html` in a browser and start. Your data stays in your browser's local storage, and you can export a backup at any time.

---

## Contents

- [Quick start](#quick-start)
- [Features](#features)
- [How progress and pace work](#how-progress-and-pace-work)
- [Keyboard shortcuts](#keyboard-shortcuts)
- [Data, backups and privacy](#data-backups-and-privacy)
- [Hosting it](#hosting-it)
- [Project structure](#project-structure)
- [Customising](#customising)
- [Browser support](#browser-support)
- [Accessibility](#accessibility)
- [Troubleshooting](#troubleshooting)

---

## Quick start

**Option 1: open the file.** Download or clone the repo, then double-click `index.html`.

```bash
git clone https://github.com/skhshths/goals.git
cd goals
open index.html          # macOS
xdg-open index.html      # Linux
start index.html         # Windows
```

**Option 2: serve it locally.** This is useful if you want to open it on your phone over your local network.

```bash
python3 -m http.server 8000
# then visit http://localhost:8000
```

On first launch, click **Try examples** to load five sample goals and explore. Delete them later from the **⋯** menu, or delete them one by one.

---

## Features

### Two ways to track a goal
| Type | Best for | How progress is measured |
| --- | --- | --- |
| **Milestones** | Projects with distinct steps ("Launch my portfolio site") | Completed milestones ÷ total milestones |
| **Number** | Countable targets ("Read 24 books", "Save $5,000", "Weigh 75 kg") | How far you've moved from *start* toward *target* |

You can switch a goal between the two types at any time from its detail panel. Both sets of data are kept, so switching back loses nothing.

### On the main screen
- **Overview tiles** show your active goals, average progress, goals due in the next 14 days (with an overdue count), and goals completed this year and all time.
- **Quick actions on every card** let you update a goal without opening it:
  - Milestone goals show the **next unchecked step** with a checkbox. Tick it and the next step slides in.
  - Number goals have **− / +** steppers. Press and hold to repeat, and the repeat speeds up the longer you hold.
- **Due-date badges** read "Due today", "3 days left" or "2 days overdue". They turn amber when a due date is within a week and red when it has passed.
- **Pace badges** (Ahead, On track or Behind) compare your progress with where you'd be at a steady pace. See [How progress and pace work](#how-progress-and-pace-work).
- **Tabs** for Active, Completed and Archived goals, each with a count.
- **Area filter chips** (Health, Career, and so on) appear when a tab contains goals from two or more areas.
- **Search** across titles, notes, areas, units and milestone text.
- **Sorting** by custom order, due date, progress or name.
- **Drag to reorder** in custom order. Grab the ⋮⋮ handle; it appears on hover on desktop and is always visible on smaller screens. Keyboard users can focus the handle and press ↑ or ↓.

### In the detail panel
Click any goal to open its panel. Every change saves as you type.
- A title you can edit in place, plus a **progress ring**.
- Area, due date and colour.
- **Why it matters**, a short note to remind you why the goal is worth it.
- **Milestones.** Add one with Enter, edit text inline, drag to reorder, and delete with ×. Pressing Backspace in an empty milestone deletes it.
- **Number settings.** A large current-value field with steppers, plus *start*, *target*, *unit* and *step*. For example, a savings goal can step by 50.
- An **activity timeline** of what changed and when. Repeated number updates within two minutes are merged into one entry, such as "12 → 15 books".
- **Complete, Reopen, Archive, Restore and Delete** actions.

### Polish
- Cards slide smoothly into new positions when you sort, filter, complete or reorder them (FLIP animations). New cards fade in one after another.
- Checkmarks animate as they're drawn. Progress bars and percentages count up. The tab indicator slides between tabs.
- A tasteful **confetti burst** in the goal's colour when you complete a goal.
- When a goal reaches 100%, a toast asks whether to mark it complete.
- **Undo** for complete, archive and delete, via the toast button or ⌘/Ctrl + Z.
- **Light and dark themes.** The app follows your system theme until you choose one, and switching plays a circular reveal animation where the browser supports it.
- On phones the detail panel becomes a **bottom sheet**.
- Respects **reduced motion**: with that setting on, every animation is switched off.
- **Syncs across tabs.** Edit in one tab and the other updates.

---

## How progress and pace work

**Progress**
- *Milestones:* `done ÷ total`. A goal with no milestones shows 0% until you complete it.
- *Number:* `(current − start) ÷ (target − start)`, clamped to 0–100%. This works in both directions. For a weight-loss goal with start 90 and target 75, moving to 85 counts as 33%. The **+** button always steps *toward* the target.

**Pace** is shown only for active goals that have a due date:
1. Expected progress is the share of time elapsed between the day you created the goal and the end of its due date.
2. Pace isn't shown until at least 8% of that time has passed, because it's too early to judge before then.
3. If your progress is ≥ 12 points above expected, the goal is **Ahead**. Within 10 points below expected, it's **On track**. Further behind than that, it's **Behind**.
4. Once the due date has passed, the red *overdue* badge replaces the pace badge.

---

## Keyboard shortcuts

| Key | Action |
| --- | --- |
| `N` | New goal |
| `/` | Focus search (`Esc` clears it) |
| `1` `2` `3` | Switch to the Active, Completed or Archived tab |
| `T` | Toggle light/dark theme |
| `?` | Show the shortcuts panel |
| `⌘/Ctrl` + `Enter` | Create the goal (in the New goal dialog) |
| `⌘/Ctrl` + `Z` | Undo the last complete, archive or delete |
| `↑` / `↓` | Move a goal or milestone (when its drag handle is focused) |
| `← / →` | Move between tabs, or between colours in a colour picker |
| `Esc` | Close the menu, dialog or panel |

---

## Data, backups and privacy

- **Where data lives:** everything is stored in your browser's `localStorage` under the key `goals-app/v1`. Nothing is sent anywhere. The only network request is for the Inter web font from Google Fonts. If it can't load, the app uses your system font.
- **Per browser:** data saved in Chrome on your laptop isn't visible in Safari on your phone. Use export and import to move it between them.
- **Export:** choose **⋯ → Export backup** to download `goals-backup-YYYY-MM-DD.json`.
- **Import:** choose **⋯ → Import backup** and pick a backup file. Imported goals are **merged** with what you already have. A goal with the same ID as an existing one replaces it; everything else is added. You'll see a confirmation first.
- **Clearing:** **⋯ → Delete all data** asks for confirmation and can't be undone. Export a backup first.
- **Private or incognito windows** usually discard local storage when the window closes, so export a backup if you need to keep anything.

### Backup file format

```jsonc
{
  "app": "goals",
  "exportedAt": "2026-10-27T17:00:00.000Z",
  "version": 1,
  "settings": { "theme": "dark", "sort": "manual", "tab": "active", "area": null },
  "goals": [
    {
      "id": "…",
      "title": "Read 24 books this year",
      "why": "Fewer feeds, more books.",
      "area": "Learning",
      "color": "violet",            // blue | violet | rose | orange | green | teal | graphite
      "type": "numeric",            // "milestones" | "numeric"
      "milestones": [ { "id": "…", "text": "…", "done": false, "doneAt": null } ],
      "start": 0, "current": 17, "target": 24, "unit": "books", "step": 1,
      "due": "2026-12-31",          // YYYY-MM-DD or null
      "status": "active",           // "active" | "done" | "archived"
      "createdAt": 1767312000000, "updatedAt": 1767312000000, "completedAt": null,
      "order": 0,
      "log": [ { "t": 1767312000000, "type": "created" } ]
    }
  ]
}
```

Import is forgiving. Missing fields get sensible defaults, and malformed goals (for example, ones without a title) are skipped.

---

## Hosting it

The app is a single static file, so any static host works.

**GitHub Pages**
1. Push this repo to GitHub (already done if you're reading this there).
2. Go to **Settings → Pages**.
3. Under *Build and deployment*, choose **Deploy from a branch**. Pick your branch (for example `main`) and the folder `/ (root)`, then click **Save**.
4. After a minute the app is live at `https://<username>.github.io/goals/`.

Other options include Netlify Drop (drag the folder in), Cloudflare Pages and Vercel. None of them need any build settings.

> Each host gives the app a different *origin*, and local storage belongs to an origin. Goals saved at `localhost:8000` won't appear on your GitHub Pages URL. Use export and import to move them.

---

## Project structure

```
goals/
├── index.html   # The whole app: markup, styles (CSS) and logic (vanilla JS)
└── README.md    # This file
```

Inside `index.html` the script is organised into clearly labelled sections:

| Section | Responsibility |
| --- | --- |
| Utilities | DOM helpers, date maths, number formatting, count-up animation |
| Data model & persistence | Goal schema, `normGoal` validation, `localStorage` save/load, cross-tab sync |
| Undo | Snapshot-based undo used by complete, archive and delete |
| Goal actions | Create, complete, reopen, archive, restore, delete, milestones, number steps, reordering |
| Rendering: main view | Overview tiles, tabs, area chips, keyed card rendering with FLIP animations, empty states |
| Sortable | Pointer- and keyboard-driven reordering, used by both the goal list and milestone lists |
| Layers | Focus trapping, Escape handling and scroll lock for the panel, dialogs and menu |
| Detail sheet | The goal editor panel |
| Modals | New-goal composer, confirm dialog, shortcuts |
| Menu, Toasts, Theme, Confetti, Keyboard shortcuts, Boot | Self-explanatory |

There are no dependencies and no build tools. Everything is vanilla HTML, CSS and JavaScript.

---

## Customising

- **Colours:** edit the `COLORS` map in the script. Each entry is an [OKLCH](https://developer.mozilla.org/en-US/docs/Web/CSS/color_value/oklch) hue (`h`) plus a chroma multiplier (`cs`). The lightness and chroma for each theme come from the `--al` and `--ac` CSS variables, so every colour stays balanced in both light and dark mode.
- **Theme tokens:** the `:root` and `:root[data-theme="dark"]` blocks at the top of the `<style>` tag hold every surface, border, text and shadow colour.
- **Suggested areas:** edit `DEFAULT_AREAS`.
- **Pace thresholds:** edit `paceOf()`. The values are `.08` (minimum time elapsed before pace shows), `.12` (ahead) and `-.1` (behind).
- **"Due in 14 days" window:** search for `<= 14` in `renderHeader()`, and change the label in the HTML to match.

---

## Browser support

Works in current versions of **Chrome, Edge, Safari (16.4+) and Firefox**, on desktop and mobile. The app uses modern but well-supported features: `oklch()` colours, `color-mix()`, `:has()`, the `inert` attribute, `structuredClone`, and the Web Animations API.

Some features are progressive enhancements. The circular theme-switch animation uses the View Transitions API; browsers without it switch themes instantly.

---

## Accessibility

- Every control is reachable by keyboard. Dialogs and the detail panel trap focus, close with `Esc`, and return focus to where you were.
- Cards expose a real button with a descriptive label, such as "Read 24 books this year, 71% complete. Open details." Progress bars use `role="progressbar"` with values.
- Reordering works without a mouse: focus a drag handle and press ↑ or ↓.
- Colour pickers are proper radio groups that you can move through with the arrow keys.
- Toasts are announced through a polite live region.
- Honours `prefers-reduced-motion` and `prefers-color-scheme`.

---

## Troubleshooting

| Problem | Fix |
| --- | --- |
| My goals disappeared | You may be on a different browser, profile or URL (origin), or in a private window. Open the app where you used it before, or import a backup. |
| "Couldn't save — browser storage is unavailable" | Storage is blocked (some privacy settings or private modes do this) or full. Export a backup, then allow site data for the page. |
| The font looks different | Inter loads from Google Fonts. Offline, the app falls back to your system font, which is expected. |
| Drag handles don't appear | Reordering is only available with **Custom order** sorting, outside the Completed tab, and while no search is active. |
