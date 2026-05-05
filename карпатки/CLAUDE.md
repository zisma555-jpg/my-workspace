# CLAUDE.md — LLM Wiki Schema
# Marketplace Business: Krymsky Khan & Travy Gornogo Kryma
# Platforms: Ozon, Wildberries

---

## Purpose

This wiki is a persistent, LLM-maintained knowledge base for managing and growing two marketplace brands:

- **Krymsky Khan** — bronze jewelry and accessories
- **Travy Gornogo Kryma** — herbal teas, dietary supplements, and herbal pillows from Crimea

It supports decision-making in: marketing, product strategy, sales analytics, competitor research, and overall business operations on Ozon and Wildberries.

---

## Directory Layout

```
карпатки/
├── raw/          # Immutable source files. Never edit these.
├── wiki/         # LLM-generated and LLM-maintained markdown pages.
├── index.md      # Entry point: map of all wiki pages with one-line summaries.
├── CLAUDE.md     # This file. The schema and operating rules.
└── log.md        # Ingest log: what was processed, when, and what changed.
```

---

## Wiki Structure

The `wiki/` directory must contain the following pages. Create a page when the first relevant source is ingested. Do not create empty pages.

### Brand Pages
- `wiki/krymsky-khan.md` — product catalog, positioning, pricing, USPs, target audience
- `wiki/travy-gornogo-kryma.md` — product catalog, positioning, pricing, USPs, target audience

### Platform Pages
- `wiki/ozon.md` — platform-specific rules, fee structure, ranking factors, ad formats, logistics
- `wiki/wildberries.md` — platform-specific rules, fee structure, ranking factors, ad formats, logistics

### Strategy Pages
- `wiki/marketing.md` — proven tactics, content strategy, SEO keywords, ad campaigns, seasonal patterns
- `wiki/competitors.md` — competitor profiles, pricing benchmarks, their strengths and weaknesses
- `wiki/product-strategy.md` — new product ideas, assortment gaps, bundling ideas, pricing strategy
- `wiki/sales-analytics.md` — sales patterns, bestsellers, slow movers, conversion insights, seasonality

### Knowledge Pages
- `wiki/market-overview.md` — Russian marketplace market context, consumer trends, regulatory notes
- `wiki/supplier-ops.md` — sourcing, production notes, packaging, stock management

---

## Source Types & Ingest Rules

When a new source is placed in `raw/`, process it according to its type:

### PDF Articles
- Extract key facts, statistics, frameworks, and actionable insights.
- Discard generic filler; keep only information relevant to the wiki's purpose.
- Distribute extracted knowledge across the relevant wiki pages (do not create one page per PDF).

### YouTube Video Links
- Treat the link as a pointer to a video. Record its title, channel, and URL in `log.md`.
- Extract knowledge from transcripts or descriptions if provided alongside the link.
- Tag insights with the source video for traceability.

### Personal Notes (owner's own text)
- These are first-person observations about products, sales, customers, or operations.
- Treat them as ground truth. Prioritize them over third-party sources when there is conflict.
- Tag extracted insights with `[Owner note]` to distinguish them from external sources.

---

## Operations

### Ingest
**Trigger:** A new file appears in `raw/` or the owner asks to ingest a source.

1. Identify the source type.
2. Extract relevant knowledge.
3. Update the appropriate wiki pages — add, revise, or expand content. Do not delete existing knowledge unless it is directly contradicted by the new source.
4. Append an entry to `log.md` with: date, source name, pages updated, and a one-line summary of what changed.
5. Update `index.md` if any new pages were created.

### Query
**Trigger:** The owner asks a business question.

1. Identify which wiki pages are relevant to the question.
2. Synthesize an answer from those pages.
3. If the wiki does not contain enough information to answer, say so explicitly and suggest what source type could fill the gap.
4. Do not invent facts not present in the wiki.

### Lint
**Trigger:** The owner asks to lint the wiki, or after every 10 ingests.

Check for:
- Pages that are stubs (fewer than 5 meaningful bullet points) — flag as incomplete.
- Contradictions between pages — flag and ask the owner to resolve.
- Wiki pages that reference a source not listed in `log.md` — flag as untraced.
- Sections in `index.md` that point to non-existent pages — fix automatically.
- Missing pages that should exist based on accumulated sources — suggest creating them.

---

## Content Rules

- Write all wiki content in **Russian** unless a term is a proper name or platform-specific label.
- Use bullet points and short paragraphs. No walls of text.
- Every factual claim should be traceable to a source (inline tag is enough: `[источник: название]`).
- Owner notes override external sources. Mark the override if it happens.
- Do not pad pages. A short accurate page is better than a long vague one.
- Prices and statistics become stale. Mark any figure older than 6 months with `[устарело?]`.

---

## index.md Format

`index.md` must stay up to date as a flat list:

```
# Wiki Index

- [Krymsky Khan](wiki/krymsky-khan.md) — бренд: украшения и аксессуары из бронзы
- [Travy Gornogo Kryma](wiki/travy-gornogo-kryma.md) — бренд: травяные чаи, БАДы, подушки
- [Ozon](wiki/ozon.md) — правила, комиссии, продвижение на Ozon
- [Wildberries](wiki/wildberries.md) — правила, комиссии, продвижение на WB
- [Маркетинг](wiki/marketing.md) — стратегии, SEO, реклама, сезонность
- [Конкуренты](wiki/competitors.md) — профили, цены, анализ
- [Продуктовая стратегия](wiki/product-strategy.md) — новинки, ассортимент, ценообразование
- [Аналитика продаж](wiki/sales-analytics.md) — динамика, хиты, аутсайдеры
- [Обзор рынка](wiki/market-overview.md) — тренды, контекст, регуляторика
- [Поставки и операции](wiki/supplier-ops.md) — производство, упаковка, склад
```

---

## log.md Format

Each ingest entry:

```
## YYYY-MM-DD — [название источника]
- Тип: PDF / YouTube / заметка владельца
- Обновлены страницы: wiki/xxx.md, wiki/yyy.md
- Итог: [одна строка — что добавлено или изменено]
```
