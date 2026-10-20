# Implementation Plan: Apparel and Textile Supplier Flood Exposure Map

**Date:** 2026-10-19 | **Spec:** [SPECIFICATION.md](./SPECIFICATION.md)  
**Status:** Draft — timeboxed first slice; full specification is not achievable within the stated hours

## Summary

Build a zero-budget, publicly accessible static prototype focused on floods. Milestone 0 is deployed as a real, data-free informational page to GitHub Pages. Then, only if the Sayari field-level license gate is passed and the source records support a join, add one source-attributed sample to an accessible table. The flood map is deferred beyond M1 to avoid promising a map implementation and reliable geometry join inside the small timebox.

The available time is **2 hours/week for 2 weeks = 4 hours total**. The deliberately limited M0/M1 implementation slice is estimated at **2.5 hours plus a 50% contingency buffer (1.25 hours) = 3.75 hours**. This estimate assumes the user supplies an immediately usable hosting destination, one already-prepared Sayari sample with field-level publication clearance, and one NOAA flood record suitable for evaluation. It does not include discovering, negotiating, or independently interpreting license terms; acquiring/cleaning datasets; the five-business ranking; all tiers; complete facility coverage; GDACS integration; historical data; or the map. If those prerequisites are absent, stop at the data-free M0 page and record M1 as blocked; do not exceed the timebox or publish uncleared data.

The production deployment uses GitHub Pages from `main` and `/docs`. M0 has been published at the URL listed in [README.md](./README.md).

## Technical Context

**Language/Version:** HTML, CSS, and browser JavaScript; exact local versions are not yet established  
**Primary Dependencies:** No runtime dependencies for M0/M1's accessible source-linked table. Leaflet is deferred with the map.  
**Storage:** Static, curated JSON files published with the site; no database  
**Testing:** Manual checks of source links, company/facility identity chain, flood match status, keyboard-only table navigation, visible focus, contrast, empty/error state, and public URL  
**Target Platform:** GitHub Pages static site, deployed from `main` `/docs` at the URL in [README.md](./README.md)  
**Performance Goals:** Not specified by the approved specification  
**Constraints:** 4 hours total, 0 budget, beginner experience; flood-only hazard scope; public read-only access; no secrets in browser code; no unsupported location guesses or invented hazard buffers; data coverage must be stated. The user states that public Sayari access is permitted, but publication is gated on confirming the specific fields and derived display against the license.

## Environments

