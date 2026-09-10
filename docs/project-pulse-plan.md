# Mona's Project Pulse Dashboard Implementation Plan

## Summary

Mona's Project Pulse is a deterministic static dashboard intended to present project status, delivery signals, and operational highlights without any backend dependencies. The implementation should prioritize clarity, stable rendering, and predictable behavior across runs. The dashboard will be built as a small front-end in the `app/` directory with a static JSON data source, simple semantic HTML, and a dedicated design system in `app/styles.css`.

The work is split clearly by ownership: the Coder owns `app/index.html`, `app/project-data.json`, and `.vscode/launch.json`; the Designer owns `app/styles.css`; collaboration is required only at the integration handoff points where structure, styling, and data must align. The final experience should be a polished static dashboard that works locally via a VS Code launch configuration that serves from `app` and opens `index.html`.

## Goals

- Build a deterministic static dashboard that renders the same data in the same order every time.
- Keep the app dependency-free and easy to preview locally.
- Separate content, structure, and styling cleanly so ownership is explicit.
- Ensure a reliable preview workflow via `.vscode/launch.json`.
- Create a minimal but thorough validation checklist for launch, rendering, and edge-case coverage.

## File Ownership and Responsibilities

### Coder

Owned files:
- `app/index.html`
- `app/project-data.json`
- `.vscode/launch.json`

Responsibilities:
- Define the static dashboard data model and ensure it is valid JSON.
- Create the semantic page structure and the rendering logic needed to display the dashboard content.
- Ensure the app can run as a static site from the `app` directory.
- Add the VS Code launch configuration so the app serves from `app` and opens `index.html`.
- Confirm the app does not require any build step or runtime server beyond a local static file server.

### Designer

Owned file:
- `app/styles.css`

Responsibilities:
- Define the visual system: layout, spacing, typography, color semantics, cards, status treatments, and responsive behavior.
- Ensure the page matches the desired dashboard aesthetic while staying consistent with the static HTML structure.
- Prepare design decisions that fit the real data shapes and card layouts created by the Coder.
- Collaborate with the Coder at the HTML/CSS integration boundary to ensure the markup and styles match exact classes and sections.

### Collaboration boundary

Integration between Coder and Designer is required at these points:
- After the data model is agreed, so the Designer understands which card types and field labels exist.
- Before final CSS polish, when the Coder confirms the final HTML structure and class names.
- During QA, when visual alignment and responsive behavior are validated against the rendered page.

## Implementation Steps (Ordered)

### Step 1: Define dashboard scope and data contract

Purpose:
- Confirm what Mona's Project Pulse needs to show: project performance, workstream health, priorities, status summaries, and any deterministic metrics.
- Define the structure of the JSON data file before building any UI.

Dependencies:
- This is the foundation for all later tasks. No HTML or styling should be finalized before the data contract is clear.

Deliverables:
- Shared understanding of dashboard sections and required data points.
- Finalized static data schema for `app/project-data.json`.

Ownership:
- Coder leads this effort with Designer input.

Parallelism:
- Designer may begin a design moodboard or layout concept in parallel with the Coder's schema work, but the final visual implementation must wait for the agreed data structure.

### Step 2: Create the static data source

File:
- `app/project-data.json`

Purpose:
- Populate the dashboard with deterministic, static values that represent status, progress, milestones, risk, and project narrative.
- Ensure the data is valid JSON, static, and ordered predictably.

Responsibilities:
- Coder owns the file and is responsible for the exact field names and cardinality.
- Use stable values and a consistent ordering to guarantee repeatable rendering.

Dependencies:
- This step depends on Step 1's agreed data model and will feed the HTML rendering step.

Parallelism:
- This can happen in parallel with the Designer's initial CSS concept work, as long as the file schema remains stable and the final visual design is not locked to an unconfirmed shape.

### Step 3: Build the HTML structure and content hooks

File:
- `app/index.html`

Purpose:
- Create semantic page structure for the dashboard using static markup and the expected classes and sections.
- Ensure the structure matches the design system and data fields that will be rendered.

Responsibilities:
- Coder creates the HTML shell, section containers, metrics cards, list blocks, and any required script hooks.
- The page should be static-first, using the project data as the source of truth and avoiding unnecessary complexity.

Dependencies:
- Depends on Step 2 so the HTML matches the JSON schema and field names.
- Requires collaboration with the Designer once the base structure exists.

Parallelism:
- This is not parallel with the final style integration, because HTML structure influences CSS class usage and layout behavior.

### Step 4: Create the design system and visual styling

File:
- `app/styles.css`

Purpose:
- Style the dashboard for readability, hierarchy, responsive behavior, and a polished static presentation.
- Implement a consistent visual language for cards, chips, headings, tables/lists, and status indicators.

Responsibilities:
- Designer owns this file and sets the visual system based on the confirmed semantic structure.
- Designer should work with the Coder to confirm classes, spacing, and status patterns.

Dependencies:
- Depends on Step 3's HTML structure so classes and section composition are known.
- The final CSS must be integrated after the HTML is in place and before validation.

Parallelism:
- The Designer may conceptually prepare style rules before Step 3 is finalized, but the implementation itself should happen after the HTML is stable.

### Step 5: Integrate structure, data, and styling

Files:
- `app/index.html`
- `app/styles.css`
- `app/project-data.json`

