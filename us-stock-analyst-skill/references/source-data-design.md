# Source and data design

## Source hierarchy

| Need | Preferred source | Use and checks |
|---|---|---|
| Identity, filings, reported results, risk factors, debt, share count | SEC EDGAR filing page and the filed document | Confirm issuer/CIK, filing form, period end, filed date, units, accounting basis, amendments, and exhibits. Use the filing as the record for reported figures. |
| Filing chronology and machine-readable facts | SEC submissions and XBRL APIs | Locate filings and candidate facts. Verify material facts in the underlying filing, especially where tags, units, duration, or company context may differ. |
| Earnings release, company guidance, segment presentation, scheduled events | Issuer's official investor-relations site; related 8-K/6-K and exhibits | Label management statements as company statements. Reconcile non-GAAP metrics and forward guidance to filing context where possible. Confirm that the domain is the issuer's official IR site. |
| Current or recent market quote | Listing exchange quote page or reputable public quote page | Record timestamp, currency, exchange, regular/extended-hours status, and whether delayed. Don't use SEC filings as a quote source. If timestamp or delay is unclear, label the quote accordingly. |
| Government rates and macroeconomic series | U.S. Treasury, Federal Reserve, FRED, or relevant government agency | Record series, observation date, units, and whether it is a market observation or an analyst assumption. |
| Industry, legal, or regulatory context | Relevant regulator, court, agency, standard setter, or company filing | Use authoritative documents for material claims. Use reputable news for context and discovery, not as the sole evidence for a key financial figure. |

No paid API is required. Public pages and web search are sufficient for the intended human-scale workflow. If the host cannot reach a source or market quote, disclose the gap instead of inferring it.

For a checked issuer example, [Apple Investor Relations](https://investor.apple.com/investor-relations/) organizes quarterly releases, financial statements, 10-Q/10-K links, and investor updates; its [SEC Filings page](https://investor.apple.com/sec-filings/) lists filing records. This illustrates how an issuer's IR portal can help discover primary company materials. For any other company, confirm the official domain and cross-check material reported figures against SEC EDGAR.

## SEC filing route

1. Search [SEC EDGAR](https://www.sec.gov/search-filings) by ticker, legal name, or CIK. Confirm the issuer and listing; tickers can be reused or refer to multiple share classes.
2. Read the latest 10-K and 10-Q (or 20-F and 6-K for a foreign private issuer). Check later 8-K/6-K filings and exhibits through the analysis date for results, guidance, acquisitions, financing, litigation, or other material events.
3. Read the relevant filing sections: business/segments, MD&A, financial statements and notes, risk factors, liquidity/capital resources, commitments, and subsequent events. For governance or compensation, use DEF 14A when relevant.
4. Open the official IR release and presentation for recent management commentary. Search the SEC filing index for the associated 8-K/6-K and exhibits. Treat the filed release and the IR site as related primary sources, while retaining the reporting-date distinction.
5. For the quote, find the listing exchange or a public quote page, note its timestamp and delay status, and use it only for market-cap or per-share comparison. Keep quote date separate from filing date.

Common forms include 10-K (annual report), 10-Q (quarterly report), 8-K (current report), DEF 14A (proxy), 20-F (foreign private issuer annual report), and 6-K (foreign private issuer current report). The relevant filing regime depends on issuer status; don't assume a US domestic company filing calendar for an ADR.

## Public SEC API routes

These routes are optional aids for getting public facts. The SEC says data.sec.gov submissions and XBRL APIs do not require an API key. Access policy still applies.

| Route | Purpose | Caution |
|---|---|---|
| `https://data.sec.gov/submissions/CIK##########.json` | Filing history and issuer metadata by 10-digit CIK, padded with leading zeroes | Current structure includes at least one year or 1,000 recent filings (whichever is more); older filings may be in referenced historical files. |
| `https://data.sec.gov/api/xbrl/companyfacts/CIK##########.json` | Standardized facts for a filing entity across supported taxonomies | Discovery/calculation aid, not a substitute for the filing. Check units, start/end dates, accession, form, amendments, and share/dilution context. |
| `https://data.sec.gov/api/xbrl/companyconcept/CIK##########/us-gaap/ConceptTag.json` | Facts for one company and taxonomy concept | Concept tags may not capture company-specific definitions or all custom disclosures. |
| `https://data.sec.gov/api/xbrl/frames/us-gaap/ConceptTag/USD/CY2025Q1.json` | Cross-company data aligned to approximate calendar periods | Issuers' fiscal periods vary; a frame's period can differ from the issuer's quarter. Avoid treating it as an issuer-specific fiscal quarter without checking. |

The SEC explains that companyfacts/companyconcept aggregate facts using non-custom taxonomies and facts applying to the entire filing entity. Companies can also use custom taxonomies. The XBRL frame API aligns facts approximately to calendar periods. For unusual, material, segment-specific, or company-defined metrics, inspect the inline XBRL and filing note directly. See the SEC's [API documentation](https://www.sec.gov/search-filings/edgar-application-programming-interfaces).

For scripts, declare an identifying User-Agent and comply with the SEC's fair-access guidance (the SEC currently states a maximum access rate of 10 requests per second). Avoid repeated or bulk requests for a one-company analysis. See [SEC Developer Resources](https://www.sec.gov/about/developer-resources) and [SEC Webmaster FAQs](https://www.sec.gov/about/webmaster-frequently-asked-questions).

## Data capture and citation rules

For each important metric, capture:

- Value, unit, currency, and definition.
- Period start/end or as-of date, fiscal/calendar basis, and whether annual, quarterly, TTM, or point-in-time.
- GAAP or adjusted status, and any reconciliation or exclusion.
- Source title, form, filed/published date, direct URL, and accession number when available.
- Any transformation: sum of four quarters, annualization, normalization, conversion, or analyst estimate.

For market data, also capture quote timestamp, exchange, currency, and delay status. Cite the underlying filing/page, not only a search snippet. If the direct document is inaccessible, say so and lower confidence.

## Freshness and conflict handling

- Search again on the analysis date for subsequent filings and material company updates. A recently published IR release may contain preliminary numbers that are later corrected or filed with detail.
- When the IR release and SEC filing differ, identify the difference, dates, accounting basis, and which number is used for valuation. Do not blend them without explanation.
- When SEC XBRL and the filed statement disagree because of tagging, restatement, units, or context, use the filing and explain the reconciliation.
- A quote from a prior close is not an intraday quote. If the market is closed or the quote source is delayed, say so.
- Historical information can be revised or reclassified. Preserve the filing version/accession and note later amendments/restatements.
