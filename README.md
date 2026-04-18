# The Daily Reflection Tree

A deterministic end-of-day reflection tool — DT Fellowship Assignment submission.

---

## Repository Structure

```
reflection-tree/
├── tree/
│   ├── reflection-tree.json     ← Part A: The tree (35 nodes, fully traversable)
│   └── tree-diagram.md          ← Part A: Mermaid visual diagram
├── agent/
│   └── index.html               ← Part B: Web UI agent (no LLM, no dependencies)
├── transcripts/
│   ├── persona-1-transcript.md  ← Victor path: Internal/Contribution/Altrocentric
│   └── persona-2-transcript.md  ← Victim path: External/Entitlement/Self-centric
├── write-up.md                  ← Part A: Design rationale (2 pages)
└── README.md                    ← This file
```

---

## Part A — Reading the Tree

The tree lives entirely in `tree/reflection-tree.json`. No code is required to understand it — every possible conversation path can be traced by reading the data.

### Quick structure

```
35 nodes total:
  start:      1    (session opener)
  question:  13    (employee picks from fixed options)
  decision:   8    (invisible routing, no user interaction)
  reflection: 9    (insight shown; employee reads and continues)
  bridge:     2    (axis transition; auto-advances)
  summary:    1    (end-of-session synthesis)
  end:        1    (session close)
```

### How to trace a path manually

1. Start at node `START`, follow `next`.
2. At a **question** node, pick any option — it records a signal and points to the next node.
3. At a **decision** node, evaluate `routes` top-to-bottom. Find the first matching condition; follow its `next`. Conditions are:
   - `{"type": "answer", "node": "X", "answer_in": [...]}` — matches if the answer at node X is in the list
   - `{"type": "signal", "axis": "axisN", "compare": "pole1 > pole2"}` — matches if the tally comparison is true
   - `{"type": "default"}` — always matches (used as fallback)
4. At **reflection**, **bridge**, **summary**, and **end** nodes, follow `next`.

### Interpolation syntax in node text

| Placeholder | Resolves to |
|-------------|-------------|
| `{A1_OPEN.answer}` | The label of the option the employee chose at node A1_OPEN |
| `{axis1.summary}` | A template string from `state_templates.axis1` based on which pole is dominant |
| `{axis2.summary}` | Same for Axis 2 |
| `{axis3.summary}` | Same for Axis 3 |

### Signal accumulation

Signals are recorded on question **options**, not nodes. When an option is selected:

```
"signal": "axis1:internal"  →  state.axis1.internal += 1
"signal": "axis2:entitlement"  →  state.axis2.entitlement += 1
```

Decision nodes read these tallies to route deterministically. No LLM. No randomness.

---

## Part B — Running the Agent

The agent is a single HTML file (`agent/index.html`) that loads `tree/reflection-tree.json` via `fetch()`. Because browsers block local file requests, you need a local HTTP server.

### Option 1: Python (recommended, zero install)

```bash
cd reflection-tree
python3 -m http.server 8000
```

Then open: **http://localhost:8000/agent/index.html**

### Option 2: Node.js

```bash
cd reflection-tree
npx serve .
```

Then open the URL shown in the terminal, navigate to `/agent/`.

### Option 3: VS Code

Install the **Live Server** extension, right-click `agent/index.html` → *Open with Live Server*.

---

## What the Agent Does

- Loads the tree from `../tree/reflection-tree.json` (relative to `agent/`)
- Renders each node type with distinct visual treatment
- Question nodes: employee clicks one option; signal is recorded; next node resolves
- Decision nodes: silently evaluated; invisible to employee
- Reflection/bridge/summary: employee reads, clicks Continue
- Accumulates per-axis signal tallies throughout the session
- Interpolates `{placeholders}` in all text using recorded answers and signal dominants
- Produces a structured summary at the end referencing all three axes
- Allows the session to be restarted

**No API calls are made at runtime. No LLM. Same inputs → same path → same reflection, every time.**

---

## The Three Axes

| Axis | Psychology | Spectrum |
|------|-----------|---------|
| 1: Locus | Rotter (1954) Locus of Control; Dweck (2006) Growth Mindset | Victim ↔ Victor |
| 2: Orientation | Organ (1988) OCB; Campbell et al. (2004) Psychological Entitlement | Entitlement ↔ Contribution |
| 3: Radius | Maslow (1969) Self-Transcendence; Batson (2011) Perspective-Taking | Self-Centric ↔ Altrocentric |

---

## Design Constraints Met

| Constraint | Status |
|-----------|--------|
| No LLM at runtime | ✅ Pure state machine, zero API calls |
| Deterministic paths | ✅ Same answers → same nodes → same reflection |
| Fixed options only | ✅ Every question has 4 predefined choices |
| No moralizing | ✅ All reflections guide without grading |
| All 3 axes in sequence | ✅ Axis 1 → Bridge → Axis 2 → Bridge → Axis 3 |
| 25+ total nodes | ✅ 35 nodes |
| 8+ question nodes | ✅ 13 question nodes |
| 4+ decision nodes | ✅ 8 decision nodes |
| 4+ reflection nodes | ✅ 9 reflection nodes |
| 2+ bridge nodes | ✅ 2 bridge nodes |
| 1+ summary nodes | ✅ 1 summary node |
| Tree loadable as data | ✅ JSON — any developer can load it independently |
