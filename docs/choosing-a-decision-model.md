# Choosing a decision model

How to pick an LLM for decision work — not chat, not code: *choosing*.

## What "good at decisions" actually means

A decision is a commitment under uncertainty. Score candidates on four axes, in this order:

1. **Calibration over raw accuracy.** A model that says "70% confident" and is right 70% of the time beats a smarter-sounding model that's confidently wrong. Check [decision-making evaluation](decision-making-evaluation.md) for the calibration benchmarks.
2. **Rationality, not eloquence.** Evals that test expected-utility reasoning, transitivity, and strategy-proofness (auctions, bargaining, matrix games) are more predictive than chat benchmarks.
3. **Deliberation budget.** Hard decisions benefit from long chain-of-thought ("thinking") modes — o-series, Deep Think, R1-style reasoning. Budget thinking tokens like compute: more for irreversible calls, less for reversible ones.
4. **Verifiability.** Prefer pipelines where the model's recommendation is checkable: tool outputs, retrieved evidence, or a second model as judge — with the judge's own calibration checked.

## Pick by decision type

| Decision type | Prefer | Why |
|---|---|---|
| High-stakes, irreversible (hiring, pricing, medical) | Deliberative reasoning models + human-in-the-loop + calibrated confidence | Latency is cheap next to a wrong call; never fully automate |
| Multi-criteria trade-offs (vendor selection, architecture) | Models with strong MCDA eval results; structured workflows that force criteria weighting | Unstructured chat collapses criteria into vibes |
| Strategic / game-theoretic (negotiation, auctions) | Models scoring well on game-theoretic benchmarks | The right move depends on the opponent's move |
| Repeated low-stakes (routing, triage, ranking) | Fast calibrated models + logged outcomes | Optimize $/decision; measure calibration in production |
| Sequential / planning (agents, ops) | ReAct/Reflexion-style pipelines; debate for hard calls | Single-shot answers compound errors |

## Anti-patterns

- **Asking one chat turn for a decision.** No criteria, no alternatives, no uncertainty — that's a guess with formatting.
- **Trusting confidence scores out of the box.** Most models are miscalibrated; verify on the decision-evaluation benchmarks first.
- **Debate for everything.** Multi-agent debate improves hard reasoning (Du et al.) but multiplies cost 3–5×; reserve it for decisions worth the tokens.
- **Sycophantic judges.** If the "judge" model just agrees with the proposer, your pipeline is theater. Test the judge independently.

## Cost thinking

Price a *decision*, not a token: deliberative models cost 5–50× more per call than fast tiers (see [awesome-flash-llms](https://github.com/dakotac1994/awesome-flash-llms) for per-token pricing), but a $0.50 deliberated decision beats a $0.01 confident blunder. Spend the budget where reversibility is lowest.