Purpose:
- Confirm that the static dashboard renders correctly and that the structure, classes, and data all align.
- Eliminate mismatches between semantic markup and CSS expectations.

Responsibilities:
- Coder handles structure and data compatibility.
- Designer handles visual alignment and final presentation.
- Both collaborate in integration to ensure the page matches the original design intent.

Dependencies:
- Requires Steps 2–4 to be complete.
- This is the critical integration checkpoint before launch configuration is finalized.

Parallelism:
- No parallel work should occur here; this is a sequential integration step.

### Step 6: Add the preview launch configuration

File:
- `.vscode/launch.json`

Purpose:
- Configure a local preview flow that serves the dashboard from the `app` directory and opens `index.html`.
- Make it easy for a learner or developer to run the app in VS Code without build tools.

Responsibilities:
- Coder owns this file and ensures the configuration matches static dashboard requirements.

Dependencies:
- Must happen after the app is functional; it should not be created before the relevant app files are stable.

Launch requirement:
- The configuration must run from the `app` directory and open `index.html` to show the dashboard.
- The server should be lightweight and deterministic, serving static assets only.

Parallelism:
- This can happen near the end in parallel with final QA checks only if the app files are already stable.

### Step 7: Validation and polish

Files:
- `app/index.html`
- `app/styles.css`
- `app/project-data.json`
- `.vscode/launch.json`

Purpose:
- Verify all parts of the dashboard are aligned, accessible, deterministic, and runnable.
- Confirm that the page opens cleanly and the design remains stable under expected conditions.

Dependencies:
- This is the final gate after all implementation work is complete.

Parallelism:
- Validation is best done as a single pass rather than splitting work across parallel contributors, because it verifies the full integrated dashboard at once.

## Dependencies Map

- `app/project-data.json` is the source of truth for content and data key names.
- `app/index.html` depends on the data contract and should be built around the exact fields defined in the JSON.
- `app/styles.css` depends on the final HTML structure and class naming to produce correct layout and styling.
- `.vscode/launch.json` depends on the static app being ready and the project file layout being confirmed.

The sequence is therefore:

1. Scope + data contract
2. JSON data source
3. HTML structure
4. CSS styling
5. Integration check
6. Launch configuration
7. Validation

## Parallel vs Sequential Decisions

### Can run in parallel

- Coder can define the static JSON model while the Designer develops early visual concepts.
- The Designer can prepare overall typography, palette, and layout ideas before the final HTML is locked.
- Near the end, launch configuration can be drafted in parallel with final QA only if the app is already functionally stable.

### Must be sequential

- Final CSS implementation must wait until the final HTML structure is stable.
- Integration between HTML, CSS, and JSON must happen after all three are ready.
- Launch configuration should be created only after the app is known to work locally.
- Final QA should be one integrated pass rather than parallelized across separate app files.

## Validation Expectations and Checklist

The dashboard is considered ready when all of the following are true:

- The page loads without a build step or complex runtime.
- The dashboard renders deterministically from static data.
- All defined data points appear in the correct sections.
- No missing data placeholders appear unexpectedly.
- Styling matches the semantic structure and doesn't rely on ad hoc hacks.
- The design remains readable across common viewport widths.
- Status colors, labels, and hierarchy are visually consistent.
- No console errors or broken asset references occur during local preview.
- The VS Code launch configuration serves from `app` and opens `index.html` as the default view.

Suggested checklist:

- [ ] JSON is valid and complete.
- [ ] HTML includes all required sections and expected hooks.
- [ ] CSS targets the correct classes and structure.
- [ ] Dashboard renders without external data fetching.
- [ ] Data ordering is deterministic and repeatable.
- [ ] Content is readable and visually balanced.
- [ ] Responsive behavior is acceptable at small and wide widths.
- [ ] The launch config starts the app correctly from `app`.
- [ ] Preview opens `index.html` directly.
- [ ] No obvious accessibility or readability regressions are present.

## Risks and Edge Cases

- Missing or malformed JSON fields: the dashboard must not silently break if a value is absent; default or fallback patterns should be considered during design.
- Inconsistent ordering: if data is not ordered intentionally, the dashboard may appear unstable. Use fixed ordering in the JSON file.
- Overly long labels or content: cards, lists, and metrics should support long names without layout breakage.
- Zero-value metrics: the dashboard should visually handle zero or null values without appearing broken or misleading.
- Color-only status meaning: status indicators should also have clear labels or text semantics so accessibility is maintained.
- Responsive layout issues: the dashboard must remain usable on smaller screens without overlapping cards or unreadable content.
- Static environment assumptions: the app should not rely on a local runtime or network service, since it is meant to be deterministic and static.
- Launch configuration drift: if the server root or file paths are wrong, the app may open the wrong directory instead of the dashboard.

## Deliverables

By the end of the implementation, the repository should include:

- `app/index.html` containing the dashboard structure.
- `app/styles.css` containing the complete dashboard styling and layout.
- `app/project-data.json` containing the deterministic static project data.
- `.vscode/launch.json` configured to serve the app from `app` and open `index.html`.
- `docs/project-pulse-plan.md` capturing the plan and ownership decisions.

## Final Delivery Principle

This project should remain intentionally simple and deterministic: static data, simple markup, direct styling, and a local preview setup. The engineering goal is not to add unnecessary complexity; it is to provide a reliable dashboard that Mona can trust, preview easily, and present cleanly without backend dependencies.

