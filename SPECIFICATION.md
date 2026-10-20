# Apparel and Textile Supplier Flood Exposure Map — Product Specification

**Governed by:** [CONCEPT-IDEA.md](./CONCEPT-IDEA.md)  
**Status:** Approved  
**Input:** Approved concept and interview answers

## 1. Purpose and boundaries

### Purpose

Specify a short, flood-focused prototype for insurance underwriters that screens the top five apparel/textile businesses within a documented candidate cohort, ranked by latest comparable segment revenue. It combines available Sayari supplier relationships and manufacturing-facility information with supported flood observations and ethical-risk indicators. It presents qualifying overlaps in an accessible map and source-linked table.

Every published flag must be traceable to source records from Sayari and the relevant public flood provider. Describe evidence as provider-sourced/source-attributed, not independently verified. The product presents source-derived signals for underwriters; it does not determine whether to insure a company, make a final ethical or legal finding, or send emergency alerts.

### Must have

1. Publish a candidate-cohort register and rank the five highest eligible apparel/textile businesses within that documented cohort using comparable latest annual-report segment revenue, with sources and currency conversions recorded. Do not claim the cohort is globally exhaustive.
2. Show available Sayari supplier relationships and manufacturing facilities, labeling supplier depth.
3. Show flood information from NOAA and, only where explicitly flood-classified and usable, GDACS. The prototype excludes earthquakes and other non-flood hazards. State the actual time window and source coverage; historical coverage is deferred unless it fits the available time.
4. Use only provider-defined flood categories/thresholds; do not derive a common high-risk threshold. Flag supported overlaps with the specified Sayari ethical-risk indicators.
5. Retain the originating Sayari and public flood-provider records behind every flag. Describe them as source-attributed evidence, not verified claims.
6. Provide both a map and a source-linked table, with visible data gaps and explicit empty/error states.
7. Make the published map and table publicly accessible only after the curator confirms that the applicable Sayari license permits publication of each field and derived display. Keep curation activities separate from the public view.
8. Provide an equivalent semantic, keyboard-accessible table/detail path for every map result; the map must not be the only way to access information.

### Should have

- Show company revenue ranking inputs and conversion basis so a reviewer can reproduce the five-company selection.
- Show supplier relationship depth, source dates, data-provider attribution, spatial-match status, and hazard time coverage alongside each flag.
- Include all supplier tiers available in Sayari data, without implying unavailable tiers were screened.

### Out of scope for first release

- Automated underwriting, pricing, coverage, or claims decisions; final legal or ethical findings; emergency alerts; or continuous monitoring.
- Any sector beyond apparel/textiles, any additional company beyond the selected five, or facility types other than manufacturing.
- A risk score or a claim of comprehensive geographic, supplier, hazard, or ethical-risk coverage.

### Scope baseline

- **Discovery method:** Review of the approved concept and the answers given in the interview.
- **Existing-code discovery:** Not applicable; this is a concept-level specification and no implementation inventory was supplied.
- **In scope:** Revenue-based selection of five businesses within an explicitly documented candidate cohort; available Sayari supplier links and manufacturing facilities; flood-only observations from NOAA and flood-classified GDACS records where usable; source-attributed flood and ethical-risk overlap screening; accessible map and source-linked table; explicit disclosure of data gaps.
- **Initial geography:** Only geographies supported by available data.
- **Out of scope:** Any additional sector or company beyond the five-company cohort result; earthquakes and non-flood hazards; automatic underwriting, pricing, coverage, claims, or emergency-response decisions; final legal or ethical determinations; presenting missing data as absence of risk.

### Out of scope

- Making, recommending, or automating underwriting, coverage, pricing, or claims decisions.
- Making final determinations that a company or supplier uses forced labor, violates sanctions, or is ethically acceptable or unacceptable.
- Issuing live alerts, forecasting events, or supporting emergency response.
- Publishing supplier/facility exposure results for more than the five selected apparel/textile businesses.
- Including facilities other than manufacturing facilities.
- Treating a supplier relationship, risk signal, hazard category, or map overlap as proof of wrongdoing or loss.
- Treating missing, stale, inaccessible, or geographically unsupported data as evidence of safety or no exposure.
- Adding export/download of licensed source data (not requested for this prototype).
- Publishing Sayari-derived content before field-by-field license clearance.
- Claiming the screened candidate cohort represents the global top five businesses.
- Treating map interaction as the only accessible way to inspect an exposure record.
- Building a general-purpose supply-chain risk platform, continuous monitoring service, or exhaustive global dataset.

