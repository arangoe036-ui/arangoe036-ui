# Hi, I'm Esteban Arango 👋

Master's student in **Artificial Intelligence** at Northeastern University, building AI-powered and full-stack products.

I care most about **rigor in ML systems** — reproducible pipelines, verifiable data, and benchmarks that hold up under adversarial pressure. My flagship project, [**llm-training-data-foundry**](https://github.com/arangoe036-ui/llm-training-data-foundry), generates verified LLM training data that reproduces bit-for-bit from a single integer seed.

- 🎓 Pursuing an M.S. in Artificial Intelligence
- 🔭 Focused on machine learning, LLM evaluation, and shipping real products end-to-end
- 🛠️ **Stack:** Python · TypeScript · Next.js · React · Supabase · PostgreSQL · Docker · Machine Learning
- 📫 **Reach me:** arangomoreno.e@northeastern.edu

## 🚀 Featured Projects

### [llm-training-data-foundry](https://github.com/arangoe036-ui/llm-training-data-foundry) — verified LLM training data + a fault-localization benchmark
A reproducible foundry that generates `(source_code, semantic-IR, English-description)` triples from integer seeds — never scraped, never model-generated. Every pair clears four verification layers (pyflakes, radon complexity, mypy, sandboxed Docker execution against oracle outputs), and a SHA-256 hash chain makes any post-generation tampering detectable. A mutation layer injects single localized faults with deterministic ground-truth keys to build a benchmark that scores a model's fault-localization answers mechanically.

`Python` · `PostgreSQL` · `Docker` · `LLM evaluation` · 25K LOC · 614 passing tests · CI reproduction gate

### [grader-gameability-study](https://github.com/arangoe036-ui/grader-gameability-study) — a pre-registered experiment that killed its own idea
A decision experiment asking whether an "un-gameable" code grader could survive an adversary. I froze the thresholds and the reading of the outcome in a pre-registration *before* collecting data, then red-teamed my own grader black-box with an independent behavioral meta-oracle judging correctness. Result: an **80% escape rate** (95% bootstrap CI [65%, 92.5%]) — a static tamper blocklist is structurally routable. The pre-registered reading said stop, so the expensive downstream tiers were deliberately never built.

`Python` · `red-teaming` · `experiment design` · pre-registration · bootstrap CIs · sandboxed execution

*More projects on the way — I'm polishing several ML and full-stack builds for release.*

---

<sub>Always open to conversations about AI, data science, and building great products.</sub>