| Environment | URL | Deployment | Status |
|---|---|---|---|
| Production (GitHub Pages) | [https://isislcn.github.io/Hazard-and-Suppliers/](https://isislcn.github.io/Hazard-and-Suppliers/) | `main` branch, `/docs` folder | Verified HTTP 200 on 2026-10-19; currently the data-free M0 page |

### Technical decisions

| Decision | Choice and reason | Alternatives rejected |
|---|---|---|
| Application shape | Static HTML/CSS/JavaScript with a semantic HTML table and local source-attributed JSON. It is beginner-friendly, has no server cost, and deploys as a static site. | A backend, database, or full-stack framework adds setup, maintenance, and possibly hosting cost without being required for a small read-only prototype. |
| Public deployment | GitHub Pages from `main` `/docs`, already enabled and serving the M0 page. | Paid hosting and a new cloud service are rejected under the zero-budget constraint. |
| Source-data handling | M0 contains no Sayari data. Curator working files/drafts stay outside the deployed artifact. Only approved records that passed field-level license clearance may be copied into the public JSON. Use official NOAA flood records; GDACS flood records are deferred. | Live browser calls to Sayari or public APIs are rejected because they risk exposing credentials, depend on external service availability, and exceed the timebox. A database is unnecessary. |
| Entity and facility linking | Retain Sayari entity identifiers, company-to-supplier relationships, tier/depth, facility record, and supplied coordinates. Only associate risk indicators with facilities through the recorded Sayari path. | Matching on names alone, substituting headquarters for facility coordinates, or treating indirect suppliers as direct is rejected because it can create false matches. |
| Spatial matching | Use only provider-supplied affected-area geometry for an exposure match. A point-only event may be displayed as context but not labeled as facility exposure. | Invented distance radii or geocoding guesses are rejected because they are unsupported by the specification. |
| Map rendering | Use Leaflet with the OpenStreetMap public tile service for a small, low-traffic prototype, with visible map/data attribution and no API key or paid account. Verify current tile usage terms before publishing. | A complex GIS stack is rejected as too large for four hours. If the public tile service's terms do not fit, do not switch to a paid provider; show an attributed coordinate/geometry view or defer the map and disclose the limitation. |
| Evidence wording | Say “provider-sourced” or “source-attributed,” not “verified”; show sources and limitations. | Provider provenance is not independent validation of the claim and must not be presented as a legal finding or completeness guarantee. |
| Sayari publication gate | Before publishing, record that the license permits each particular field and derived display; uncleared material is excluded. | Publishing based only on an assumed general license permission risks disclosing unauthorized data. |
| Hazard scope | Floods only; NOAA is the primary source where its documented geography supports the facility. GDACS is optional and deferred. | USGS earthquake and other non-flood datasets are excluded from this prototype rather than mixed into a flood demonstrator. |
| Data download/export | Do not include public bulk export/download in the first version. | Export increases license and disclosure risk and is not required by the approved spec. |

## Constitution Check

No project constitution file was found in the project folder. Against the approved concept and specification:

- **Human decision-making:** PASS — the product presents evidence and does not decide coverage, pricing, or legal/ethical status.
- **Traceability:** PASS — each displayed item must retain Sayari/flood-provider attribution and record identifiers/links.
- **No unsupported inference:** PASS — no guessed facility locations or event radii; missing coverage is visibly unknown.
- **Privacy/licensing:** GATED — M0 is data-free. No Sayari-derived field or result is deployed until the curator records license clearance for that exact field/display.
- **Zero-budget/time constraint:** CONDITIONAL — a minimal first slice fits only under the estimate below; full specification coverage does not fit.

## Applied Guidelines

- No framework migration or technology-to-technology transformation is specified, so no migration guideline applies.
- Use the approved specification's safeguards: preserve source references, distinguish missing from negative evidence, avoid unsupported facility/event joins, and keep the public view read-only.

## Implementation Steps

### Phase 1 — Milestone 0: Data-free production shell

**Demo outcome:** Open the public production URL and show a real project page that explains its flood-only scope and says no source data has been published yet. No Sayari data or draft content is included.

#### Step 1.1: Create and publish the static shell
- **Requirements:** FR-017, FR-018, FR-020
- **Design inputs:** [SPECIFICATION.md](./SPECIFICATION.md), public-read-only requirement
- **Description:** Create `docs/index.html` and the empty `docs/.nojekyll`; GitHub Pages now deploys from `main` `/docs`. The deployed, data-free page has been checked at the production URL. If the live deployment becomes unavailable, report M0 as blocked until restored.
- **Estimate:** 0.75 hours
- **Decision:** Deploy the empty/informational page before building the data view, as required by Milestone 0.

### Phase 2 — Milestone 1: One source-traceable flood sample

**Demo outcome:** At the public URL, show one source-linked table example only if license clearance and source records support publication. Otherwise show an explicit “Sayari-derived data withheld pending license clearance” or “join unsupported” state. This is a sample, not the five-company product; the map is deferred.

#### Step 2.1: Gate publication and record one bounded Sayari sample
- **Requirements:** FR-005, FR-006, FR-007, FR-010, FR-011, FR-012, FR-017, FR-019
- **Design inputs:** [SPECIFICATION.md](./SPECIFICATION.md), approved Sayari-to-hazard matching procedure
- **Description:** Receive one already-prepared sample and its field-level publication-clearance decision. Record the permitted field/display scope and attribution/retention conditions in private curation notes. If permission is unclear or the sample is not ready, keep it outside the repository and mark M1 blocked. If cleared, prepare one source-linked sample record including the company/supplier/facility chain, depth, facility type/location evidence, and ethical-risk signal where available. Mark missing fields unknown.
- **Estimate:** 0.50 hours
- **Schedule:** Week 1

#### Step 2.2: Record one NOAA flood observation and match status
- **Requirements:** FR-008, FR-009, FR-011, FR-012, FR-013, FR-019
- **Design inputs:** [SPECIFICATION.md](./SPECIFICATION.md), official NOAA flood record; GDACS flood references deferred
- **Description:** Use one official NOAA National Water Prediction Service flood record only if its geography matches the available candidate facility. Preserve provider, record URL/ID, observation dates, provider flood category, and supported geometry. If no overlap/geometry can be established, record the unresolved/context-only status. Do not substitute a point or invented radius.
- **Estimate:** 0.50 hours
- **Schedule:** Week 1
- **Decision:** Use NOAA flood information only for M1; GDACS flood coverage is deferred and earthquakes are out of scope.

#### Step 2.3: Display one sample or safe unavailable state in an accessible table
- **Requirements:** FR-013, FR-015, FR-016, FR-017, FR-018, FR-019, FR-020
- **Design inputs:** [SPECIFICATION.md](./SPECIFICATION.md), map/table/evidence screen definitions
- **Description:** Render a single approved record in a semantic table with source links, relationship depth, flood record/category/time, match status, ethical-risk signal (if licensed and available), and limitations. Proposed paths: `docs/data/published-sample.json`, `app.js`, and updates to `docs/index.html` / `styles.css`. Keep working drafts outside the repository. If Sayari data are uncleared, display only the withheld/unavailable state and do not claim an overlap.
- **Estimate:** 0.50 hours
- **Schedule:** Week 2

#### Step 2.4: Verify and republish
- **Requirements:** FR-013, FR-015–FR-020
- **Design inputs:** [SPECIFICATION.md](./SPECIFICATION.md), defined empty/error states
- **Description:** Open the production URL and verify source links, attribution, private license-clearance record, no draft exposure, semantic table headers, keyboard-only navigation, visible focus, non-color-only status cues, and WCAG 2.2 AA contrast for the results flow. Confirm that no failed or unsupported join appears as “no risk” or facility exposure. Republish corrections.
- **Estimate:** 0.25 hours
- **Schedule:** Week 2

### First-slice effort and 50% buffer

| Work | Base estimate |
|---|---:|
| Step 1.1 — confirm host, build, and deploy data-free shell | 0.75 h |
| Step 2.1 — clear exact Sayari fields and record bounded sample | 0.50 h |
| Step 2.2 — record NOAA flood observation/match status | 0.50 h |
| Step 2.3 — render accessible table or safe withheld state | 0.50 h |
| Step 2.4 — verify release gate, accessibility, and republish | 0.25 h |
| **Total estimated work** | **2.50 h** |
| **50% contingency buffer** | **1.25 h** |
| **Planned total with buffer** | **3.75 h** |
| **Available time** | **4.00 h** |

| Week | Scheduled work | Base | 50% buffer | Total |
|---|---|---:|---:|---:|
| 1 | Confirm host; deploy data-free shell; record license clearance decision and one candidate sample | 1.25 h | 0.625 h | 1.875 h |
| 2 | Record one NOAA flood/match status; display accessible table or safe withheld state; verify and republish | 1.25 h | 0.625 h | 1.875 h |

The weekly buffered estimates are each below the 2-hour weekly limit. The buffer covers setup friction and one small, prepared source record, not data discovery, license analysis, or the deferred full specification. If a prerequisite is unavailable, stop at the data-free deployed shell rather than implying an overlap or exceeding the user's limit.

## Deferred work outside the 4-hour first slice

These items remain in the approved specification and are deferred beyond M0/M1:

- **P3.1 Candidate cohort and ranking:** publish the candidate register and rank the top five only within it using latest comparable annual-report segment revenue and the approved exchange-rate convention (FR-001–FR-004).
- **P3.2 Supplier coverage:** include available suppliers and tiers for the five businesses and manufacturing facilities with source-backed locations (FR-005–FR-007).
- **P3.3 Flood coverage:** add flood-classified GDACS records if usable and historical flood coverage where supported; earthquakes remain out of scope (FR-008–FR-009).
- **P3.4 Complete results experience:** add the accessible map, complete source-linked table, record detail, public read-only access, and empty/error/coverage states (FR-013–FR-020).
- **P3.5 Data breadth and maintenance:** expand beyond the sample, refresh source snapshots, and record changed/unavailable provider records without implying continuous monitoring (FR-011–FR-013, FR-018–FR-019).
- **P3.6 Sayari publication clearance:** retain field-level evidence that every published Sayari value/derived display is permitted and keep working drafts outside the deployable artifact (FR-011, FR-017).

## Ordered cuts if time runs out

1. Do not publish Sayari-derived content if field-level license clearance is incomplete; keep the deployed M0 page data-free and show the clearance/unavailability state.
2. Cut the map from M1 and retain the accessible semantic source-linked table; implement the map later with the same table/detail alternative.
3. Cut GDACS flood integration from the first demonstrator; disclose that only NOAA flood data are represented and do not imply GDACS has no floods.
4. Cut historical flood coverage from the first demonstrator; disclose the actual date window shown.
5. Limit M1 to one sample company/facility path; label it as a sample, not as the five-company result, and do not imply all supplier tiers were screened.

Do not cut source attribution, field-level license clearance, keyboard-accessible equivalent information, the distinction between unknown and no risk, the no-invented-geometry rule, or the distinction between a supplier entity and a manufacturing facility. Never describe the timeboxed sample as the complete product.

## Project Structure

```text
Hazard and Suppliers/
├── CONCEPT-IDEA.md
├── SPECIFICATION.md
├── PLAN.md
├── README.md                 # live URL, scope, and source/data limitations
└── docs/
    ├── index.html            # public read-only page
    ├── .nojekyll
    ├── app.js                # render static table/sample in M1
    ├── styles.css            # minimal accessible styling
    └── data/
        └── published-sample.json # only approved, license-cleared public records
```

No application framework, server, database, API key, or paid service is planned for the first slice. M1's semantic table needs no map dependency. Curator drafts and uncleared Sayari data must remain outside the repository and deployed artifact. If adding a later Leaflet map with OpenStreetMap tiles, verify current license, attribution, and usage conditions first.

## Testing Strategy

- **appType:** Static browser application
- **Critical user journeys:**
  1. Public visitor opens the live URL and sees the flood-only purpose and honest no-data state.
  2. Public visitor inspects an approved sample and reaches its originating Sayari/NOAA flood records.
  3. Public visitor sees a supported facility-flood match or an explicit unsupported/withheld state.
  4. Keyboard-only and assistive-technology users can inspect the same results and evidence without using a map.
  5. Public visitor sees no private draft, uncleared data, or editing control.
- **primaryValidationStack:** Manual browser walkthrough, direct source-link review, keyboard-only navigation, screen-reader spot check, and WCAG 2.2 AA contrast check; no test framework is justified for the first 2.5-hour implementation slice.
- **fallbackMatrix:** `infra-tier`: static JSON and a deployed shell; `browser-tier`: browser inspection. If public deployment is blocked, preserve the completed local shell but mark Milestone 0 as failed, not complete.
- **Environment requirements:** Existing GitHub account/repository access and public static hosting for M0; field-level Sayari license clearance before publication; browser; internet access to official flood records. No Docker or paid services.
- **knownGaps:** One sample does not validate candidate-cohort completeness, five-business ranking, all tiers, live updates, historical coverage, GDACS, or global flood coverage. The M1 map and automated geospatial accuracy tests are deferred.
- **Test data strategy:** M0 uses no source data. M1 uses only minimal records cleared for public display; curator drafts remain outside the repository. Preserve provider IDs/links and retrieval dates; never add fabricated example exposures.
- **Acceptance criteria:** Production URL loads publicly; source attribution and private license clearance are recorded; every displayed match has an explicit entity path and supported flood geometry; unsupported data is labeled unknown/context-only; public view is read-only; every result has semantic table access, keyboard operation, visible focus, and WCAG 2.2 AA contrast.
- **Validation review expectations:** Confirm field-level Sayari license permission before publication and label the sample as cohort-limited, flood-only, and source-attributed—not independently verified or a final risk judgment.

## Complexity Tracking

No constitution violations are proposed. The timebox means the first public demonstration will be a partial slice and will not satisfy all approved specification requirements; this is explicitly documented rather than treated as full completion.

## Requirement Mapping

| Requirement ID | Description | Plan Items | Implementation Evidence |
|---|---|---|---|
| FR-001 | Rank top five within documented candidate cohort by segment revenue | P3.1 | Candidate register, revenue records, cohort-bounded company screen |
| FR-002 | Preserve source, period, amount, currency, and business basis | P3.1 | Revenue records and ranking details |
| FR-003 | Convert to USD by annual-report rate or annual-average rate | P3.1 | Revenue records with conversion basis/source |
| FR-004 | Mark unsupported ranking evidence unresolved | P3.1 | Company ranking status and disclosure |
| FR-005 | Preserve supplier links and tier/depth | 2.1, P3.2 | `docs/data/published-sample.json`, supplier relationship fields |
| FR-006 | Include only sourced manufacturing facilities | 2.1, P3.2 | Facility records in `docs/data/published-sample.json` |
| FR-007 | Distinguish supported from missing/ambiguous facility location | 2.1, 2.3, P3.2 | Facility location and match status |
| FR-008 | Use NOAA flood records and optionally flood-classified GDACS; exclude non-floods | 2.2, P3.3 | Flood observations with dates, source and coverage state |
| FR-009 | Use provider flood category; no invented threshold | 2.2, P3.3 | Provider flood category/status displayed verbatim |
| FR-010 | Display Sayari signals as source-attributed, not determinations | 2.1, 2.3 | Signal wording, subject and source references |
| FR-011 | Retain originating records and field-level Sayari publication clearance | 2.1, 2.2, 2.3, P3.6 | Private license-clearance record and provider/source references |
| FR-012 | Mark unusable records/joins unresolved | 2.2, 2.3, P3.5 | Join status and limitations |
| FR-013 | Do not show missing data as no risk | 2.3, 2.4, P3.5 | Explicit unknown/unavailable states |
| FR-014 | Provide public map for supported facility-flood overlaps | P3.4 | Deferred map display and linked result detail |
| FR-015 | Provide public source-linked result table | 2.3, P3.4 | Accessible table rows with sources/status |
| FR-016 | Provide source, dates, match basis, and limitations | 2.3, P3.4 | Evidence/result detail |
| FR-017 | Public read-only view; drafts isolated; only cleared Sayari content published | 1.1, 2.1, 2.3, P3.6 | Data-free shell, published-only JSON, license-clearance record |
| FR-018 | Explicit empty/error states; no failed partial data as complete | 1.1, 2.4, P3.4 | Empty/error messaging and manual verification |
| FR-019 | Join via Sayari entity path and flood geometry without invented radius | 2.1, 2.2, 2.3 | Published sample chain and explicit match basis |
| FR-020 | Provide keyboard-accessible equivalent table/detail for map results | 1.1, 2.3, 2.4, P3.4 | Semantic table, meaningful headers, visible focus, contrast and keyboard tests |