## 2. Users and core jobs

| User | Job |
|---|---|
| Insurance underwriter / public reviewer | Inspect publicly accessible supplier manufacturing-facility and trade-link context for the selected apparel/textile businesses, and review source-derived overlaps between hazard exposure and ethical-risk indicators. |
| Data curator (inferred) | Assemble the company screen and provider records, map supplier/facility and hazard evidence, maintain source attribution, and publish or correct the public view. No independent human check is required by this concept. |

The curator role is an operational assumption (inferred). Public access applies to the published view; editing and draft curation are not public. Provider-sourced records identify the origin of a signal; they do not independently verify its truth or guarantee provider-data completeness.

## 3. Screens and permissions

Prototype roles:

- **Public (user-specified):** Read-only access to the published map, table, and displayed source attribution/evidence, after field-level license clearance. The user states that the Sayari license permits public access.
- **Curator (inferred):** Prepares, reviews for license clearance, and publishes records using a private workflow outside the static public application. Curator editing/authentication is not part of this prototype.
- No account is required to view the published prototype (inferred from the public-access requirement). The deployed site has no editing controls; drafts and license-clearance evidence stay outside the repository/deployment.

| Screen | Purpose and content | Permission | Empty state | Error state |
|---|---|---|---|---|
| Company screen | Show the documented candidate cohort and the five selected apparel/textile businesses, latest annual-revenue basis, reporting period, source, USD conversion basis, and cohort-bounded rank. | Public: read published cohort/register and ranking. Curator: maintain evidence in a private workflow outside the site. | Explain that the cohort/ranking is incomplete and identify missing evidence; do not substitute companies without a documented basis. | Explain which source or conversion could not be retrieved; keep affected ranks unresolved and do not imply a global top five. |
| Exposure map | In a later release, plot source-derived flood overlaps at supported manufacturing-facility locations, with company, supplier-tier depth, flood category/time, source attribution, and ethical-risk indicator summary. | Public: read published map. Curator: prepare data outside the site. | State that no matching records are available; distinguish “no matched records” from “no flood risk.” | Explain whether provider data, coordinates, or map content failed to load. Do not treat failure as a negative result. |
| Flag table | List source-derived flood overlaps with company, supplier, relationship depth, facility, flood observation, ethical-risk signal, source attribution, and coverage/match status. | Public: read published rows. Curator: maintain source data in a separate private workflow; no public-site editing. | State that no matched entries are available and identify known coverage gaps. | Identify the failed data operation and offer retry/recovery where possible. Do not present partial results as complete. |
| Evidence and flag detail | Show Sayari identity/relationship references, facility location, flood-provider record, ethical-risk indicator, spatial-match basis, dates, and limitations. | Public: read evidence cleared for published records. Curator: review source evidence and license clearance privately. Drafts remain outside the deployment. | Explain that no detail is available or the source record is missing; distinguish a missing record from a record showing no event. | If a provider record is inaccessible or malformed, show the source and retrieval failure; mark the result unavailable and correct/withdraw it in the next approved publication. |

The user states that the Sayari license permits public access to the licensed data in this prototype. Public access is read-only; data export/download is not included.

## 4. User scenarios and testing

### User Story 1 — Review a published supplier exposure (Priority: P1)

As a public reviewer, including an insurance underwriter, I want to see a source-linked map and table of Sayari supplier hazard/ethics overlaps for the five selected apparel/textile businesses, so I can review the provider-sourced information.

**Why this priority:** This is the central user value in the concept.

**Requirements:** FR-013–FR-018, FR-020.

**Independent test:** Load provider-sourced Sayari and hazard records with a documented company-to-supplier-to-facility link and a supported spatial match; confirm that a public user can inspect the resulting source attribution, relationship depth, and data limitations.

**Acceptance scenarios:**

1. **Given** a published flag with supported coordinates and provider records, **When** a public user opens the map, **Then** the facility is shown with its company, supplier depth, flood category/time, and ethical-risk signal.
2. **Given** a published flag, **When** a public user opens its table row or detail, **Then** the Sayari and hazard-provider source records are accessible and the item is clearly described as a signal, not a final judgment.
3. **Given** incomplete or unsupported data for a facility, **When** a reviewer views the map or table, **Then** the limitation is stated and missing data is not represented as no risk.
4. **Given** a public user cannot or does not use the map, **When** they navigate by keyboard or assistive technology, **Then** the semantic table and evidence details expose the same result and source information.

