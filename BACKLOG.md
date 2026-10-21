# Apparel and Textile Supplier Flood Exposure Map — Backlog

Prioritized work for the Apparel and Textile Supplier Hazard Exposure Map. Keep
this list aligned with the approved [SPECIFICATION.md](./SPECIFICATION.md) and
[PLAN.md](./PLAN.md).

## Now

Only Milestone 0 and Milestone 1 work is listed here. The first item delivers
the required production outcome without exposing any source data.

### T-001 — Confirm the hosting destination and deploy the data-free shell

- **Priority:** High
- **Milestone:** M0
- **Spec:** Infrastructure; FR-017, FR-018
- **Issue:** —
- **Why:** A real production page is required at M0. The repository currently has no production URL, so this task begins by checking that an existing GitHub repository and Pages publishing permission are available.
- **Done when:**
  - **Given** an existing GitHub repository and Pages permission are available, **when** `index.html` and `styles.css` are created and published, **then** a public production URL loads a real, data-free page describing the flood-only scope.
  - **Given** a visitor opens the page, **when** no source data have been cleared for publication, **then** the page states that no source data are published and does not imply no flood or ethical risk.
  - **Given** the hosting destination or permission is unavailable, **when** the task is attempted, **then** M0 is marked blocked and no fabricated production URL is recorded.

### T-002 — Clear Sayari fields for public release or explicitly withhold them

- **Priority:** High
- **Milestone:** M1
- **Spec:** FR-011, FR-017
- **Issue:** —
- **Why:** A general statement about public access does not establish that every field or derived display may be published.
- **Done when:**
  - **Given** specific Sayari fields and a proposed public display, **when** the curator reviews the applicable license, **then** a private clearance record outside the repository names the permitted fields/display and any attribution or retention conditions without copying license text into the public site.
  - **Given** a field/display cannot be cleared, **when** the sample is prepared, **then** that content stays outside the repository and deployed site and the public page shows a withheld/unavailable state.

### T-003 — Curate one license-cleared Sayari sample

- **Priority:** High
- **Milestone:** M1
- **Spec:** FR-005, FR-006, FR-007, FR-010, FR-011, FR-012, FR-017, FR-019
- **Issue:** —
- **Why:** The first useful data slice must preserve company-to-supplier-to-manufacturing-facility relationships and expose missing links instead of guessing.
- **Done when:**
  - **Given** field-level public clearance is recorded, **when** one candidate is curated into `data/published-sample.json`, **then** the sample records the source entity/reference, relationship depth, manufacturing-facility identity, location evidence, and ethical-risk signal/source where licensed and available.
  - **Given** the sample lacks a required relationship, facility type, source record, or supported coordinates, **when** its status is recorded, **then** the affected link is marked unknown or unresolved and no location or relationship is inferred.

### T-004 — Record one NOAA flood observation and match status

- **Priority:** High
- **Milestone:** M1
- **Spec:** FR-008, FR-009, FR-011, FR-012, FR-013, FR-019
- **Issue:** —
- **Why:** The prototype focuses on floods and needs an originating record plus a defensible spatial-match outcome, not a search snippet or an invented distance rule.
- **Done when:**
  - **Given** one official NOAA flood record is available for the candidate geography, **when** it is recorded alongside the sample, **then** its source reference, dates, provider flood category, and available geometry are retained.
  - **Given** the facility coordinates and provider-supplied affected-area geometry support a join, **when** the match is evaluated, **then** the sample records the match basis and provider category; **and given** the required geometry or link is missing, **then** the result is marked unresolved or contextual, not facility exposure.

### T-005 — Render the sample or withheld state in an accessible table

