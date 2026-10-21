# Policyholder Supplier-Risk Screening: A Build Playbook

How to rebuild the "hidden supplier accumulation" screen for any list of policyholders: drop in the companies, get back shared supplier countries, flood context, and Sayari risk flags, in aggregated form.

**Audience:** analysts and developers at an insurer, broker, or research team.
**Reference build:** the apparel prototype (six policyholders, 43 suppliers, 11 countries), data retrieved 20 October 2026.

---

## 1. What you will produce

For a list of policyholders (insurance clients), the screen answers four questions:

| Question | Output |
|---|---|
| Where are each policyholder's suppliers? | Supplier counts by policyholder and country |
| Where does supply overlap? | Countries relied on by several policyholders ("shared dependence") |
| Where does shared supply meet hazard activity? | "Focus countries": shared by 3+ policyholders and hit by at least one flood in the window |
| Which suppliers need a closer look? | Counts of Sayari forced-labor, sanctions, and ownership flags by country and policyholder |

The result supports decisions at two moments:

- **Before an event:** which policyholders to warn, and where losses may cluster.
- **After an event:** which claims to prioritize, and which payees or vendors to check before money moves.

## 2. Before you start

| Requirement | Notes |
|---|---|
| Sayari access | A licensed Sayari account, through the Sayari MCP connector or the Sayari API (docs.sayari.com). Confirm in writing which fields and derived displays your license allows you to show, and to whom. |
| Hazard data | GDACS flood feed (public, CC BY 4.0). Add NOAA National Water Prediction Service for U.S. sites. |
| Revenue data (optional) | Public annual reports, if you rank policyholders by size. |
| Tools | Python 3 for data processing. A static HTML page with Leaflet for display. No paid map service is needed. |
| Time | About 30–45 minutes per policyholder for resolution and supplier review, plus a one-off 2–3 hours for the pipeline. |

## 3. Step 1: Prepare the policyholder list

Fill in `policyholders_template.csv`, one row per policyholder:

| Column | Required | Example | Why |
|---|---|---|---|
| `policyholder` | yes | lululemon | Display name |
| `legal_name` | yes | lululemon athletica inc. | Used to search Sayari |
| `hq_country` | yes | USA | Narrows the search |
| `identifier_type` | recommended | LEI / CUSIP / company number | Resolves the right record; names alone are unreliable |
| `identifier_value` | recommended | 550021109 | |
| `importer_hint` | optional | LULULEMON USA INC | The subsidiary that appears on customs records, if you know it |
| `rank_metric`, `rank_value`, `currency`, `fiscal_period`, `source_url` | optional | Apparel revenue, 11100, USD, FY2025, (report URL) | Only if you rank or size the portfolio |

**If you rank policyholders,** fix the candidate list before comparing figures. Use the most comparable figure for each company (a segment figure where one is reported), and convert currencies using one stated source, such as the Federal Reserve G.5A annual averages.

## 4. Step 2: Resolve each policyholder to a Sayari record

1. Search by legal name plus country (Sayari MCP: `search_entities`; for broad names, run `search_entity_facets` first).
2. Choose the record whose **identifiers** match: LEI, CUSIP, national registry number, or U.S. FEI. Do not pick by name alone.
3. Large groups are often fragmented across many trade-record name variants. If the parent has few trade links, use the **importer of record** instead: the subsidiary named on customs filings (in the reference build, Old Navy LLC for Gap, UNIQLO USA LLC for Fast Retailing, NIKE USA, INC. for Nike).
4. Record the chosen entity ID, its label, and the reason it was chosen. This is your audit trail.

## 5. Step 3: Pull and clean suppliers

1. **Pull tier-1 suppliers:** `traverse_network(entity_id, relationships=["receives_from"], max_depth=1, limit=25)`. Each result is a company that ships to the policyholder in Sayari's trade records.
2. **Optional tier 2:** for selected suppliers, read `receives_from` from `get_entity_profile`. Label every supplier with its tier.
3. **Remove records that are not suppliers:**
   - freight forwarders and logistics firms (for example Maersk, Damco, DSV, Kuehne+Nagel, DHL, DB Schenker, Expeditors, and 3PL warehouses);
   - the policyholder's own group companies and retail stores;
   - natural persons;
   - records with no country;
   - goods outside the sector you are screening.
4. **Cap the sample** (the reference build kept up to 8 per policyholder) and write down the cap.

> **Known issue:** in the reference build, product filters (HS codes) returned no results through the MCP connector, and `get_upstream_supply_chain` timed out without a filter. Plan for manual product review, or apply the filters through the API directly.

## 6. Step 4: Assign each supplier a country

- Use the country named in the supplier's Sayari address text. If no address is returned, use Sayari's country field, and record which basis you used.
- **Do not geocode addresses into map points.** A guessed location looks precise when it is not. Sayari's data model has address coordinate fields (`x`, `y`, `precision_code`); use them for site-level work only if your access returns them.
- Sayari sometimes types factories as "person" because of how trade records are parsed. Treat supplier type as unconfirmed unless a source says "manufacturing facility".

