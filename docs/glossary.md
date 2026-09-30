# Glossary

Terms used in this repo.

- **Decision-making (LLM):** choosing an action or recommendation from alternatives under goals, constraints, and uncertainty — not just generating plausible text. Includes tool selection, planning, negotiation, and multi-criteria trade-offs.
- **Decision-verified (✅):** the entry's decision-making angle was confirmed on an official source (vendor docs, project repo, arXiv abstract) on the stamped date. **Unverified (⚠️)** means the claim comes from third-party sources — never guessed.
- **Rationality:** behavior consistent with expected-utility maximization — stable preferences, transitive rankings, calibrated uncertainty. Tested by game-theoretic and economic evals.
- **Game-theoretic benchmark:** evaluates models in strategic settings (auctions, bargaining, matrix games) where the right move depends on what other agents do.
- **MCDM / MCDA:** multi-criteria decision-making / analysis — choosing between options that trade off competing criteria (cost vs quality vs risk). A classic decision-support discipline now being tested with LLMs.
- **Decision under uncertainty:** choices where outcomes are probabilistic or unknown; tests risk sensitivity, hedging, and information gathering (explore vs exploit).
- **Calibration:** whether a model's stated confidence matches its actual accuracy. Critical for decisions: an overconfident model makes expensive mistakes confidently.
- **Cognitive bias evals:** tests for anchoring, framing effects, loss aversion, and other human biases in model choices — whether the model inherits our worst decision habits.
- **Multi-agent debate:** several model instances argue for competing options, then a judge decides. Du et al. (2023) showed debate improves factuality and reasoning over single-agent answers.
- **Deliberative reasoning:** long chain-of-thought / "thinking" modes (o-series, Deep Think, R1-style) that trade latency and tokens for better decisions on hard problems.
- **Decision Transformer:** Chen et al. (2021) — reframes reinforcement learning as sequence modeling: condition on desired return, predict actions. The conceptual ancestor of LLMs-as-decision-makers, from before the LLM era.
- **OPRO:** "Large Language Models as Optimizers" — using an LLM to iteratively propose solutions and learn from scores, a decision-loop primitive.
- **Reflexion / ReAct:** agent patterns where the model reflects on failures (Reflexion) or interleaves reasoning with tool actions (ReAct) — the building blocks of decision pipelines.
- **LLM-as-judge:** using a model to score or rank options — a decision step that needs its own calibration checks.
- **Sycophancy:** the model agreeing with the user's stated preference rather than the best answer — a failure mode for decision support.
- **Explore vs exploit:** the fundamental sequential-decision trade-off: gather information (explore) or act on what you know (exploit). Bandits, Bayesian optimization, and agent planners all wrestle with it.