- **Priority:** High
- **Milestone:** M1
- **Spec:** FR-013, FR-015, FR-016, FR-017, FR-018, FR-019, FR-020
- **Issue:** —
- **Why:** A source-linked semantic table provides a useful, accessible first result view without overpromising map integration in the four-hour timebox.
- **Done when:**
  - **Given** an approved record is publishable, **when** the page renders it, **then** a semantic table includes supplier depth, facility, flood observation/status, source links, ethical-risk signal where cleared, and limitations.
  - **Given** a keyboard-only user navigates results, **when** they reach each row and evidence link, **then** focus is visible and all result information is available without a map or pointer.
  - **Given** a supported overlap cannot be established or Sayari data are withheld, **when** the page renders, **then** it displays an explicit unresolved/withheld status, not facility exposure or “no risk.”

### T-006 — Verify and republish the M1 demonstration

- **Priority:** High
- **Milestone:** M1
- **Spec:** FR-013, FR-015, FR-016, FR-017, FR-018, FR-019, FR-020
- **Issue:** —
- **Why:** The deployed result must preserve traceability and honest failure/coverage states before it is shown as a demo.
- **Done when:**
  - **Given** the M1 view is published, **when** it is checked at the production URL, **then** source links work, attribution is visible, license clearance is recorded, and the page is publicly read-only.
  - **Given** a visitor uses keyboard-only navigation or a screen reader, **when** they inspect the results table, **then** result content and links remain perceivable and operable.
  - **Given** a visitor inspects result status and controls, **when** they use keyboard navigation or contrast settings, **then** status is not conveyed by color alone, focus is visible, and text meets WCAG 2.2 AA contrast.
  - **Given** a data source fails, returns no usable record, or has unsupported coverage, **when** the page is checked, **then** the error/empty/unknown state is visible and no partial result is presented as complete.

## Next

Extend the cohort-bounded, flood-focused prototype after M0/M1. Do not imply
global cohort coverage.

### N-001 — Define and freeze a cohort of up to 10 candidates

- **Priority:** High
- **Spec:** FR-001
- **Issue:** —
- **Why:** “Top five” is not testable without a visible boundary for the companies considered; the inferred 10-candidate cap keeps the initial cohort bounded.
- **Done when:** The register contains no more than 10 named candidates, states eligibility/inclusion criteria, records each candidate's inclusion basis or exclusion reason and identification source/date, and is frozen before revenue comparison. The public ranking says “top five within this documented cohort,” not “global top five.”

### N-002 — Record comparable revenue for one cohort candidate

- **Priority:** High
- **Spec:** FR-001, FR-002, FR-003, FR-004
- **Issue:** —
- **Why:** Each annual report and currency basis needs separate attention; limiting this task to one candidate makes it small enough to estimate and review.
- **Done when:** One candidate has business-specific apparel/textile revenue basis, reporting period, amount/currency, annual-report reference, USD comparison value and FX method/source when needed; unsupported comparisons are marked unresolved. Create one separately estimated task per remaining candidate in the frozen cohort.

### N-003 — Publish the cohort-bounded five-business ranking

- **Priority:** High
- **Spec:** FR-001, FR-002, FR-003, FR-004
- **Issue:** —
- **Why:** Comparable records must be ranked consistently without silently dropping uncertain candidates.
- **Done when:** The public company view selects the five highest eligible candidates from the frozen cohort, links revenue basis and conversion evidence, and marks the selection unresolved if the cohort or evidence cannot support a defensible ordering.

### N-004 — Add one bounded batch of supplier relationships

- **Priority:** High
- **Spec:** FR-005, FR-011, FR-012, FR-019
- **Issue:** —
- **Why:** Relationship data can grow beyond a few hours; limit each task to one selected business and at most 10 relationship records.
- **Done when:** The batch records up to 10 company-to-supplier links with source references and depth; unknown or ambiguous links are labeled. Use separate tasks for additional batches.

### N-005 — Add one bounded batch of manufacturing facilities

- **Priority:** High
- **Spec:** FR-006, FR-007, FR-011, FR-012, FR-019
- **Issue:** —
- **Why:** Facilities require distinct source-backed location records; supplier headquarters are not proxies.
- **Done when:** The batch records at most 10 Sayari-linked manufacturing facilities for one selected business with source and supported coordinates/status; missing or ambiguous coordinates are not guessed. Use separate tasks for additional batches.

