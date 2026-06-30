# Writing Pipeline

A simple file-based writing tool for getting individual pieces *finished*. The goal is to move them from a rough idea, through an outline and a draft, to published. There is also a journal feature that skips the workflow to help with regular journalling, e.g. Morning Pages.

It is one self-contained HTML file with no dependencies, no build step, and no account. Everything you write is stored as plain Markdown files in a folder you choose and control.

---

## Why I made it

Most writing tools are good at helping you *start*. They are far less good at helping you *finish*. It is easy to accumulate a graveyard of half-ideas and abandoned drafts, and easy to lose your words inside a proprietary app or a database you don't really own.

Writing Pipeline is built around a few deliberate opinions:

- **Finishing is the point.** The whole tool is shaped like a pipeline (Ideas → Outline → Drafts → Published) to keep work moving toward "done" rather than piling up at the start. A hard limit of three drafts at a time exists specifically to stop you spreading yourself thin and to push you to ship what you've started.
- **Fewer distractions.** No fonts to fiddle with, no formatting toolbar, no menus of features. Just a clean blank page and a focus mode that hides everything but the words.
- **You own your words, no lock-in.** Your writing is plain Markdown with YAML frontmatter, sitting in an ordinary folder. If this app disappeared tomorrow, every piece would still open in any markdown editor (e.g. Obsidian). Nothing is locked in, which means you can switch between this app and others with the same files too.
- **Low maintenance.** It's a single file with zero dependencies.
- **No mobile** - I find that the note I take on mobile just stay there. I wanted to force myself to have to open my desktop every time I write, even when it's just a quick idea. If I'm without my laptop I write it in my notebook. This may not work for you and you're free to fork this and make it responsive.

---

## Requirements

Writing Pipeline reads and writes files on your computer using the browser's File System Access API. That means it runs on **desktop Chromium browsers — Chrome, Edge, Brave, or Opera**. It does not work in Firefox or Safari, and it isn't designed for phones or tablets.

---

## Getting started

1. Save `writing-pipeline.html` anywhere on your computer.
2. Open it in Chrome, Edge, Brave, or Opera.
3. Click **Open folder** and choose (or create) an empty folder to keep your writing in. (tip: use it with a file fyncing service like Google Drive, Proton Drive, etc.)
4. On first use it creates a `_projects.yaml` file with three starter projects — `newsletter`, `blog`, and `journal`. You can edit these any time.

That's it. Start capturing ideas.

> **Tip — running from a local address.** If you open the file directly (a `file://` address) some browsers won't remember your folder between sessions. If you'd like the folder to be remembered reliably, serve the file from a simple local server instead, e.g. run `python -m http.server` in the folder containing the HTML file and open `http://localhost:8000/writing-pipeline.html`. Having said that, I personally haven't had issues with opening the file directly yet.

---

## Using it across devices

Because the app works on a plain folder, you can write on more than one computer by **keeping that folder in a synced location** — Google Drive, Proton Drive, Dropbox, iCloud Drive, OneDrive, or anything similar.

Point the app at your synced folder on each machine. Your Markdown files and `_projects.yaml` sync like any other files, and the app simply reads whatever is currently there. Open the folder on your laptop, write, let it sync, then open the same folder on your desktop and carry on.

A few things to keep in mind:

- Let your sync service finish before you open the folder, so you're working on the latest version.
- Don't edit the same piece on two machines at the same time — like any synced files, the last save wins, and your sync tool may create conflict copies.
- It's still desktop-Chromium-only on each device; a synced folder doesn't change the browser requirement.

The app file itself (`writing-pipeline.html`) doesn't need to be synced — it holds no data.

---

## The writing workflow

Every piece moves left to right through four stages, shown as a board.

### 1. Ideas
Capture quickly. Type into the box at the top of the Ideas column and press **Enter**.

Write it however best works for you. For my workflow I write a working title and a _purpose_. The title gives me a quick reference point that's helpful for scanning my ideas, the purpose reminds me what I was trying to achieve with the writing.

### 2. Outline
Open an idea and **Promote to outline**. You'll choose a **project** at this point (see below), and your original idea moves to an editable reference pane on the side so you don't lose the spark.

