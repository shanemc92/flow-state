# flow-state

Build a process as a flowchart, get a runbook out of it. Then play the runbook and log each event. 

One HTML file, no build step, no dependencies, no network calls. Open it from disk or serve it as a static page.

## What it does

**build tab**

![screenshot-build](docs/screenshot-build.png)

- Steps are cards: give each one a label, a type and a swimlane, then point it at what comes next.
- Types: `start`, `action`, `decision` (path splits on an outcome), `parallel` (several things happen at once), `end`.
- Swimlanes are columns, for separate workstreams running alongside each other.
- The flowchart is laid out automatically from the step list. Drag a box or a branch label to move it,
  Reset layout to clear every nudge.
- Edges that skip past a row route around the side instead of through the boxes in between, and branch labels sit in their own tag so they stay readable.
- Scroll inside the frame, zoom, or open Full preview for the whole chart at once.
- Export SVG or PNG, or print.

**runbook tab**

![screenshot-runbook](docs/screenshot-runbook.png)

- The same steps with the detail a runbook needs: owner, evidence to capture, and how to actually do it.
- Editing a label or an outcome here updates the flowchart, and the other way round.
- Export Markdown writes the whole runbook out as one `.md` file, or print it straight from the tab.

**run tab**

![screenshot-run](docs/screenshot-run.png)

- Import a config (drag the JSON in, or add the flow you are building) and it stays in a list in this browser.
- Start a run and the tool walks the flow: only the steps that are live right now are shown, with the owner,
  the detail and what evidence to capture.
- Live steps are grouped under their swimlane, so parallel workstreams stay visibly separate rather than
  landing in one pile.
- Decisions show one button per outcome. Parallel steps open every branch at once. Each step takes a note
  before you close it, and every choice, note and skip is timestamped.
- Off-script actions get logged against the timeline rather than being lost.
- Position view shows the flowchart with the live steps outlined and closed ones dimmed.
- Runs survive a refresh. Export the record as Markdown or JSON, or print it.

Save config writes the whole thing (process metadata, lanes, steps, runbook detail, layout nudges)
to one JSON file. Load config reads it back.

`Ctrl+S` saves, `Ctrl+O` loads, `Esc` closes the preview.

## Where the data goes

Nowhere. Work is kept in this browser's localStorage until you reset. Imported processes and run
records are stored separately from the flow you are building, so resetting the builder leaves them alone, and the only way data
leaves the page is a file you download yourself. The CSP in the head blocks network access.

## Licence

MIT. See LICENSE.