### N-006 — Expand NOAA flood observations for supported locations

- **Priority:** Medium
- **Spec:** FR-008, FR-009, FR-011, FR-012, FR-013, FR-019
- **Issue:** —
- **Why:** M1 uses one flood record only; additional facilities need appropriately covered official flood observations.
- **Done when:** Supported NOAA flood observations for selected locations include provider reference, observation period, category and geometry/match status; locations outside source coverage are unknown, not flood-free.

### N-007 — Add flood-classified GDACS records where usable

- **Priority:** Medium
- **Spec:** FR-008, FR-009, FR-011, FR-012, FR-013, FR-019
- **Issue:** —
- **Why:** GDACS is optional and must not be treated as a generic multi-hazard feed for this flood prototype.
- **Done when:** Only records explicitly classified as floods are included; provider fields, dates, categories, geometry, and limitations are preserved, and unsupported records are not converted into facility exposure.

## Later

Add breadth and completeness beyond the timeboxed first slice. Decompose further
before starting any item that grows beyond a few hours.

### L-001 — Add historical flood observations where provider coverage supports them

- **Priority:** Medium
- **Spec:** FR-008, FR-011, FR-012, FR-013, FR-019
- **Issue:** —
- **Why:** The initial plan defers historical flood coverage to fit the two-week timebox.
- **Done when:** Historical observations are added only for provider/geography/time periods with usable source records, and actual coverage dates and gaps are visible.

### L-002 — Complete accessible source-linked result-table fields and detail views

- **Priority:** Medium
- **Spec:** FR-015, FR-016, FR-018
- **Issue:** —
- **Why:** The first demo may show only one sample and a reduced evidence view.
- **Done when:** Each published flood overlap has a semantic table row and evidence detail containing company, supplier depth, facility, flood observation, ethical-risk signal, source references, relevant dates, match basis, coverage status, and limitations; keyboard navigation and visible focus work; empty/error states do not imply no risk.

### L-003 — Add a map for supported published flood overlaps

- **Priority:** Medium
- **Spec:** FR-014, FR-018, FR-019
- **Issue:** —
- **Why:** The first demo may omit map coverage if no supported facility-level geometry can be established.
- **Done when:** Every published flood overlap with supported facility coordinates and usable affected-area geometry is shown with source-derived context; unsupported/context-only records are not plotted as confirmed exposure, and all map results remain available in the semantic table/detail path.

### L-004 — Add explicit coverage and failure states to all screens

- **Priority:** Medium
- **Spec:** FR-004, FR-007, FR-012, FR-013, FR-018
- **Issue:** —
- **Why:** The full product must distinguish incomplete ranking, missing locations, unsupported joins, empty results, and source failures.
- **Done when:** Each screen identifies its empty/error/coverage condition and does not present missing, stale, inaccessible, or partial source data as a negative risk result or a complete screen.

### L-005 — Expand the Sayari data slice to all available supplier tiers

- **Priority:** Low
- **Spec:** FR-005, FR-006, FR-007, FR-011, FR-012, FR-019
- **Issue:** —
- **Why:** The first slice is limited to a small, auditable sample; the specification asks for available tiers without implying unavailable tiers were screened.
- **Done when:** Available supplier tiers are represented with relationship depth and traceable entity-to-facility links; absent or unsupported tiers and locations are identified as such.

### L-006 — Maintain field-level publication clearance and draft separation

- **Priority:** High
- **Spec:** FR-011, FR-017
- **Issue:** —
- **Why:** License permission may differ by source field, derived display, attribution, and retention requirement.
- **Done when:** Each published Sayari-derived field/display has a recorded clearance basis and required attribution; working drafts and uncleared fields remain outside the repository and deployed artifact.

This backlog follows the generation rules in Section 4 of the repository's
[PROMPT-PACK.md](../PROMPT-PACK.md): Now contains only M0/M1 tasks with
Given/When/Then criteria; all tasks cite specification IDs or infrastructure;
and later work is placed in Next or Later.
