# Esteban Arango

**M.S. Artificial Intelligence — Northeastern University**

Master's student in Artificial Intelligence, building toward ML engineering.

Right now that means inference and evaluation — speculative decoding, quantization, and the
occasional reinforcement learning detour — all of it built and measured on a single consumer GPU.

The part I like most is finding out whether an idea actually holds up. So these repos tend to
carry the controls and the arms that didn't work alongside the ones that did.

**Looking for a Spring 2027 co-op in ML / AI engineering.**

- 🔭 Inference optimization · quantization · LLM evaluation · multi-agent RL · retrieval
- 🛠️ Python · PyTorch · CUDA · Docker · PostgreSQL · FastAPI · ChromaDB · TypeScript · Next.js
- 📫 arangomoreno.e@northeastern.edu

---

## Featured

### [speculative-coder](https://github.com/arangoe036-ui/speculative-coder) — 2.40× faster local inference, provably lossless

**13.6 → 32.7 tok/s on a 7B code model, single RTX 5080, emitting exactly the tokens the target
model would have sampled.** No `vllm`, no `assistant_model=` — the rejection sampler, generation
loop, KV-cache rollback and twelve speculation strategies are written from scratch in PyTorch.

The winning design drafts one branch and splits it only where the drafter is unsure: certainty
costs one batch row, uncertainty costs two. It hits the highest measured throughput on **3.1×
less draft compute** than fixed-width parallel drafting.

Losslessness is verified, not asserted — a 10,000-run Monte Carlo goodness-of-fit on the sampler,
an independent full-recompute oracle every engine must match token-for-token, and a precision
sweep reported as measured. The classic implementation bug in this algorithm is caught at **20σ**,
so the test is proven able to fail. Twelve architectures built, eight falsified, each with the
mechanism that ruled it out.

`PyTorch` · `CUDA` · speculative decoding · 12.7K LOC · 451 tests

### [mixed-precision-search](https://github.com/arangoe036-ui/mixed-precision-search) — an LLM agent lost to a greedy loop by 4,386×

**Deterministic search over per-layer bit-widths to fit a model into a fixed VRAM budget**, with an
exact integer ledger for memory so the constraint is checkable rather than estimated. PPL **6.38**
at a 3.5-bit envelope.

The finding worth having in 2026 is the negative one, and it is measured rather than argued: an
LLM agent proposing bit allocations **never beat uniform assignment**, violated a constraint
reducible to summing 24 integers on **14 of 14 and 9 of 14** attempts across runs, found zero
feasible allocations in 2 of 4 runs, and correlated **−0.205** and **+0.000** with measured
layer sensitivity. It lost to plain greedy ascent by 4,386× at the same memory envelope, so I
deleted it. A second arm found 2:4 structured sparsity losing to dense by **3,307× at equal
memory** — against an iso-VRAM control I had to build myself, because the two configurations I
was handed were not memory-matched.

`PyTorch` · quantization · sparsity · constrained search · 2.5K LOC

### [apex-matrix](https://github.com/arangoe036-ui/apex-matrix) — 96 agents learning simultaneously at ~770 decision-steps/sec

**A predator–prey testbed where both species learn at once** — MAPPO with a centralized critic over
a 224-wide global state, structure-of-arrays physics, and throughput that *rises* as the population
grows. Population is a state variable: animals mate, gestate and are born mid-episode.

Learning is real and proven against a control verified inert — predators go **7.441 → 13.921 mean
return on 3 of 3 seeds** against frozen prey, while a learning-rate-zero control goes 7.441 → 7.005
on 0 of 3, with policy entropy bit-identical across all 240 recorded rows. Ten mechanisms designed
to produce pack hunting were then each measured against **its own** chance floor. All ten failed.

`PyTorch` · `PettingZoo` · multi-agent RL · 48K LOC · 467 tests

### [industrial-ai-copilot](https://github.com/arangoe036-ui/industrial-ai-copilot) — RAG that cites the cell and the formula, not just the document

**A local multi-agent copilot over a real industrial document set** — an ISO 9001 quality manual,
a cable-run quoter with 47 live spreadsheet formulas, and an installation SOP — answering
operational questions while citing the exact page, cell and formula behind every number.

The Excel formula chain survives **byte-for-byte** into vector metadata, and the engine resolves
the full chain through surcharges, freight and tax to the final total. A three-stage degradation
cascade falls from a 14B model to an 8B one to a **citation-only extractive mode** that still
answers auditably with no LLM at all, and `/api/health` warns when a substitute model is loaded
rather than pretending it is the intended one.

`FastAPI` · `Streamlit` · `ChromaDB` · `Ollama` · recursive-descent formula parser · 22 tests

---

## Also

**[mario-imitation-learning](https://github.com/arangoe036-ui/mario-imitation-learning)** — can
behavioural cloning alone clear Mario 1-1 from a perfect TAS speedrun? Where it demonstrably works
is the Koopas: **+5.5 pp** over a script matched on the policy's own action statistics, 10/10
paired seeds, **p = 0.0020**, surviving Bonferroni across a four-region family. The mechanism was
named before the result was known.

**[llm-training-data-foundry](https://github.com/arangoe036-ui/llm-training-data-foundry)** —
`(source, semantic-IR, description)` triples reproducible to the bit from a single integer seed,
never scraped and never model-generated. Four verification layers including sandboxed Docker
execution against oracle-computed outputs, a SHA-256 hash chain binding all three fields, and a CI
reproduction gate. `PostgreSQL` · `Docker` · 276 test functions / 615 cases.

**[flbench](https://github.com/arangoe036-ui/flbench)** — repair difficulty is a property of the
fault class, not the model: family ordering is identical across three models from two labs, every
pairwise Spearman **rho = +1.000**, surviving a program-length control. Also retracts its own
original headline in full, because that headline turned out to be a defect in my scorer.

**[grader-gameability-study](https://github.com/arangoe036-ui/grader-gameability-study)** — a
pre-registered black-box red team that broke my own code grader in **80%** of attempts (95% CI
[65%, 92.5%]), with an independent behavioural meta-oracle so the harness could only make the
grader look worse, never falsely better.

---

<sub>Also building an ML-augmented statistical arbitrage engine — PCA/DBSCAN cointegration
screening with FDR control and a walk-forward backtester. Open to conversations about inference,
evaluation, and building things that hold up under scrutiny.</sub>
