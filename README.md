# Awesome Decisions LLMs [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> A curated directory of **LLMs and systems for decision-making**: decision-tuned models, benchmarks and evals that test decisions (game-theoretic, multi-criteria, under uncertainty, bias/calibration), frameworks and tools for LLM-driven decision support, and the key research papers — as of **September 2026**.

Chat benchmarks tell you how well a model *talks*. This list is about how well it *chooses*: strategic reasoning in games and negotiations, multi-criteria trade-offs, calibrated uncertainty, and the pipelines (debate, reflection, planning, prediction markets) that turn language models into decision systems.

**Verification confidence:** every entry below is stamped ✅ **verified 2026-09-29** (the decision-making angle was confirmed on the vendor's official page, the project repo, or the arXiv abstract). **Scores and specs are never guessed** — benchmark deltas are attributed to whoever reported them. Machine-readable records live in [`data/decisions-llms.json`](data/decisions-llms.json) with a `decision_verified` boolean per entry.

## Contents

- [Decision-making models](#decision-making-models)
- [Benchmarks & evals](#benchmarks--evals)
  - [Game-theoretic & strategic](#game-theoretic--strategic)
  - [Planning & sequential decisions](#planning--sequential-decisions)
  - [Bias, calibration & rationality](#bias-calibration--rationality)
  - [Bounded real-world decisions](#bounded-real-world-decisions)
- [Frameworks & tools](#frameworks--tools)
  - [Deliberation & search](#deliberation--search)
  - [Multi-agent decision systems](#multi-agent-decision-systems)
  - [Prediction markets & mechanism design](#prediction-markets--mechanism-design)
  - [Classical decision analysis + LLMs](#classical-decision-analysis--llms)
- [Research papers](#research-papers)
- [Guides](#guides)
- [Related repositories](#related-repositories)
- [Contributing](#contributing)
- [License](#license)

---

## Decision-making models

Models fine-tuned or designed for decision tasks — not general chat models with a reasoning mode bolted on.

- [Bosun v3.1](https://huggingface.co/blog/Hanno-Labs/decisionbench-bosun-v3-1) — ✅ Hanno Labs (Sept 2026): open-weight Qwen3-based decision models (0.6B & 1.7B) with 256 learned decision tokens — runtime answer choices are scored via masked softmax over decision-token slots (up to 255 candidates), returning full answer distributions over a typed API (`choice`/`score`/`noul`) with a Jev-compatible `/v1/systemone` server.
- [Sky-T1-32B-Preview](https://huggingface.co/NovaSky-AI/Sky-T1-32B-Preview) — ✅ NovaSky AI (UC Berkeley): open-weight 32B long-CoT reasoning model trained to replicate o1-style deliberate reasoning; SFT on 17K verified reasoning traces for under $450 (vendor-reported); card-reported Math500 82.4, AIME2024 43.3, GPQA-Diamond 56.8.
- [Prometheus 2](https://github.com/prometheus-eval/prometheus-eval) — ✅ Open-weight evaluator LLMs (7B & 8x7B) for the judging step of decision pipelines: direct Likert assessment and pairwise ranking; 0.6–0.7 Pearson with GPT-4-1106 and 72–85% human-judgment agreement (per repo README); Apache-2.0.
- [DeepSeek-R1](https://github.com/deepseek-ai/DeepSeek-R1) — ✅ DeepSeek: open 671B-MoE reasoning model trained with large-scale RL (GRPO); the deliberative substrate behind many decision benchmarks and distilled decision fine-tunes. Listed here once — full coverage in [awesome-flagship-llms](https://github.com/dakotac1994/awesome-flagship-llms).

---

## Benchmarks & evals

### Game-theoretic & strategic

- [GTBench](https://arxiv.org/abs/2402.12348) — ✅ NeurIPS 2024 (Duan et al.): 10 games in a language-driven OpenSpiel environment (tic-tac-toe, Connect-4, breakthrough, nim, blind auction, Kuhn poker, liar's dice, negotiation, pig, iterated prisoner's dilemma). Per authors: LLMs fail in complete/deterministic games but are competitive in probabilistic ones. [HF leaderboard](https://huggingface.co/spaces/GTBench/GTBench).
- [GameBench](https://arxiv.org/abs/2406.06613) — ✅ Costarelli et al. (2024): 9 game environments selected to resist pretraining contamination, each targeting a distinct strategy-game reasoning skill. Per authors: no tested model matched human performance; at worst GPT-4 performed below random action.
- [TMGBench](https://arxiv.org/abs/2410.10479) — ✅ 2×2 game benchmark in sequential, parallel, and nested formats. Per paper: o1-mini 66.6%/60.0%/70.0% vs gpt-4o 50.0%/35.0%/70.0%. Single-sourced (arXiv PDF only) — less established than GTBench.
- [EconArena](https://openreview.net/forum?id=NMPLBbjYFq) — ✅ NeurIPS 2024: dynamic benchmark using competitive economics games (beauty contests, second-price auctions) with well-defined Nash equilibria. Per authors: even when told opponents were rational, all 9 tested LLMs deviated from NE (Claude 2, GPT-4 deviated least). Pip-installable.
- [Bargaining Abilities of LLMs](https://arxiv.org/abs/2402.15813) — ✅ Xia et al. (2024): bargaining formalized as an asymmetric incomplete-information game on real Amazon price-history data. Playing buyer is much harder than seller; larger size didn't help buyers. OG-Narrator raised buyer deal rates 26.67%→88.88% (per authors).

### Planning & sequential decisions

- [BALROG](https://arxiv.org/abs/2411.13543) — ✅ ICLR 2025 (Paglieri et al.): long-horizon interactive decision-making for LLM/VLM agents across BabyAI, TextWorld, Crafter, Baba Is AI, MiniHack, NetHack (10¹–10⁵ steps). Per authors: LLMs can answer mechanics questions yet fail to apply them in practice.
- [PlanBench](https://arxiv.org/abs/2206.10498) — ✅ NeurIPS 2023 D&B (Valmeekam et al.): planning on International Planning Competition domains (Blocksworld etc.). Per authors LLM plan generation "falls quite short"; the repo leaderboard shows reasoning models (R1, o1) later hit ~99% on Blocksworld but collapse on Mystery Blocksworld variants.
- [MACHIAVELLI](https://arxiv.org/abs/2304.03279) — ✅ ICML 2023 Oral (Pan et al.): 134 choose-your-own-adventure games, 500K+ social decision scenarios measuring the tension between reward maximization and ethical behavior. LM-based steering achieved Pareto safety+capability improvements (per authors).

### Bias, calibration & rationality

- [STEER](https://arxiv.org/abs/2402.09552) — ✅ Raman et al. (2024): Systematic and Tuneable Evaluation of Economic Rationality — fine-grained "elements" (risk, time, social preference, strategic choice) with a report card across 14 LLMs, analyzing model-size effects.
- [LLM economicus?](https://arxiv.org/abs/2408.02784) — ✅ COLM 2024 (Ross, Kim, Lo): utility-theory quantification of economic biases (loss aversion, anchoring, framing) vs perfect-rationality and human benchmarks. Current LLMs are neither fully human-like nor fully economicus-like.
- [The Bias is in the Details](https://arxiv.org/abs/2509.22856) — ✅ Knipper et al. (Sept 2025): 8 cognitive biases across 45 LLMs, 220 hand-curated decision scenarios, 2.8M+ responses. Bias-consistent behavior in 17.8–57.3% of instances; models >32B reduced bias in ~39.5% of cases (per authors).
- [LCB-Bench](https://github.com/UltraDeep-Tech/lcb-bench) — ✅ Ultra Deep Tech (2026): community benchmark — 1,500 paired baseline-vs-biased cases, 30 cognitive biases, 7 categories, standardized 0–100 LCB Score. Self-reported leaderboard (GPT-4o 83.8, Claude Sonnet 4.6 69.0) is author-claimed, not independent; tiny project (1 star) — treat accordingly.
- [SycophancyEval](https://arxiv.org/abs/2310.13548) — ✅ Sharma et al. (2023): do assistants agree with the user's beliefs over the evidence? Five SOTA assistants exhibited sycophancy; optimizing against preference models sometimes sacrificed truthfulness (per authors).
- [Economic rationality of GPT](https://www.pnas.org/doi/full/10.1073/pnas.2316205120) — ✅ PNAS 2024: revealed-preference (GARP) measurement across 10,000 budgetary tasks. GPT-3.5-Turbo outscored 347 human subjects on rationality (per authors); robust to temperature/demographics, sensitive to price framing.
- [NegotiationArena](https://github.com/vinid/NegotiationArena) — ✅ Bianchi et al. (2024): platform for probing LLM negotiation (buy-sell, ultimatum, resource-exchange games). All tested models showed anchoring/framing biases; one LLM improved its payoff ~20% by feigning desperation (per secondary survey). Repo mid-refactor — use the `paper_experiment_code` branch.
- [LLM-Deliberation](https://github.com/S-Abdelnabi/LLM-Deliberation) — ✅ NeurIPS 2024 (Abdelnabi et al.): scorable multi-agent, multi-issue negotiation testbed measuring cooperation, competition, and maliciousness. GPT-3.5 and small models mostly fail; GPT-4/SoTA still underperform in adversarial games (per authors). MIT.

### Bounded real-world decisions

- [DecisionBench](https://github.com/atlanai/decision-bench) — ✅ Atlan AI (2026): how accurately, quickly, and cheaply models make bounded decisions on real data. Corpus bench-v4: 1,071 rows, 35 tasks, 11 use cases from 36 public datasets; reports accuracy with 95% CIs, calibration, latency, tokens, cost. 12-model results (2026-09-23) at [decisionbench.ai](https://decisionbench.ai). MIT.
- [DecisionBench (Hanno Labs)](https://huggingface.co/blog/Hanno-Labs/decisionbench-bosun-v3-1) — ✅ Hanno Labs (Sept 2026): MTEB-inspired open decision-model benchmark — frozen tasks with row-level evidence and a community result record. DecisionBench 1.0: 43 tasks, 23,900 English rows, 28 domains; 22,700-row applied suite + 1,200-row reasoning track; primary score all-row accuracy with coverage, ECE, NLL. Distinct from Atlan AI's DecisionBench above — see [status changes](docs/status-changes.md).

---

## Frameworks & tools

### Deliberation & search

- [Tree of Thoughts](https://github.com/princeton-nlp/tree-of-thought-llm) — ✅ Yao et al., NeurIPS 2023 (Princeton/Google DeepMind): generalize CoT to deliberate decision-making — explore multiple reasoning paths, self-evaluate choices, lookahead/backtrack via BFS/DFS. Game of 24: 74% vs 4% for GPT-4 with CoT (per abstract).
- [Graph of Thoughts](https://github.com/spcl/graph-of-thoughts) — ✅ Besta et al., AAAI 2024 (ETH Zurich): thoughts as an arbitrary graph with generate/aggregate/refine ops. Sorting quality +62% over ToT at −31% cost (per abstract); CoT/ToT are special cases.
- [Reflexion](https://github.com/noahshinn/reflexion) — ✅ Shinn et al., NeurIPS 2023: verbal reinforcement learning — agents reflect on feedback, store it in episodic memory, improve across trials with no weight updates. 91% pass@1 on HumanEval at the time (per abstract); evaluated on AlfWorld sequential decision-making.
- [ReAct](https://arxiv.org/abs/2210.03629) — ✅ Yao et al., ICLR 2023: interleave Thought/Action/Observation so reasoning grounds decisions in tool feedback — the decision loop under modern agents. ALFWorld 71% vs 22% imitation-learning baseline (secondary source).
- [DSPy](https://github.com/stanfordnlp/dspy) — ✅ Stanford NLP: program (don't prompt) LMs — declarative signatures plus algorithmic optimizers (MIPRO) compile high-quality multi-step decision pipelines. MIT; ~38.4K stars; docs at [dspy.ai](https://dspy.ai).

### Multi-agent decision systems

- [ReConcile](https://github.com/dinobby/ReConcile) — ✅ Chen, Saha, Bansal, ACL 2024: round-table consensus among diverse LLMs with confidence-weighted voting. Beats prior single- and multi-agent baselines by up to 11.4%; outperforms GPT-4 on three datasets (per abstract).
- [Mixture-of-Agents](https://github.com/togethercomputer/moa) — ✅ Wang et al., ICLR 2025 (Together AI): proposer layers generate diverse candidates, an aggregator synthesizes one decision. 65.1% on AlpacaEval 2.0 with open models only, beating GPT-4 Omni's 57.5% (per repo README); no fine-tuning. Apache-2.0.
- [ChatEval](https://github.com/chanchimin/ChatEval) — ✅ Chan et al. (THUNLP): multi-agent referee team — diverse role-prompted LLMs debate and judge responses. Included for the debate-judge pattern; evaluation-focused, not decision-support per se. Apache-2.0.
- [TradingAgents](https://github.com/TauricResearch/TradingAgents) — ✅ Tauric Research: multi-agent LLM financial decision framework — analyst team → bull/bear researcher debate → trader → risk-manager → portfolio-manager final decision. v0.5.2 (Sept 2026), LangGraph orchestration. Research-only, no live order execution — not financial advice. Apache-2.0.

### Prediction markets & mechanism design

- [ForecastArena](https://github.com/incredibledays/forecast-arena) — ✅ Retrieval-augmented multi-agent prediction-market simulator: binary/categorical/scalar markets priced by Hanson's LMSR, with LLM belief updates, evidence retrieval, and leaderboard scoring.
- [DMsim](https://github.com/nunobrazz/dmsim) — ✅ Mechanism-design research tool: simulates agent organizations with private beliefs, comparing a Decision Market against a VCG-inspired auction. LLM-generated agent profiles; FastAPI backend + Jekyll UI.
- [prediction-market-lmsr](https://github.com/curious7-web/prediction-market-lmsr) — ✅ LMSR simulation engine with truthful/noisy/LLM-based/robust/adversarial agents for stress-testing decisions under uncertainty; reports mean wealth, worst outcomes, CVaR tail risk.

### Classical decision analysis + LLMs

- [pyDecision](https://github.com/Valdecy/pyDecision) — ✅ Valdecy Pereira et al. (Federal Fluminense University): 70+ Multi-Criteria Decision Analysis methods (AHP, TOPSIS, ELECTRE, PROMETHEE, VIKOR, fuzzy variants) with LLM integration for interpreting and comparing method outcomes. Active through 2026-06; companion paper arXiv 2404.06370 (via secondary source).

---

## Research papers

- [OPRO — Large Language Models as Optimizers](https://arxiv.org/abs/2309.03409) — ✅ Yang et al. (Google DeepMind), ICLR 2024: meta-prompt carries a score-sorted trajectory of past solutions; the model proposes better ones. Beat human-designed prompts by up to 8% on GSM8K, 50% on Big-Bench Hard (per authors).
- [Decision Transformer](https://arxiv.org/abs/2106.01345) — ✅ Chen et al., NeurIPS 2021: RL as conditional sequence modeling — causally-masked Transformer conditioned on desired return outputs actions directly. Pre-LLM, but the template for all RL-as-sequence-modeling decision work.
- [Multiagent Debate](https://arxiv.org/abs/2305.14325) — ✅ Du et al., ICML 2024: N instances answer independently, then revise over rounds toward consensus ("society of minds"). Improves mathematical/strategic reasoning and factuality; reduces but doesn't eliminate hallucinations. ~9 calls per question.
- [Deliberative Alignment](https://arxiv.org/abs/2412.16339) — ✅ Guan et al. (OpenAI), Dec 2024: teach the model the safety spec text directly; train it to reason over specs in CoT before answering. Used to align the o-series; pushed the Pareto frontier on jailbreak robustness + over-refusal + OOD generalization (per authors).
- [Teaching Models to Express Their Uncertainty in Words](https://arxiv.org/abs/2205.14334) — ✅ Lin, Hilton, Evans, TMLR 2022: GPT-3 finetuned to emit verbalized confidence — well-calibrated without logits. Introduced the CalibratedMath suite; generalized under distribution shift.
- [Navigating the Grey Area](https://arxiv.org/abs/2302.13439) — ✅ Zhou, Jurafsky, Hashimoto (2023): epistemic markers ("I'm sure", "I think") in prompts shift accuracy >80%; high-certainty expressions *reduced* accuracy 7% vs low-certainty ones (per authors).
- [Judging LLM-as-a-Judge](https://arxiv.org/abs/2306.05685) — ✅ Zheng et al., NeurIPS 2023 D&B: GPT-4 judge matches human preferences at ~80% agreement. Introduced MT-Bench and Chatbot Arena; documents position, verbosity, and self-enhancement biases in judges.
- [Decision-Focused Learning survey](https://arxiv.org/abs/2307.13565) — ✅ Train predictors to minimize downstream *decision regret*, not standalone prediction error, by differentiating through the optimizer. Foundational method: Wilder et al., "Melding the Data-Decisions Pipeline" (AAAI 2019) — arXiv ID not verified here.
- [One for All (MCDM)](https://arxiv.org/abs/2502.15778) — ✅ LLMs on multi-criteria decision-making vs human-expert ground truth: ~60% accuracy for open models + Claude/ChatGPT, ~70% with CoT/few-shot, ~95% with LoRA finetuning (per authors).
- [LLMs for Sequential Decision-Making](https://arxiv.org/abs/2605.09009) — ✅ Finetune pretrained LLMs on oracle-labeled trajectories for few-shot decisions in MDPs/POMDPs; finetuned attention implicitly estimates optimal Q-functions; largest gains in long-horizon, partially-observed settings.
- [Game-theoretic LLM workflows](https://huggingface.co/papers/2411.05990) — ✅ Wenyueh et al. (2024): game-theoretic workflows guiding LLM reasoning in strategic decisions and negotiations; markedly improve optimal-strategy identification; also tests whether adopting the workflow is itself a rational meta-strategy.
- [LanguageMPC](https://arxiv.org/abs/2310.03026) — ✅ Sha et al. (Tsinghua, 2023): LLM as the decision-making "brain" for autonomous driving, with language as the decision interface — interpretability suited to regulatory scrutiny.
- [Agentic LLMs survey](https://arxiv.org/abs/2503.23037) — ✅ Plaat et al. (2025): organizes agentic-LLM literature into reasoning, acting, interacting; the reasoning strand explicitly "aims to improve decision making".

---

## Guides

- [Choosing a decision model](docs/choosing-a-decision-model.md) — calibration-first selection by decision type (irreversible, multi-criteria, strategic, repeated, sequential).
- [Decision-making evaluation](docs/decision-making-evaluation.md) — what each benchmark family tests, how to read scores honestly, and a minimum viable eval for a decision pipeline.
- [Glossary](docs/glossary.md) — rationality, MCDM, calibration, deliberative reasoning, OPRO, sycophancy, and more.
- [Status changes](docs/status-changes.md) — retirements, naming collisions, and material claim changes, newest first.
- [Machine-readable catalog](data/decisions-llms.json) — all 48 entries with decision-verification status, source, and date.

## Related repositories

- [awesome-flagship-llms](https://github.com/dakotac1994/awesome-flagship-llms) — sibling list: the single most capable model from every major lab. Decision angle: deliberative reasoning tiers.
- [awesome-flash-llms](https://github.com/dakotac1994/awesome-flash-llms) — sibling list: cost-performance Flash-class LLMs and pricing — price a *decision*, not a token.
- [awesome-fast-llms](https://github.com/dakotac1994/awesome-fast-llms) — sibling list: inference-speed LLMs — latency budgets for decision pipelines.
- [awesome-free-llms](https://github.com/dakotac1994/awesome-free-llms) — sibling list: free LLM tiers and models for zero-cost decision experiments.
- [awesome-ai-sandboxes](https://github.com/dakotac1994/awesome-ai-sandboxes) — sibling list: sandboxes for safely executing agent decision loops.
- [awesome-ai-agents](https://github.com/dakotac1994/awesome-ai-agents) — sibling list: AI agent frameworks and ecosystems.
- [awesome-jev](https://github.com/dakotac1994/awesome-jev) — sibling list: TypeSafe's Jev / System One — typed decisions with calibrated confidence.

## Contributing

Entries and corrections are welcome — see [CONTRIBUTING.md](CONTRIBUTING.md). Every PR is checked by CI: lychee link check over all markdown files, and validation of `data/decisions-llms.json` (required fields, allowed `status`/`category` sets, and the `decision_verified` boolean with an https `source_url` for verified entries).

## License

[MIT](LICENSE) © 2026 dakotac1994