### User Story 2 — Establish the five-company screen (Priority: P1)

As a curator, I want to document the candidate cohort and rank its apparel/textile businesses using comparable latest annual reports and a documented currency-conversion basis, so the prototype's five-company result is reproducible and not mistaken for a global ranking.

**Why this priority:** Supplier analysis cannot be interpreted until the company selection and revenue basis are transparent.

**Requirements:** FR-001–FR-004.

**Independent test:** Provide a published candidate register and enough comparable company revenue records, including a record requiring annual-average FX conversion, and verify that the displayed five-company ordering follows the recorded inputs and is labeled as cohort-bounded.

**Acceptance scenarios:**

1. **Given** a candidate business, **When** the curator includes or excludes it from the screened cohort, **Then** the register records its business identity, inclusion basis or exclusion reason, and annual-report/source reference where available.
2. **Given** a company with a latest annual report and an apparel/textile business revenue figure, **When** the curator records the revenue evidence, **Then** the ranking stores the business scope, reporting period, reported amount/currency, source, and conversion basis when converted to USD.
3. **Given** an annual report that states a conversion rate, **When** its revenue is normalized for ranking, **Then** the annual-report rate is used and retained as the conversion basis.
4. **Given** an annual report without a stated conversion rate, **When** the curator normalizes its revenue, **Then** a reputable published annual-average exchange rate for the reporting year is recorded with its source.
5. **Given** insufficient evidence to distinguish apparel/textile business revenue or normalize a ranking comparison, **When** the curator reviews company selection, **Then** the affected rank remains unresolved rather than being silently estimated.
6. **Given** the cohort and comparable revenue records are displayed, **When** a user reads the ranking, **Then** it is labeled “top five within the documented cohort,” with the cohort register accessible and no claim of global exhaustiveness.

### User Story 3 — Join and publish a source-derived flag (Priority: P1)

As a curator, I want to join Sayari supplier/facility records to public hazard-provider records, so source-derived overlaps can be presented to public users.

**Why this priority:** The provider-to-facility join is the core analysis. The user has specified provider provenance as the verification basis and has excluded separate human independent verification.

**Requirements:** FR-005–FR-012, FR-017, FR-019.

**Independent test:** Use one set of source-attributed Sayari entities/relationships/facilities and public hazard records, and verify that supported spatial/entity matches are displayed while unlocated facilities or point-only hazard records are not described as facility exposure.

**Acceptance scenarios:**

1. **Given** a Sayari supplier entity linked to a manufacturing facility and an available flood record with usable affected-area geometry, **When** their source data and location geometries are joined, **Then** a candidate overlap records the entity path, spatial-match basis, flood record, ethical-risk indicator, and source references.
2. **Given** a candidate overlap whose input records come from Sayari and the selected public flood provider, **When** the curator publishes the source-derived result, **Then** it is attributed to those providers and described as source-attributed, not independently verified.
3. **Given** a facility without reliable coordinates or a hazard event with only a point and no supported affected-area geometry, **When** a join is attempted, **Then** the facility is not described as exposed using an invented location or distance radius.
4. **Given** an input source record is unavailable or malformed, **When** the curator prepares the result, **Then** the affected match is marked unavailable or unresolved, not silently treated as a verified absence of risk.

### User Story 4 — Understand coverage and data gaps (Priority: P2)

As a reviewer, I want to see which facility and hazard information is unavailable or unsupported, so I do not mistake partial coverage for low risk.

**Why this priority:** The concept explicitly limits the geography to available data and requires data gaps to be visible.

**Requirements:** FR-005–FR-009, FR-013, FR-018.

**Independent test:** Provide facilities with complete, partial, and absent hazard coverage and confirm that each state is distinguishable in the screen and its evidence detail.

**Acceptance scenarios:**

1. **Given** a facility outside a source's supported geography or time coverage, **When** a reviewer opens the facility detail, **Then** the unsupported coverage is identified as unknown/unavailable, not as no hazard.
2. **Given** a supplier relationship with a known tier/depth, **When** the reviewer sees the facility in a map or table, **Then** the displayed relationship depth is retained and not presented as a direct supplier if it is not one.