## 7. Step 5: Map Sayari flags to three signals

Count only flags on the supplier's own record. Ignore flags prefixed `psa_` ("possibly same as"), which Sayari borrows from a similar record. Exclude the country indices `basel_aml`, `cpi_score`, and `eu_high_risk_third`.

| Signal | Sayari risk factors (prefixes or ids) | Suggested action |
|---|---|---|
| Forced-labor risk | `forced_labor_uflpa_*`, `forced_labor_sheffield_hallam_*`, `forced_labor_aspi_*`, `forced_labor_xinjiang_*`, `forced_labor_wro_*`, `exports_ilab_forced_labor`, `*_forced_labor_reports_entity_adjacent` | Ask the policyholder about this supplier and its due diligence |
| Sanctions link | `sanctioned`, `sanctioned_adjacent`, `export_controls_adjacent` | Screen payees and vendors before paying a claim |
| Opaque ownership | `controlled_by_mass_business_registration`, `mass_address_usage`, `owned_by_tcsp_keyword_risk` | Confirm the ultimate owner before money moves |
| Other context | `exports_ilab_child_labor`, `soe_adjacent`, `regulatory_action` | Background for the policyholder conversation |

Use `lookup_risk_factors` to check definitions; Sayari's catalog changes over time. **Present flags as prompts to investigate, never as findings.**

## 8. Step 6: Add hazard context

1. Download the GDACS flood feed: `https://www.gdacs.org/xml/rss_fl_3m.xml` (floods updated in the last three months).
2. For each event, keep the event ID, ISO3 country code(s), alert level, start and end dates, whether it is ongoing, centre point, and report link.
3. Match events to suppliers **by country**. That is context, not exposure.
4. **Site-level upgrade:** fetch event outlines from `https://www.gdacs.org/gdacsapi/api/polygons/getgeometry?eventtype=FL&eventid=<id>&episodeid=<ep>` and test supplier coordinates against them. Never draw your own buffer around a point-only event. (This endpoint timed out on 20 Oct 2026; build in retries.)
5. Use the provider's own categories (GDACS Green, Orange, Red); do not invent a risk threshold. For U.S. sites, add NOAA National Water Prediction Service gauge flood categories.

## 9. Step 7: Aggregate

Compute these from the cleaned supplier table:

| Metric | Definition |
|---|---|
| Suppliers mapped | Count of cleaned supplier records |
| Countries covered | Distinct supplier countries |
| Shared dependence | A policyholder shares a country if at least one other policyholder has a supplier there |
| Flagged share | Suppliers with at least one forced-labor, sanctions, or ownership flag, divided by all suppliers |
| Focus countries | Countries with suppliers from at least 3 policyholders **and** at least 1 flood event in the window (adjust thresholds to the portfolio size, and state them) |
| Severe-alert reach | Suppliers in countries whose highest alert is Orange or Red |

Write the "so what" line from these numbers, not before computing them. In the reference build, supply was concentrated in countries with only Green alerts, while the Orange and Red alerts fell where few suppliers sat, and the callout says so.

## 10. Step 8: Publish safely

- **Two outputs:** a full working file (supplier-level, kept private) and a site file with **counts only**: no supplier names, IDs, or addresses. Check the site file with a script before every release.
- Keep a field-level license clearance record for every Sayari-derived value you display.
- Label the portfolio as illustrative if it is not real policy data.
- Show sources and retrieval dates beside every number.
- For maps opened from a local file: OpenStreetMap and CARTO tile servers block requests without a referrer. Embed country outlines (Natural Earth 1:110m, public domain) instead, or serve the page from a web server.

## 11. Checklist

- [ ] Policyholder list complete, with identifiers
- [ ] Each policyholder resolved to a Sayari record, with a written reason
- [ ] Suppliers pulled, cleaned, capped, and labelled with tier
- [ ] Country assigned with a recorded basis; no geocoding
- [ ] Flags mapped; `psa_` flags excluded from counts
- [ ] Hazard feed downloaded with a retrieval date
- [ ] Aggregates computed; "so what" written from the numbers
- [ ] Site file contains counts only (checked by script)
- [ ] License clearance recorded for every displayed Sayari-derived field
- [ ] Limits stated: country-level placement, flags are not findings, sample coverage, no real policy data

## 12. Where to take it next

- Site coordinates from a direct Sayari export, matched to GDACS flood outlines: country context becomes site exposure.
- Cyclone tracks and wind fields alongside floods.
- Dependence weighted by shipment volume or value instead of supplier counts.
- Deeper tiers and larger samples, to find suppliers shared by several policyholders.
- Historical events, to compare past floods with business-interruption losses.
