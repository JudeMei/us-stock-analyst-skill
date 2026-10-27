# US Stock Analyst Skill

A reusable ChatGPT/Codex skill for fundamental research and value-oriented valuation of US-listed companies. The package is instruction-led and uses public filings, issuer investor-relations material, web search, and other public sources. It does not require a paid market-data API.

**Documentation checked:** 26 October 2026. Product availability and menus can vary by account, workspace policy, and app version.

## Package contents

```text
us-stock-analyst-skill/
├── SKILL.md
├── README.md
├── agents/
│   └── openai.yaml
└── references/
    ├── output-template.md
    ├── practical-caveats.md
    ├── source-data-design.md
    ├── test-cases.md
    └── valuation-workflow.md
```

The ZIP contains this single top-level skill folder. The optional `agents/openai.yaml` supplies a display name and starter prompt. The skill itself has no scripts or tool dependencies; live research requires that the host provide web search or access to the documents you supply.

## Install in ChatGPT

1. Open **Plugins → Plugin Directory → Skills** in ChatGPT.
2. Choose **Create → Upload from your computer** and select `us-stock-analyst-skill.zip` (or the extracted skill folder if the upload dialog asks for a folder).
3. Review the scan result and install the skill. ChatGPT may flag a skill for review or block it; follow the workspace's review controls.
4. Start a new chat and invoke it with `@US Stock Analyst`, or ask for an analysis that clearly matches its description.

The ChatGPT Skills interface is available to eligible Business, Enterprise, Healthcare, and Edu users, subject to workspace settings and product availability. If **Skills** or uploading is not available, use the supported **Create with editor/chat** route if offered, or install locally in Codex below. An administrator may control workspace permissions.

## Install in Codex

For a user-wide installation on macOS, extract the ZIP and copy the `us-stock-analyst-skill` folder to:

```text
~/.agents/skills/us-stock-analyst/
```

For a repository-only installation, put the folder here instead:

```text
<repository>/.agents/skills/us-stock-analyst/
```

Keep `SKILL.md` at the root of the `us-stock-analyst` folder. Codex detects skill changes automatically; restart Codex if the skill does not appear. In Codex, type `$` and select **US Stock Analyst** to invoke it explicitly. In the CLI or IDE extension, `/skills` can show available skills.

## First-use setup

1. Confirm that the host has web search or browser access enabled. A skill supplies the research workflow; it does not add search or quote tools by itself.
2. Ask for a specific issuer/ticker and the intended horizon, such as long-term, next-quarter review, or both.
3. For current analysis, ask it to verify the latest annual/quarterly filing and material subsequent filings, and to date any market quote it uses.
4. Review the cited filings and assumptions. Use the bundled test prompts in `references/test-cases.md` to check activation and output quality after installation or edits.

## Public-source model

- **Financial reporting and material events:** SEC EDGAR filings (10-K, 10-Q, 8-K; for foreign private issuers, 20-F/6-K), exhibits, and SEC XBRL APIs.
- **Issuer context:** the company's official investor-relations site for releases, presentations, guidance, and event dates; reconcile important non-GAAP measures to filed GAAP results.
- **Market quote:** a public exchange or other reputable quote page. Record price, timestamp, currency, and any delay disclosure. EDGAR is not a live stock-price source.
- **Rates and macro inputs:** official public sources such as U.S. Treasury and Federal Reserve/FRED publications; record the observation date and distinguish data from valuation assumptions.

See `references/source-data-design.md` for source selection, SEC API routes, freshness, and limitations. SEC company submissions and XBRL APIs do not require API keys, but programmatic access still has to follow SEC access requirements. The skill uses web search/public pages where direct API access is unavailable.

## Current official setup references

- [Build skills — ChatGPT Learn](https://learn.chatgpt.com/docs/build-skills): `SKILL.md` format, skill discovery/invocation, Codex locations, optional metadata, and packaging guidance.
- [Skills in ChatGPT — OpenAI Help Center](https://help.openai.com/en/articles/20001066-skills-in-chatgpt): current ChatGPT access, upload, review, sharing, and workspace availability.
- [OpenAI API Skills guide](https://developers.openai.com/api/docs/guides/tools-skills): a separate developer/API route for uploading and attaching skills to API environments. It is not required for ChatGPT or local Codex use.

## Official SEC references

- [EDGAR Search Filings](https://www.sec.gov/search-filings): public company and filing search.
- [EDGAR Application Programming Interfaces](https://www.sec.gov/search-filings/edgar-application-programming-interfaces): submissions, XBRL company facts/concepts/frames, timing, and data limitations.
- [SEC Developer Resources](https://www.sec.gov/about/developer-resources): data API and EDGAR access resources.
- [SEC Webmaster FAQs](https://www.sec.gov/about/webmaster-frequently-asked-questions): User-Agent declaration, fair-access rate, and related access notes.
- [data.sec.gov](https://data.sec.gov/): SEC EDGAR API landing page.

## Practical limitations

Public sources can be delayed, incomplete, revised, inconsistent in definitions, or hard to compare across companies. Search snippets are not enough for important claims. SEC XBRL aggregations may omit custom-tagged disclosures or facts that do not apply to the whole filing entity; always verify material figures in the filing. A web-enabled skill can still misread a filing, so inspect calculations and sources before using them. See `references/practical-caveats.md`.

This skill provides general educational research, not individualized investment, legal, or tax advice. Market prices and valuations can change, and scenario values are estimates rather than predictions.
