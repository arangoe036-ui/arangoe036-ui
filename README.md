# Esteban Arango

M.S. Artificial Intelligence — Northeastern University

**I build the control that could kill my result, and I report it.**

Most ML write-ups report the number that worked. I'm more interested in the comparison that
decides whether the number means anything — the null that never looks at the data, the adversary
attacking my own grader, the baseline matched on my own model's statistics. Two of the three
projects below lead with a result I didn't want.

- 🎓 M.S. in Artificial Intelligence, Northeastern University
- 🔭 Imitation learning · LLM evaluation · geospatial ML · reproducible pipelines
- 🛠️ Python · PyTorch · Docker · PostgreSQL · TypeScript · Next.js
- 📫 arangomoreno.e@northeastern.edu

---

## Projects

### [speculative-coder](https://github.com/arangoe036-ui/speculative-coder) — 2.40× faster local LLM inference, distribution provably unchanged
A from-scratch PyTorch speculative decoding engine — no `vllm`, no `assistant_model=` — and an
empirical study of the thirteen architectures built around it. **2.40× on a 7B code model** (13.6 →
32.7 tok/s, single RTX 5080) with the emitted tokens **provably identical** to what the target model
would have sampled. The winning design splits a draft branch only where the drafter is unsure —
certainty costs one batch row, uncertainty costs two. **Seven of the thirteen architectures were
falsified**, each with the measured mechanism that killed it.

Losslessness is verified, not asserted: a 10,000-run Monte Carlo goodness-of-fit on the rejection
sampler, an *independent* full-recompute greedy oracle every engine must match token-for-token, and a
precision sweep reported honestly (fp32 5/5 bitwise identical, bf16 4/5, int8 2/5). The naive
implementation bug — resampling from `p` instead of the residual — is **caught at 20σ**, so the test
is proven able to fail.

`Python` · `PyTorch` · `CUDA` · speculative decoding · 10.5K LOC · 451 tests

### [apex-matrix](https://github.com/arangoe036-ui/apex-matrix) — ten mechanisms built to produce pack hunting, all ten falsified
A multi-agent RL testbed for predator–prey coevolution: 96 agents, MAPPO with a centralized critic,
raycast vision, energy budgets and reproduction. Learning is real and proven against a control
verified **inert** — policy entropy bit-identical across all 240 recorded rows. Then ten separate
mechanisms designed to produce cooperative hunting were each measured against **its own** chance
floor, and **all ten failed**. The only effect that moved unanimously — more episode time — made
coordination *worse*.

`Python` · `PyTorch` · `PettingZoo` · multi-agent RL · 47K LOC · 449 tests

### [mario-imitation-learning](https://github.com/arangoe036-ui/mario-imitation-learning) — can supervised learning alone clear Mario 1-1?

A verified TAS→training-data pipeline, a behavioural-cloning policy, and — the actual contribution —
the controls that decide whether any of it worked.

The policy reaches the flagpole on **2.0% of episodes [0.8%, 5.0%]**. A fixed-rate script that never
looks at the screen does it on **0.5% [0.09%, 2.8%]**, Fisher **p = 0.372**. So the completion is real,
and it is not evidence of learned skill — the control that empties it of meaning is the point.

Where learning genuinely wins is the Koopas: **+5.5 pp** over a script matched on the policy's own
action statistics, **10/10 paired seeds, p = 0.0020**, surviving Bonferroni correction across a
four-region family. The mechanism was specified before the result — the Koopas move, and a blind
fixed distribution cannot track a moving obstacle.

`PyTorch` · behavioural cloning · NES emulation · 324 tests (306 pass, 18 need a ROM you supply) · Apache-2.0

### [llm-training-data-foundry](https://github.com/arangoe036-ui/llm-training-data-foundry) — verified LLM training data, reproducible to the bit

Generates `(source_code, semantic-IR, English-description)` triples from a single integer seed —
never scraped, never model-generated. Every pair clears four verification layers (pyflakes, radon
complexity, mypy, and sandboxed Docker execution against oracle-computed outputs), and a SHA-256
hash chain binds source, IR, and description so any consumer can independently detect post-generation
tampering.

A mutation layer injects single localized faults with deterministic ground-truth keys, turning the
dataset into a fault-localization benchmark that scores a model's WHERE / WHAT / HOW-TO-FIX answers
mechanically — no human annotation, no model in the loop.

`Python` · `PostgreSQL` · `Docker` · 274 tests across 28 files · CI reproduction gate

### [grader-gameability-study](https://github.com/arangoe036-ui/grader-gameability-study) — a pre-registered experiment built to kill its own idea

**The negative result is the deliverable.** I froze the thresholds and the reading of the outcome in
a pre-registration *before* collecting any data, then red-teamed my own code grader black-box, with an
independent behavioural meta-oracle deciding correctness so the harness could only make the grader look
worse, never falsely better.

Result: an **80% escape rate** (95% bootstrap CI [65%, 92.5%]) — a static tamper blocklist is
structurally routable. The pre-registered stop rule said stop, so the expensive downstream tiers were
deliberately never built. The `NotImplementedError`s under `experiments/` are that rule working as
designed, not abandoned work.

`Python` · red-teaming · pre-registration · bootstrap CIs · sandboxed execution

---

<sub>Open to conversations about AI, evaluation, and building things that hold up under scrutiny.</sub>
