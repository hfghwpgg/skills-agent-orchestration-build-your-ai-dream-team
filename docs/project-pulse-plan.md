# Project Pulse Implementation Plan

## Summary
Mona's team requires a lightweight Project Pulse dashboard to help contributors quickly understand active projects, owners, current statuses, recent activity, and priority/risk levels. The goal is to build a polished, contributor-friendly static web application. It will consist of an HTML frontend, polished CSS styling, mock JSON data, and a VS Code launch configuration so the dashboard can be seamlessly run locally.

## Ordered Implementation Steps

### Phase 1: Data & Launch Configuration
- **Agent**: Coder
- **Files**: `app/project-data.json`, `.vscode/launch.json`
- **Tasks**:
  1. Create `app/project-data.json` with a top-level `projects` array. Ensure each object explicitly contains: `name`, `owner`, `status`, `recentActivity`, and `priority`.
  2. Create `.vscode/launch.json` using strict JSON (no comments). Define a configuration named **Run Project Pulse Dashboard**. Set `cwd` to `${workspaceFolder}/app` and ensure the configuration serves the directory and automatically opens `index.html` (avoiding a raw server directory listing).

### Phase 2: Design & Styling
- **Agent**: Designer
- **Files**: `app/styles.css`
- **Tasks**:
  1. Create a polished, responsive visual layout for the dashboard.
  2. Implement clear visual affordances: visible project cards, status badges, clear priority treatments, rounded corners, shadows, high contrast, and readable spacing.
  3. Define deterministic CSS hooks such as `.dashboard` and `.project-card` that the Coder can target later.

### Phase 3: UI Implementation & Data Integration
- **Agent**: Coder
- **Files**: `app/index.html`
- **Tasks**:
  1. Create `app/index.html` and link it to `app/styles.css`.
  2. Write embedded JavaScript to `fetch('project-data.json')` and dynamically render the project data.
  3. Apply the Designer's deterministic CSS classes (e.g., `.dashboard`, `.project-card`) to the generated DOM elements to ensure the layout matches the visual design.

### Phase 4: Validation & Review
- **Agent**: Orchestrator
- **Tasks**:
  1. Execute the **Run Project Pulse Dashboard** launch configuration in VS Code.
  2. Verify the application successfully opens `index.html` without showing a server directory listing.
  3. Ensure the dashboard accurately renders data, looks polished per the Designer's rules, and operates deterministically.

## File Assignments
- `app/project-data.json`: **Coder**
- `.vscode/launch.json`: **Coder**
- `app/styles.css`: **Designer**
- `app/index.html`: **Coder** (using structural input and CSS class names provided by the Designer)

## Responsibilities
- **Designer**: Handle UI/UX, accessibility, information hierarchy, and visual design. Prioritize user outcomes over decorative changes and build a polished frontend. Explain design tradeoffs, use proper visual affordances, and establish strict CSS classes to guide the HTML layout.
- **Coder**: Implement robust, testable, and predictable logic. Set up the strict JSON launch configuration, build the structured `project-data.json` schema, and construct the `index.html` file to fetch and render the JSON using the CSS classes created by the Designer.

## Dependencies & Execution Order
- **Parallel Work**: Phase 1 (Data & Configuration by Coder) and Phase 2 (Design & Styling by Designer) can be executed in **parallel** since they do not block each other's initial creation.
- **Sequential Work**: Phase 3 (UI Implementation) must execute **sequentially** *after* Phase 1 and Phase 2. The Coder needs the JSON structure to fetch data and the CSS class names to correctly assemble `app/index.html`.
- **Validation**: Phase 4 strictly relies on the completion of all preceding phases.

## Edge Cases to Handle
- **Fetch Errors**: The JS in `index.html` must handle cases where `project-data.json` fails to load, is empty, or is malformed.
- **Missing Data Fields**: The HTML renderer should handle missing object properties (e.g., missing `recentActivity`) gracefully without breaking the UI layout.
- **Responsive Layouts**: The dashboard must remain readable and functional on varying screen sizes (e.g., utilizing CSS Grid or Flexbox wrapping).

## Validation Expectations
- The project successfully runs via the VS Code "Run Project Pulse Dashboard" launch configuration.
- The launch flow directly opens the UI (`index.html`) rather than a backend folder structure.
- Data is dynamically loaded from `app/project-data.json` and presented accurately.
- The dashboard exhibits a high level of visual polish (project cards, status badges, typography) reflecting the Designer's work.

## Open Questions
- What underlying server command/tool should `.vscode/launch.json` rely on to serve the static app in this specific environment (e.g., Python's `http.server`, Node's `npx serve`, or a specific VS Code extension)?
- Is there a specific color palette preferred by Mona's team, or should the Designer default to a modern, neutral theme with semantic status colors (e.g., Green/Healthy, Red/At-Risk)?