### Edge cases

- The annual report reports only whole-company revenue and does not separate apparel/textile business revenue.
- The five-company set cannot be established because a relevant revenue figure or FX basis is unavailable.
- One company has multiple business segments, subsidiaries, or reporting currencies; the entity boundary must be stated rather than inferred.
- Sayari identifies a supplier relationship but does not provide a usable manufacturing-facility location.
- A facility has ambiguous, imprecise, or conflicting coordinates or addresses.
- A flood source has no coverage for the location, applicable time window, or flood category.
- A source reports current/near-term conditions but not historical events, or vice versa.
- A Sayari indicator is associated with a supplier entity but the supplier-to-facility identity link is absent or ambiguous.
- Provider records use incompatible or absent spatial geometry or coordinates.
- A provider record is updated, withdrawn, or stale after publication.
- A source record is updated, withdrawn, or becomes stale after a flag is published.
- Multiple hazard events or ethical-risk signals apply to the same facility; the table must retain separate evidence rather than collapse distinct claims into an unsupported single conclusion.
- A map or table data load fails; the interface must show an explicit error and must not pass off incomplete data as a complete screen.
- A user cannot access or operate the map; the semantic table and evidence detail must still expose the same records and source links.
- Sayari license terms do not clearly permit one field or derived display; that content must remain unpublished until cleared.

## 5. Functional requirements

### Company selection and revenue basis

- **FR-001:** The system MUST maintain a candidate-cohort register, limited to at most 10 candidates for the initial prototype (inferred), whose membership and eligibility rule are fixed before revenue comparison. When enough comparable evidence exists, it MUST show the five highest-ranked apparel/textile businesses within that cohort using latest annual-report business-specific revenue rather than whole-group revenue. Each candidate MUST have a business identity, inclusion basis or exclusion reason, reporting period and annual-report/source reference where available. Reporting periods and business boundaries MUST be sufficiently comparable; otherwise the ranking MUST be unresolved. The ranking MUST be labeled cohort-bounded and MUST NOT claim global exhaustiveness.  
  **Given** a frozen cohort of up to 10 candidates and comparable revenue records, **When** the curator finalizes the screen, **Then** it contains the five highest-ranked eligible businesses in the cohort with its boundary and reporting basis visible; **and given** the evidence or comparability is insufficient, **then** the selection is marked unresolved.
- **FR-002:** The system MUST retain the reported revenue amount, currency, reporting period, annual-report source, and the basis identifying apparel/textile business revenue for each ranked company.  
  **Given** a revenue record is added, **When** it is saved for ranking, **Then** all required revenue and source details are available for review and the record is not treated as complete if a required detail is missing.
- **FR-003:** The system MUST normalize revenue to USD using the annual report's stated exchange rate when available, and otherwise use a reputable published annual-average exchange rate for that reporting year. The rate and its source MUST be recorded.  
  **Given** a reported revenue is not in USD, **When** the curator records the normalized comparison value, **Then** the chosen rate, rate period, source, original amount/currency, and USD amount are retained together.
- **FR-004:** The system MUST mark company rankings unresolved when the business-specific revenue or conversion evidence is insufficient, and MUST NOT silently substitute an estimate or a different company.  
  **Given** required comparison evidence is missing, **When** the ranking is displayed, **Then** the affected entry and overall selection status are clearly marked unresolved.

### Supplier relationships and facilities

- **FR-005:** The system MUST represent available Sayari trade links and label each supplier's relationship depth/tier.  
  **Given** a supplier relationship is included, **When** it is displayed, **Then** the company-to-supplier relationship and available tier/depth are visible, and unknown depth is labeled unknown.
- **FR-006:** The system MUST limit facility records in the initial screen to manufacturing facilities and retain the source and location evidence for each facility.  
  **Given** facility information is imported or curated, **When** it is considered for a flag, **Then** it is identified as a manufacturing facility and has source evidence; otherwise it is excluded or marked unresolved.
- **FR-007:** The system MUST distinguish a facility with supported coordinates from one with missing, ambiguous, or unsupported location data.  
  **Given** a facility location cannot be reliably placed, **When** map results are prepared, **Then** the facility is not plotted at a guessed location and its location limitation is available in the table or detail.