The outline is a list of cards, one per point:
- **Enter** makes a new item.
- **Tab** / **Shift-Tab** nests and un-nests an item, so you can group points under a heading.
- **Drag the ⠿ handle** to reorder — dragging a heading brings its sub-points with it.

I like to flesh out an idea with the main points I want to get across. They aren't always in order so I like to move them around, think about the struture of the writing and figure out if any of the outline items should be taken out (and possibly turned into anothe ridea)

### 3. Drafts
**Start draft** opens a clean, full-width Markdown writing surface. Your idea and outline sit in a side rail as editable references, and the outline pane expands to fill the space. Hit **Focus mode** to hide everything but the text (press **Esc** to leave it).

- You can set an optional **word target** which will add a simple progress bar to the bottom of the app.
- **There is a hard limit of three drafts at once.** I have a terrible habit of writing many unfinished drafts. A limit of 3 gives me enough space to write when inspiration hits. To start a fourth, publish one or step one back to Outline first. (Journal entries are exempt — see below.)
- **Internal links:** select some text and press **⌘/Ctrl-K** (or click **Link…**) to link it to one of your already-published pieces. Search the list, pick one, and a Markdown link is inserted using that piece's published URL.

### 4. Published
**Publish** marks a piece done. You'll enter the live link (this is required, except for journal entries), and the word count and date are frozen at that moment. Published pieces are read-only.

---

## Projects and templates

A **project** controls what kind of writing a piece is. Each project defines:

- the **frontmatter fields** that piece carries (for example, a blog post might need `title`, `description`, `slug`, `date`, `tags`, while a newsletter only needs `title` and `description`);
- whether a **link is required** to publish;
- whether its drafts **count toward the three-draft limit**.

Manage projects from the **Projects** button in the header. They're stored in `_projects.yaml` in your folder, so they're portable and editable by hand if you ever want to. You assign a project when promoting an idea to an outline, and you can change it later (fields that don't belong to the new project are dropped).

Frontmatter lives in a collapsible **Fields** panel at the top of the editor and never appears in your writing. I added projects in because I write for different websites with different frontmatter requirements. This way I can do it all in-app the copy and paste directly to the site. 

---

## Journal

Journaling has a different rhythm to finished articles, so it gets a fast path. The **+ Journal** button creates an entry straight as a draft — no idea or outline step, no reference panes, just write. 

Journal entries:

- don't need a link to publish;
- don't count toward the three-draft limit;
- default to a 750-word target;
- have their own section on the dashboard.

---

## The Dashboard

There are two sections to the dashboard.

**Overview** (your pipeline writing, excluding journal): words currently in drafts, drafts open, pieces published, total words published, a published-per-month chart, and a **Writing activity** grid — a 12-month, GitHub-style heatmap coloured by how many words you published each day.

**Journal:** a **day streak** counting consecutive days you've finished a journal entry, words written today / this week / this month, and a **Journal activity** grid on the same 12-month heatmap.

Hover any square in a grid for the date and word count; click a filled square to open that day's entry.

---

## How your writing is stored

- **One Markdown file per piece**, named by a timestamp, in your chosen folder.
- **YAML frontmatter** holds everything structural: the stage (`status`), the `project`, template fields, the `idea` and `outline` text, the `word_target`, and — once published — the `published_url`, `published_date`, and a frozen `word_count_at_publish`.
- **The body of the file is your draft**, in plain Markdown, ready to paste into whatever you publish with.
- **`_projects.yaml`** in the same folder holds your project definitions.

The files are the source of truth. The app is just a calm way to look at and move through them. You can open, edit, back up, version-control, or sync these files however you like — they're yours.

---

## Licence

Released under **[CC0 1.0 Universal](https://creativecommons.org/publicdomain/zero/1.0/)** — dedicated to the public domain. Use it, modify it, build on it, whatever you'd like. No permission and no attribution required.

---

## Credits

Created by **Matt Smith**.

- Website — [https://thisismattsmith.com](https://thisismattsmith.com)
- LinkedIn — [https://www.linkedin.com/in/thisismattsmith/](https://www.linkedin.com/in/thisismattsmith/)
- Newsletter - [https://mattsmith.substack.com/](https://mattsmith.substack.com/)
- Source — [https://github.com/thisismattsmith/writing-pipeline](https://github.com/thisismattsmith/writing-pipeline)
