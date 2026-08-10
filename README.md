# Hi, I'm Esteban Arango 👋

Master's student in **Artificial Intelligence** at Northeastern University.

I build the control that could kill my own result, run it, and report what it says — including
when it says the result isn't there. Across the projects below that has meant a red-team that
broke my own grader, a baseline with no neural network that matched my policy, and a headline
I withdrew after re-measuring it at the right unit of analysis.

- 🎓 M.S. in Artificial Intelligence
- 🔭 Machine learning, LLM evaluation, and measurement you can actually defend
- 🛠️ **Stack:** Python · PyTorch · TypeScript · Next.js · PostgreSQL · Docker
- 📫 **Reach me:** arangomoreno.e@northeastern.edu

## 🚀 Featured Projects

### [mario-imitation-learning](https://github.com/arangoe036-ui/mario-imitation-learning) — can imitation alone clear Mario 1-1?
Supervised learning from a flawless tool-assisted speedrun — no policy gradient, no value
bootstrapping. The policy does reach the flagpole, on **4 of 200** episodes. A script that never
looks at the screen does it on **1 of 200** (Fisher p = 0.372), so that clip proves nothing, and
the README says so. What survives is narrower and real: at the **Koopas** — the one obstacle that
*moves* — the policy beats a representation-matched blind baseline by **+5.5 pp, 10/10 paired
seeds, p = 0.0020**, surviving Bonferroni correction. The negative has a mechanism: the corpus is
**1,223,797 frames containing zero deaths and zero recoveries**, so the policy never sees a single
example of getting out of trouble, and live play peaks at **0.82 epochs** while the loss keeps
falling.

`Python` · `PyTorch` · imitation learning · 324 tests · 8 intervention families closed by measurement

### [llm-training-data-foundry](https://github.com/arangoe036-ui/llm-training-data-foundry) — verified LLM training data + a fault-localization benchmark
A reproducible foundry generating `(source_code, semantic-IR, English-description)` triples from
integer seeds — never scraped, never model-generated. Every pair clears four verification layers
(pyflakes, radon, mypy, sandboxed Docker execution against oracle outputs), and a SHA-256 hash
chain makes post-generation tampering detectable. A mutation layer injects single localized faults
with deterministic ground-truth keys to build a benchmark that scores a model's answers
mechanically.

`Python` · `PostgreSQL` · `Docker` · LLM evaluation · 25K LOC · 614 passing tests · CI reproduction gate

### [grader-gameability-study](https://github.com/arangoe036-ui/grader-gameability-study) — a pre-registered experiment that killed its own idea
Could an "un-gameable" code grader survive an adversary? I froze the thresholds and the reading of
the outcome *before* collecting data, then red-teamed my own grader black-box with an independent
behavioural meta-oracle judging correctness. Result: an **80% escape rate** (95% bootstrap CI
[65%, 92.5%]) — a static tamper blocklist is structurally routable. The pre-registered reading said
stop, so the expensive downstream tiers were deliberately never built.

`Python` · red-teaming · pre-registration · bootstrap CIs · sandboxed execution

---

<sub>Always open to conversations about AI, evaluation, and building things that hold up under scrutiny.</sub>