### Hazard and ethical-risk evidence

- **FR-008:** The system MUST support flood observations from NOAA and may include GDACS records only when they are explicitly flood-classified and provide usable data. Earthquakes and other non-flood hazards are out of scope. The system MUST display the actual supported geography and time window; historical data is optional and deferred if it cannot fit the prototype.  
  **Given** a selected source returns a usable flood observation, **When** it is prepared for display, **Then** its provider, flood type/category, applicable time, supported geography, and source reference are retained; **and given** a non-flood event or unsupported coverage, **then** it is excluded or labeled unsupported.
- **FR-009:** The system MUST retain the selected flood dataset's own category/threshold and MUST NOT invent a common high-risk threshold across sources. It MUST NOT label a flood high-risk unless the provider supplies an applicable category/threshold that supports that wording.  
  **Given** a flood source supplies a category or threshold, **When** a candidate overlap is evaluated, **Then** the provider's category and wording are retained; **and given** the provider supplies no applicable category/threshold, **then** the flood is not labeled high-risk and that status remains unresolved.
- **FR-010:** The system MUST represent Sayari ethical-risk indicators for forced-labor risk, sanctions links, and opaque ownership as evidence signals, not final determinations.  
  **Given** Sayari provides one of these indicators, **When** it is included in a candidate flag, **Then** the indicator type, subject, source, and observed/retrieved date are visible to the curator.
- **FR-011:** The system MUST retain the originating Sayari and NOAA or flood-classified GDACS source record for every ethical-risk indicator and flood observation included in a candidate flag. Evidence MUST be described as provider-sourced/source-attributed, not independently verified. Before any Sayari-derived field or display is published, the curator MUST record that the applicable license permits that specific field and public display.  
  **Given** a candidate is prepared from provider data, **When** its source record is saved, **Then** the provider, source record link or identifier, applicable date, and claim/observation are attached to the candidate.
  **Given** a Sayari-derived field is proposed for public release, **When** the release is prepared, **Then** it remains excluded until license clearance for that field/display is recorded.
- **FR-012:** The system MUST withhold or mark a candidate unresolved when a required provider record is unavailable, malformed, or cannot be linked to the relevant supplier, facility, or hazard geography.  
  **Given** a required source record or identity/spatial link is missing or unusable, **When** a curator prepares or publishes the candidate, **Then** the affected claim is not represented as a supported facility-level overlap and the limitation is visible.
- **FR-013:** The system MUST record data coverage and uncertainty so that missing or unsupported information is not represented as absence of hazard or ethical risk.  
  **Given** a source has no record or does not cover a location/time, **When** the result is shown, **Then** it is labeled unknown, unavailable, or unsupported as applicable, not “no risk.”

### Map, table, evidence, and access

- **FR-014:** The system MUST provide a publicly accessible map of source-derived flood overlaps at supported manufacturing-facility locations, with company, supplier depth, flood information, and ethical-risk signal.  
  **Given** a published overlap has supported facility coordinates and a usable spatial match, **When** a public user opens the map, **Then** the facility is shown with its source-derived context and links to evidence detail.
- **FR-015:** The system MUST provide a publicly accessible source-linked table of flood overlaps containing company, supplier/relationship depth, facility, flood information, ethical-risk signal, provider attribution, and match/coverage status.  
  **Given** one or more results are published, **When** a public user opens the table, **Then** every row includes these fields or an explicit unavailable value and links to evidence detail.
- **FR-016:** The system MUST provide evidence detail for each published flood overlap, including provider record references, relevant dates, entity/spatial-match basis, and known limitations.  
  **Given** a public user selects a result, **When** its detail is opened, **Then** the user can trace the Sayari and flood claims to their originating records and see that the entry is a signal, not a final judgment.
- **FR-017:** The system MUST permit public read-only access to published map, table, and displayed source attribution/evidence, while restricting editing and draft curation to the curator. Only license-cleared Sayari-derived content may be published. Draft records MUST be stored outside the deployed public artifact and excluded from public deployment.  
  **Given** a public user opens the product, **When** the user views published information, **Then** the user can read it without curator privileges and cannot change records; **and given** an unpublished draft exists, **when** a public user accesses the product, **then** the draft is not exposed.
