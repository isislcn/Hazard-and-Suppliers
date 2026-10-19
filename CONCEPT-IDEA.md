# Apparel and Textile Supplier Flood Exposure Map (inferred)

**Status:** Approved concept  
**Initial screen:** Top five apparel/textile businesses within a documented cohort of up to 10 candidates (inferred), ranked by latest comparable segment revenue
**Intended audience:** Insurance underwriters

For the revenue ranking, use the apparel/textile business rather than the whole corporate group. Use each company's latest annual report as the revenue source. Convert amounts to USD using the rate stated in the annual report when available.

If an annual report does not state an exchange rate, use a reputable published annual average exchange rate for that reporting year.

## The idea

Create a map that brings together supplier facility and trade-link information from Sayari with public flood information. For the initial screen, compare the latest apparel/textile-business revenue for an explicitly documented candidate cohort, then show where available supplier manufacturing facilities intersect with supported flood areas and Sayari ethical-risk signals. The result is the top five within that documented cohort, not a claim about the five largest businesses globally.

The map is intended to flag supplier manufacturing facilities where a provider-supported flood area coincides with a Sayari signal such as forced-labor risk, a sanctions link, or opaque ownership. Describe records as **provider-sourced** or **source-attributed**, not independently verified: provenance identifies where a claim came from, but does not confirm that the underlying claim is true. No separate human fact-check is required for this prototype. The map is evidence for underwriters to review; it does not make coverage or ethical-risk decisions or establish a final legal or ethical finding.

## The problem and current evidence

The initial hypothesis is that insurance underwriters may benefit from seeing disaster exposure and ethical-risk signals together for suppliers. This need has not yet been validated with customer evidence. No current insurer workflow or alternative is known at this stage; this does not establish that no such workflow exists.

## Who it serves

- **Primary users:** insurance underwriters deciding whether or how to provide coverage.
- **Intended use:** review supplier-related evidence about hazard exposure and ethical-risk signals while assessing coverage.

## Initial scope

- Focus only on apparel and textiles.
- Screen the top five within a documented curator-defined candidate cohort of up to 10 businesses (inferred to bound the prototype). Freeze and publish cohort membership and eligibility criteria before comparing revenues; do not claim it represents all apparel/textile businesses globally.
- Use Sayari for available supplier facilities and trade links; licensed Sayari access is available.
- Limit facility screening to manufacturing facilities.
- Focus this prototype on floods. Use NOAA's National Water Prediction Service as the primary public flood source where its U.S.-focused coverage fits. Include GDACS only when an official record is explicitly a flood and provides usable data. Do not use USGS earthquake data in this flood prototype. Do not treat search-result snippets as source records.
- Include all supplier tiers available in Sayari data and label the supplier depth.
- Show current/near-term flood conditions in the first prototype. Historical flood events are deferred unless they can be added without exceeding the four-hour first-slice limit.
- Use the source's flood category/threshold as published; do not create a cross-provider high-risk threshold. If no provider-defined category is available, do not label the flood high-risk.
- Flag overlaps between high-hazard exposure and the stated ethical-risk signals: forced-labor risk, sanctions links, and opaque ownership.
- Treat Sayari and flood-provider records as evidence provenance, not independent verification. A Sayari-derived field may be published only after the curator has confirmed that the specific field and its public display are allowed by the applicable license.
- Deliver a map plus a source-linked table of flags.
- The user states that Sayari's license permits public access. Before publishing, the curator must still confirm and record that each specific field and derived display is allowed. Working drafts and uncleared fields stay outside the public deployment.

## How the data is joined

