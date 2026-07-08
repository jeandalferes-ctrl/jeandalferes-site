# REQUIREMENTS.md — Dashboard Phase 1: Operations Tab (Mock Data / Public Demo)

Repo: jeandalferes-site (new route: `/demo-dashboard`)
Date: 2026-07-08
Contract between: Gareth (strategy) · Vesper (orchestration) · Forge (execution)

## 1. Vision & Rationale

Build the widget-based Operations tab specified in GARETH-04, bound to fabricated mock data, as both a public teaching artifact for the Agent Sovereignty course and the visual proof-of-concept for the eventual private dashboard (GARETH-11 Phase 2). A course viewer should see this and think "I want that system" — while a security review confirms zero real vault/agent data is present anywhere in the public build.

## 2. Success Criteria

- [ ] Page loads in under 1.5s on cellular
- [ ] Fully legible and navigable on phone and desktop
- [ ] Six widgets render correctly: Agent Status, Active Tasks, Token Economy, Recently Completed, Calendar & Todos, Project Pulse
- [ ] Every widget has two states — collapsed (glanceable) and expanded (one additional hierarchy level) — and both states render without errors
- [ ] Zero build step, single HTML file (or minimal file set) with inline/linked CSS, no framework runtime
- [ ] Aesthetic matches the approved dark-theater system: deep neutral ground, parchment `#F5F0EB` accents, project colors as the only saturation, Inter (UI) / Fira Code (logs/numbers) typography
- [ ] Mock data is the ONLY data source — verified by direct file inspection, no live vault/API calls present anywhere in the shipped code

## 3. Scope

**IN**: Operations tab only, six widgets per GARETH-04, mock adapter bound to static committed JSON, `/demo-dashboard` route, link from `/course` and `/kit` ("See a live example").

**OUT (future phases)**: live data binding (Phase 2), Cloudflare Access gating (Phase 2 — this route is public by design), Knowledge Base / Graph View tabs (Phase 3), the private `/dashboard` route itself.

## 4. Technical Requirements

- Static HTML/CSS/JS, no framework, no build step (matches the existing site's pattern)
- Mock data as a static JSON file committed to the repo, loaded client-side
- Data-adapter pattern: widgets read from a small JS interface, not hardcoded inline — so Phase 2 can swap the adapter without rewriting widget markup
- Responsive: works on phone and desktop, per the existing site's `clamp()`-based sizing approach

## 5. Design Specification

Per GARETH-04 §2 (widget-as-primitive doctrine) and §4 (aesthetic direction). Reference the already-shipped site pages (`index.html`, `course/index.html`, etc.) for the established color/typography system. **Aesthetic gate applies**: a frontier-model visual review pass before this is presented as done, same process used for the Course/Kit/About pages.

## 6. Acceptance Criteria

- All Success Criteria (§2) verified — checked, not assumed
- Aesthetic gate passed (Vesper visual review, documented)
- Zero real data present — verified by direct inspection of every shipped file
- Repo history clean per CODE.md commit format
- Live at `jeandalferes.com/demo-dashboard`, confirmed via HTTP check + browser render

## 7. Deliverables & Milestones

Given Forge's current single-file operating rule (see `per-agent-model-routing.md` — no verified sample yet for multi-file batches), this build is decomposed into discrete single-file assignments rather than one multi-file task:

1. `demo-dashboard/index.html` shell + page structure + nav — single file
2. `demo-dashboard/mock-data.json` — fabricated dataset — single file
3. `demo-dashboard/dashboard.js` — data adapter + widget rendering logic — single file
4. `demo-dashboard/dashboard.css` (or inline in the HTML, following the existing site's pattern) — single file

Each delivered and disk-verified independently before assembly.

## 8. Dependencies & Blockers

- No external dependencies — pure static build
- Mock data content needs a first draft (this session, Vesper-authored) before Forge/Quill touch it — see Mock Data Design Note below

## 9. Risks & Mitigations

| Risk | Impact | Likelihood | Mitigation |
|---|---|---|---|
| Real data accidentally leaks into mock build | High (privacy gate violation) | Low if disciplined | Explicit file-by-file inspection before deploy; mock data authored fresh, not copied from real vault files |
| Forge multi-file failure repeats | Medium (rework needed) | Unknown (small sample) | Single-file decomposition per current operating rule; disk verification after each file |
| Aesthetic drift from established site design | Medium (inconsistent brand) | Low | Reference existing shipped pages directly; aesthetic gate before ship |

## 10. Approval & Handoff

Owner: Vesper (orchestrator) · Reviewer: Vesper (aesthetic gate) → Commander (final) · Assigned agent: Forge (single-file tasks) + Vesper (assembly, mock data authorship, verification)

---
*Drafted 2026-07-08 · Vesper · per GARETH-11 §"Requirements Discipline"*