- **FR-018:** The system MUST show explicit empty and error states on the company, map, table, and evidence-detail screens as defined in Section 3, and MUST NOT display failed or partial loads as complete results.  
  **Given** a screen has no data or encounters a loading/source failure, **When** a user opens it, **Then** the screen explains the empty/error condition and any available recovery path without converting failure into a negative risk result.
- **FR-019:** The system MUST join records by preserving the chain from selected company to Sayari supplier entity and relationship depth to manufacturing facility, then spatially compare supported facility coordinates with provider-supplied hazard affected-area geometry. It MUST NOT infer a facility location from a headquarters address or invent a proximity radius for point-only hazard records.  
  **Given** Sayari identifies supplier entities, relationships, and facility coordinates and a hazard provider supplies usable affected-area geometry, **When** the records are joined, **Then** the match retains its entity path and spatial-match basis; **and given** any required link or geometry is unavailable, **when** the join is evaluated, **then** the result is marked unresolved or contextual rather than a facility exposure flag.
- **FR-020:** The system MUST provide a keyboard-accessible, semantic table and evidence-detail path equivalent to map results. Map information MUST NOT be available only through visual or pointer interaction. Status MUST NOT be conveyed by color alone; controls and links MUST have accessible names and visible focus. The primary results flow MUST meet WCAG 2.2 AA contrast and keyboard-operability criteria.  
  **Given** a user navigates without a pointer or uses assistive technology, **When** they inspect published results, **Then** every map result's company, supplier depth, facility, flood status, ethical-risk signal, source links, and limitations are available in semantic table/detail content with visible keyboard focus and meaningful headers; **and given** the flow is checked for conformance, **then** no WCAG 2.2 AA contrast or keyboard-operability failure is present.

## 6. Key entities and data model

Each entity below supports at least one screen and/or functional requirement. No field is intended for collection unless it supports the listed review, ranking, validation, or display needs.

- **Company business:** The apparel/textile business being evaluated within a parent or reporting entity. Fields: stable record identifier; displayed business name; reporting/company entity name; sector/boundary note; cohort inclusion basis or exclusion reason; latest annual-report period/source; selection rank within the documented cohort; selection status. Used by cohort register, company screen, map, and table.
- **Revenue observation:** One reported revenue figure used to compare a company business. Fields: company business reference; reporting period; reported amount; reported currency; apparel/textile basis/source description; annual-report source reference; normalized USD amount when available; exchange rate; rate period/method; FX source reference; comparison status. Used by company screen and ranking.
- **Supplier organization:** A supplier entity linked to a selected company. Fields: stable record identifier; displayed name; source entity reference when available. Used by map, table, and evidence detail.
- **Supplier relationship:** A source-supported link between a selected company business and supplier organization. Fields: company business reference; supplier reference; relationship depth/tier; Sayari source reference; source observation/retrieval date; relationship status/uncertainty. Used by all exposure screens.
- **Manufacturing facility:** A facility associated with a supplier. Fields: stable record identifier; supplier reference; facility name when available; facility type; address/location description; coordinates when supported; geographic coverage status; source reference; source observation/retrieval date. Used by map, table, and evidence detail.
- **Source record:** An origin record used to support revenue, relationship, facility, flood, or ethical-risk claims. Fields: stable reference; publisher/provider; title or description; source URL or provider record identifier; source type; publication/observation date when available; retrieval date; claim/observation supported; availability/status. Used wherever evidence is shown.
- **Publication clearance record (private curation data):** Sayari-derived field/display scope; private license reference; decision/status; applicable attribution/retention conditions; reviewer; review date. Used as the release gate for FR-011 and FR-017. Do not deploy license text or private clearance notes.
- **Flood observation:** A flood category/event that may spatially relate to a facility. Fields: provider/dataset (NOAA or flood-classified GDACS); flood type; provider's own category/threshold when available; observation/event time or time range; current/historical designation; affected-area geometry or event point when supplied; geographic/time coverage status; source reference; uncertainty. Used by map, table, evidence detail, and spatial join.
- **Ethical-risk indicator:** A Sayari signal associated with a supplier organization or facility. Fields: subject reference; indicator type (forced-labor risk, sanctions link, or opaque ownership); indicator wording/status from source; source reference; observation/retrieval date; uncertainty. Used by table, evidence detail, and flag validation.
- **Facility-hazard match:** The spatial comparison between a manufacturing facility and a hazard observation. Fields: facility reference; hazard observation reference; match basis (within/intersects provider-supplied affected area, contextual point-only event, unsupported, or unmatched); match status; source geometry reference when available; limitation note. Used by map, table, evidence detail, and flag creation.
- **Exposure flag:** A source-derived overlap associated with one company business and manufacturing facility. Fields: company business reference; supplier relationship reference; facility reference; hazard observation/match reference(s); ethical-risk indicator reference(s); status (draft, unresolved, published, withdrawn); source-derived summary; last updated date. Used by map, table, and evidence detail.