1. Create and publish an explicit candidate-cohort register before comparing revenue: business name, cohort eligibility criteria, annual-report period/source, apparel/textile segment basis, and any exclusion reason. Limit the initial cohort to at most 10 candidates (inferred) and freeze membership before calculating ranks. Rank comparable candidates by documented segment revenue and USD conversion. If reporting periods or business boundaries are not comparable, mark the ranking unresolved. Call the result the top five only within this documented cohort; never imply an exhaustive global ranking.
2. Keep only supplier manufacturing facilities that Sayari links to those supplier entities. Use the facility's provider-supplied coordinates when available. Do not guess a facility location from a supplier's headquarters or an incomplete address.
3. Find official public flood records through web search, then use the originating provider's record/feed for the data. Search results help locate sources; they are not evidence. Start with NOAA's National Water Prediction Service API where its U.S.-focused coverage fits. Include a GDACS record only when it represents flooding and has usable data. The chosen records and source links must be stored with provider, dates, flood category, and supplied geometry.
4. Match facility coordinates to the official hazard record's supplied affected area or geometry. For event records that provide only a point and no affected-area geometry, do not invent a radius or claim that a facility is exposed; show the event as contextual information only or leave the overlap unresolved.
5. Attach Sayari ethical-risk indicators to the supplier entity they identify, and connect those indicators to facilities only through the recorded Sayari supplier/facility relationship. Preserve entity and facility distinctions.
6. Publish a source-derived overlap with the source names, record links/identifiers, observation dates, relationship depth, and any known data-coverage or location limitations. A source-derived flag is a signal for review, not proof of legal wrongdoing or a final risk judgment.

## Evidence and review principles

- Treat map entries as source-derived signals for underwriters, not proof of wrongdoing or a definitive risk finding.
- Keep the source and evidence behind each published flag visible so a reviewer can check it.
- Say “provider-sourced” or “source-attributed,” not “verified.” Provider provenance is not independent confirmation of the underlying claim.
- Before publishing any Sayari-derived data, confirm that the exact fields and derived display are permitted by the license. Do not publish Sayari-derived content until this release gate is satisfied.
- Make gaps in coverage and unavailable information explicit rather than presenting them as evidence of no risk.
- Do not imply that Sayari or hazard datasets establish an insurer's coverage decision.

## Success

Every published flag for the five-company screen is traceable to its Sayari indicator and relevant public hazard-provider record, with source dates and a documented spatial/entity match. No percentage or numeric accuracy threshold has been set.

User validation with underwriters is deferred to a later phase; it is not a first-prototype success requirement. The four-hour prototype is a bounded demonstration, not completion of the full cohort, supplier, flood-history, or map coverage.

## Constraints

The available delivery time is four hours total over two weeks (two hours per week), with a zero-dollar budget. The relevant geographic coverage is limited to what the available data supports.

## Public data starting points

- [NOAA National Water Prediction Service API information](https://water.noaa.gov/about/api) — public API information includes forecasts, observations, flood impacts, and flood-category levels; the listed coverage is not global.
- [GDACS](https://www.gdacs.org/) — public global disaster awareness site. Use only flood records for this prototype, and confirm the official feed, flood classification, and geometry coverage before using a record.

## Out of scope

- Making, recommending, or automating underwriting, coverage, pricing, or claims decisions.
- Making final determinations that a company or supplier uses forced labor, violates sanctions, or is ethically acceptable or unacceptable.
- Issuing live alerts, forecasting events, or supporting emergency response.
- Publishing supplier/facility exposure results for more than the five selected apparel/textile businesses.
- Treating missing facility, trade-link, hazard, or ethics data as proof that a supplier is safe or exposed.
- Treating a map flag as an independently verified legal finding or as a substitute for an underwriter's review.
- Earthquakes and all non-flood hazards in this prototype.
- Publishing Sayari-derived fields before confirming that the license permits the specific public display.

## Open questions

- Which candidate businesses will be included in the documented cohort, and do the available annual reports provide comparable business-specific revenue?
- Which geographies and facility locations are actually present in the available Sayari data, and can NOAA or flood-specific GDACS records be matched to them?
- Which chosen flood feeds supply suitable affected-area geometry and provider-defined categories for the prototype's selected time window?
- What exact Sayari export fields/entity references are available to link company businesses, supplier tiers, supplier entities, ethical-risk indicators, and manufacturing facilities?
- Does the applicable Sayari license permit public display of each specific field and derived result planned for publication?
- Which reputable annual-average exchange-rate source should be used when an annual report does not state a rate?
