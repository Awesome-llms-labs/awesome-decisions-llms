# Decision-making evaluation

How to read the benchmarks in this repo — what each family actually tests, and what it doesn't.

## Benchmark families

**Game-theoretic / strategic.** Models play matrix games, auctions, and bargaining scenarios. Tests: does the model pick the Nash equilibrium when it should, exploit weak opponents, avoid being exploited? Scores are usually reported as payoff or win-rate against baselines. *Caveat:* many are zero-shot single-prompt games — real strategy needs repeated play and opponent modeling.

**Multi-criteria (MCDM).** Options trade off competing criteria; the benchmark checks whether the model weights criteria consistently and handles Pareto trade-offs. *Caveat:* "correct" answers often encode the benchmark authors' utility function — read it before trusting the ranking.

**Uncertainty & risk.** Probabilistic choices, information-gathering (pay for a signal?), hedging. Tests risk sensitivity and explore-vs-exploit behavior. *Caveat:* models' risk attitudes are prompt-fragile; small wording changes flip risk-seeking to risk-averse.

**Rationality / economic.** Expected-utility problems, transitivity of preferences, resistance to framing. *Caveat:* human subjects fail these too — "worse than humans" is a finding, "fails a normative axiom" is a design signal, not a verdict.

**Bias & calibration.** Anchoring, framing, loss aversion, overconfidence. These measure whether the model *inherits* human decision pathologies. *Caveat:* a model can be unbiased on the benchmark's framing and biased on yours; calibrate on your own decision distribution.

**Sequential / planning.** Multi-step tasks where early choices constrain later ones (agent benchmarks, planning tracks). This is decision-making under the hood. *Caveat:* conflates tool-use skill with decision quality — decompose the failure before blaming the decision.

## Reading scores honestly

- **Who reported it:** vendor-reported scores are marketing-adjacent; prefer independent replications. Both are labeled in this repo.
- **Prompt sensitivity:** a 20-point swing from rewording means the benchmark measures prompt fit, not decision ability.
- **Saturation:** when every flagship scores 90%+, the benchmark no longer discriminates — look for harder or newer variants.
- **Your distribution:** no benchmark is your workload. Sample 50–200 of your own decisions, score them, and check the model's calibration there before trusting any leaderboard.

## Minimum viable eval for a decision pipeline

1. Calibration plot on your own past decisions (predicted confidence vs observed outcomes).
2. A bias probe: reframe 20 decisions (gain vs loss framing) and check choice stability.
3. A debate-or-not A/B: single-agent vs multi-agent debate on 30 hard cases; keep debate only if the win rate justifies the token cost.