Relationship constraints:

- One company business may have multiple supplier relationships; each relationship identifies its recorded depth and supporting source.
- A supplier organization may have multiple manufacturing facilities.
- A facility may have multiple flood observations and ethical-risk indicators; retain separate source evidence rather than merging them into a single unsupported score.
- A facility-hazard match records the actual spatial relationship. A point-only hazard event without provider-supplied affected-area geometry is contextual, not proof that a facility is exposed.
- An exposure flag references the exact provider records and entity/spatial matches that support it. Provider provenance identifies the source; it is not independent verification.
- Public deployment contains only approved published records. Working drafts and uncleared Sayari data remain outside the deployable artifact.
- USD revenue may remain unavailable if an exchange rate or business-specific amount cannot be established; ranking status must then disclose the limitation.

## 7. Success criteria

### Measurable outcomes

- **SC-001:** The initial published company screen contains the five highest eligible businesses within a documented, pre-frozen candidate cohort, or is explicitly marked incomplete if evidence does not support selecting five. It does not claim a global top five.
- **SC-002:** Every published flag has a facility and supplier relationship with a recorded depth, a source-attributed flood observation in the selected dataset's own category, a Sayari ethical-risk indicator, and a documented entity/spatial match.
- **SC-003:** A public user can trace every published flag's hazard and ethical-risk claims to the originating provider records from the map or table.
- **SC-004:** Every public-facing result is read-only; draft curation is not exposed to public users.
- **SC-005:** In the defined empty/error scenarios, missing, unsupported, inaccessible, or failed data is labeled as such and is never shown as evidence of no risk.
- **SC-006:** Every map result can also be reached and understood through a semantic, keyboard-accessible table/detail path; keyboard-only navigation is tested before the demo.

No percentage accuracy target or user-validation target has been set. Underwriter validation is deferred beyond the first prototype.

## 8. Constraints, assumptions, and scope pressure

### Confirmed constraints

- Four hours total over two weeks (two hours per week), with a zero-dollar budget.
- Floods only are in scope for this prototype; earthquakes and other non-flood hazards are excluded.
- The five businesses are the top five within the documented candidate cohort, not a globally exhaustive ranking.
- Five apparel/textile businesses, selected on latest annual-report revenue for the apparel/textile business.
- Sayari license is available; the user states that public access is permitted. Before publication, the curator must confirm and record permission for each specific field and derived display.
- Facilities are limited to manufacturing facilities.
- Include all supplier tiers available in Sayari data and label depth.
- Use NOAA flood information and optionally flood-classified GDACS records where usable; USGS earthquake records are excluded from this flood prototype.
- Show a documented current/near-term window first; historical data is deferred unless feasible. Use only provider-defined flood categories/thresholds.
- Provide both a map and source-linked table.
- Treat Sayari and flood-provider records as source-attributed evidence, not independently verified claims.
- Keep drafts outside the deployed public artifact; publish only approved, license-cleared records.

### Assumptions (inferred)

- A curator prepares and publishes records; anyone can read the published map, table, and evidence.
- Draft records are not visible in the public view.
- Provider attribution identifies the record source; it is not independent confirmation, adjudication, or proof of a legal fact.
- No export/download capability is included in the first version.
- To bound the prototype, the initial candidate cohort contains at most 10 businesses (inferred); the five selected are only the top five within that cohort, not a global ranking.

### Scope pressure and proposed cuts

The full combination of cohort construction and five-company revenue comparison, all available supplier tiers, manufacturing-facility resolution, multiple flood providers, current and historical coverage, a public data join, an accessible map, and a source-linked table exceeds the four-hour first slice. Actual effort depends heavily on the Sayari export structure, field-level license terms, facility coordinates, and usable flood geometries.

To preserve the concept's core while reducing effort, the recommended order is:

