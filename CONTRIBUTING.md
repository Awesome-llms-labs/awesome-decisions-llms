# Contributing

Thanks for helping keep this the most current directory of LLMs and systems for decision-making!

## Adding an entry

1. **Check it fits:** an LLM or system whose primary design goal (or published evaluation) is *decision-making*: decision-tuned models, decision-focused reasoning tiers, benchmarks that test decisions (game-theoretic, multi-criteria, under uncertainty, bias/calibration), frameworks for LLM-driven decision support (multi-agent decision systems, debate-based pipelines, structured decision workflows), or key research papers. A PR must point at a primary source: the vendor's docs, the project's repo, the benchmark repo, or the arXiv abstract page.
2. **Add to the right section** of `README.md`:
   - Decision-making models → models fine-tuned/designed for decision tasks or reasoning about decisions
   - Benchmarks & evals → game-theoretic, multi-criteria, uncertainty, bias/calibration, rationality evals
   - Frameworks & tools → multi-agent decision systems, debate pipelines, structured decision workflows, decision-support tooling
   - Research papers → foundational papers (surveys, decision transformers, debate, LLM rationality)
   - Archived / superseded → retired models, dead benchmarks, superseded papers
3. **One entry = one bullet.** Format:
   `- [Name](https://official-site-or-repo) — ` one-line description + 2–4 key facts inline.
   Tag verification honestly: write `✅ verified 2026-09-29` only when you read the claim on the official page/repo/arXiv yourself; otherwise mark it `⚠️ unverified`.
4. **Add the matching record** to `data/decisions-llms.json` with these exact fields:

| field | type | values |
|---|---|---|
| `name` | string | model, benchmark, framework, or paper title |
| `vendor` | string | vendor / organization / authors |
| `url` | string | official https:// URL (docs, repo, or arXiv abstract) |
| `description` | string | one sentence |
| `decision_verified` | bool | `true` only if you verified the decision angle on an official source |
| `source_url` | string | the official source you verified against, or `""` |
| `verified_date` | string | `YYYY-MM-DD` of verification, or `""` |
| `status` | string | `active` / `maintenance` / `archived` / `commercial` / `paper` |
| `category` | string | `model` / `benchmark` / `framework` / `paper` |
| `features` | string[] | 3–6 key capabilities or facts |

5. **Status changes:** if an entry is retired, a repo is archived, or a paper is superseded, update its README entry *and* add a row (newest-first) to `docs/status-changes.md`.

## Style rules

- Link the **official site** (vendor docs, project repo, arXiv abstract page), never a blog post or aggregator.
- Facts that can change (scores, model versions, repo activity) get "as of" context in prose or are omitted — link the source instead of hard-coding numbers that rot.
- Benchmark scores stay labeled by who reported them ("vendor-reported" vs "independent").
- **Scores, specs, and dates are never guessed.** If you can't verify it on an official source, mark it `⚠️ unverified` or leave it out.
- Keep README descriptions to one entry per bullet; put depth in `docs/`.

## CI

Every PR runs:
- **Link check** (lychee) over all markdown files — no dead links.
- **JSON validation** — `data/decisions-llms.json` must parse, every record must have the required fields, and `status`/`category` must be from the allowed sets above. Verified entries require an https `source_url`.

Run locally before pushing:

```bash
python3 -c "import json; d=json.load(open('data/decisions-llms.json')); print(len(d),'ok')"
```