1. Preserve the documented candidate cohort and cohort-bounded five-business result; do not imply global exhaustiveness.
2. Demonstrate one flood source (NOAA where the available facility geography is supported) and one small Sayari sample only after field-level license clearance. Add GDACS flood records later if usable.
3. Defer historical coverage, additional flood providers, all-company/all-tier coverage, and advanced map behavior. The semantic source-linked table remains an equivalent way to inspect each result.
4. Do not fabricate facility locations, invent a proximity radius, call an unsupported match an exposure, or claim complete supply-chain/hazard coverage.
5. Do not publish Sayari-derived data that has not passed the field-by-field license-clearance gate.

These are approved prototype boundaries for the flood-focused delivery; unbuilt items remain deferred rather than silently counted as complete.

## 9. Open questions

Carry forward from [CONCEPT-IDEA.md](./CONCEPT-IDEA.md):

1. Which businesses will be included in the documented candidate cohort, and do their annual reports provide comparable apparel/textile segment revenue?
2. Which geographies and manufacturing-facility locations are present in available Sayari data, and can NOAA or explicitly flood-classified GDACS records be matched to them?
3. Which selected flood feeds offer usable affected-area geometry and provider-defined categories for the current/near-term prototype window?
4. What exact Sayari export fields or entity references are available to connect businesses, supplier tiers, supplier entities, ethical-risk indicators, and manufacturing facilities?

Additional specification questions:

5. Which reputable annual-average exchange-rate source should be used when an annual report does not state a rate?
6. Does the applicable license permit each Sayari field and derived result to be publicly displayed, and what attribution or retention conditions apply?

## 10. Public data references and Sayari matching guidance

Use web search to discover source pages, but retrieve and cite the originating provider's record/feed rather than a search-result snippet. The initial official starting points found for this specification are:

- [NOAA National Water Prediction Service API information](https://water.noaa.gov/about/api): describes forecasts, observations, flood impacts, flood-category levels, and location metadata. Its published coverage is U.S.-focused, and its historical information is limited; do not present it as a global all-weather hazard source.
- [GDACS public site](https://www.gdacs.org/): starting point for global disaster information. Use only records explicitly classified as floods for this prototype; confirm the current feed URL, time coverage, category meaning, and whether affected-area geometry is available before treating a record as spatial exposure.

### Sayari-to-hazard matching procedure

1. Establish each selected apparel/textile business from the documented revenue ranking and identify its Sayari entity reference.
2. Follow Sayari's available company-to-supplier trade links, retaining each relationship and known tier/depth. Do not collapse intermediate entities or describe all suppliers as direct.
3. Select Sayari-linked manufacturing facilities. Use facility coordinates when supplied by the source; do not use a supplier headquarters as a proxy facility location.
4. Retrieve official NOAA flood records and, if usable, explicitly flood-classified GDACS records. Retain source links/IDs, dates, categories, and available geometry. Search-result pages are discovery aids, not evidence records. Do not include USGS earthquake data in this flood prototype.
5. Attach Sayari risk indicators to the exact supplier entity identified by Sayari. Associate an indicator with a facility only through the recorded Sayari relationship path.
6. Compare a facility point with provider-supplied affected-area geometry using containment/intersection. Do not invent a buffer around an event point. If only a point is provided, show it as contextual event information or mark the match unsupported rather than claiming facility exposure.
7. Before publication, confirm and record that the license permits each Sayari-derived field and derived display; then publish only cleared records with the Sayari entity path, facility location/match status, flood record and provider category, ethical-risk indicator, retrieval/observation dates, and coverage limitations. Describe evidence as source-attributed, not independently verified.

## 11. Three least-certain areas

1. **Candidate cohort and comparable revenues.** The ranking is bounded to a documented candidate cohort, not a global top-five claim. Publish the candidate register with inclusion/exclusion basis and confirm whether enough comparable segment-revenue records support a ranking.
2. **Sayari-to-facility identity chain.** The available Sayari fields and facility coordinates are unknown. To resolve this, inspect a sample export and confirm which identifiers connect selected businesses to suppliers, supplier tiers, risk indicators, and facility records.
3. **Flood geometry and four-hour scope.** Flood sources may not provide suitable affected-area geometry for available facilities. Compare actual facility coordinates with an official NOAA flood record (and GDACS only if useful); if no supported match exists, demonstrate the unresolved state instead of fabricating an overlap.
