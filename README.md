# Wenjie Luo · 罗文杰

**Agentic AI product & evaluation × transport engineering**
NUS MSc Civil Engineering (Transport), graduating Jan 2027 · Singapore

交通工程出身，做 Agent 产品和评测。一句话主张：**硬数字交给确定性工具，模型只做它擅长的部分，高风险动作必须有人点头——而判断模型放没放对位置，只能看闭环，不能看损失。**

[Site](https://luoaini1213.github.io) · [English](https://luoaini1213.github.io/en.html) · e1576499@u.nus.edu · wenjiluo7@gmail.com

*8 weeks, 200+ commits, 4 releases: everything below was built between July and September 2026.*

---

## Selected work

### [Civil Buddy](https://github.com/LUOaini1213/civil-buddy) — agentic AI workspace for engineering

`NL → agent routing → deterministic tools → HITL → evaluation`

66-role workflow system for civil / construction / tendering; the packing engine is one deterministic tool inside it.

- Coordinates, container counts and prices come from tools — the model never writes them
- Human approval gates every high-risk action (eligibility, bid, write-to-disk)
- **128** automated packing evaluations (16 lanes × 8 rounds; [re-run 2 Sep 2026, 128/128 PASS](https://github.com/LUOaini1213/civil-buddy/blob/main/docs/eval/fanout16x8-2026-09-02/rollup.md)); shadow evaluation of the deterministic path against LLM tool-calling runs in CI
- Policy engine and failure recovery: refuse with a reason → retry → degrade with an audit trail → cost circuit-breaker
- Golden-path E2E 8/8 (measured at R13, needs playwright, not in CI)

[Download a trial build (Releases)](https://github.com/LUOaini1213/civil-buddy/releases) · [one-page PRD with acceptance table](https://github.com/LUOaini1213/civil-buddy/blob/main/docs/civil-buddy/prd-pack-ship.md)

![Civil Buddy workbench](https://raw.githubusercontent.com/LUOaini1213/civil-buddy/main/docs/assets/workbench.png)

### [NAVSIM ability ladder](https://github.com/LUOaini1213/navsim-ability-ladder) — what caps open-loop planning

A 10-agent ablation on NAVSIM (563 scenes, one metric cache, paired bootstrap CIs on every rung), then three attempts to put a learned part back in.

- Kinematics first: ConstantVelocity 0.233 → 0.580; GT boxes do not close the gap, the map does (DAC 0.737 → 0.950)
- A learned model asked to draw the whole line scores 0.527 vs the hand rule's 0.730; let the rule draw the line and the model only pace it → 0.763
- Regularising and training longer both lowered open-loop L1 and **lowered** the closed-loop score
- Contamination handled by re-scoring every agent on 135 held-out scenes; effects that stop separating are reported as suggestive

### GPU & systems — two controlled experiments with honest outcomes

[**cuda-fused-layernorm**](https://github.com/LUOaini1213/cuda-fused-layernorm) — fused residual-add + LayerNorm hand-written in CUDA C++ (NVRTC), ported from Triton: warp-shuffle + shared-memory block reduction, float64-referenced accuracy gate, numerical-stability sweep. Same-card three-way comparison on a T4 over 12 shapes: Triton 1.341× over eager, my CUDA 1.087×, **CUDA vs Triton 0.812× — it loses on every shape** (best 0.997×), most likely because Triton autotunes `num_warps` and block size per shape while mine uses a fixed heuristic. Written up as a negative result, not hidden.

[**vllm-sm75-throughput**](https://github.com/LUOaini1213/vllm-sm75-throughput) — a 10× vLLM throughput collapse on a GTX 1650 (sm_75, no tensor cores) traced to a cuBLAS fp16 GEMM small-M cliff: bandwidth 99.5 → 4.3 GiB/s from M=1 to M=2. The refutation experiment on a T4 — same sm_75, same Turing, tensor cores kept — shows 106.7 → 88.1 (0.83×) across three shapes. One variable differs and the ratio moves 20×; the attribution holds.

### TikTok TechJam 2026 — four tracks, submitted 1 Sep, results pending

[Track 1 · Glass Box](https://github.com/LUOaini1213/track1) agent-observability middleware (span waterfalls, redaction, policy deny; official starter + my trace plane) · [Track 2 · RecAgent](https://github.com/LUOaini1213/recagent-techjam2026-track2) autonomous MLE loop, test 0.6015 vs FM 0.5946 with 0 manual edits · [Track 3 · GPU kernel](https://github.com/LUOaini1213/tiktok-techjam-2026-track3) 13/13 shapes PASS, median 2.07× · [Track 4 · ByteSize](https://github.com/LUOaini1213/track4) value-of-information stopping, +60 rank-1 at zero hit-rate loss, $0

### [EDA Copilot](https://github.com/LUOaini1213/eda-copilot) — flow Q&A over OpenROAD/ORFS that asks instead of guessing

Ran the full RTL→GDSII flow myself (ORFS official image, nangate45/gcd) and turned the 46 reports/logs plus 31 script docs into a 1,215-chunk corpus with line-level provenance. Seven structured stop codes (ambiguous metric, setup/hold unspecified, out of scope, …): **12/12** should-stop questions stop with the right code; with the guard off all 12 are answered anyway, each with a citation — a cited wrong answer is the dangerous kind. Hybrid retrieval was switched off, then back on when run artifacts made the corpus heterogeneous (Hit@5 0.957 vs 0.913); both numbers stay in the README. Reading my own QoR report: TNS −7.18 vs WNS −0.16 (violations spread over many paths), timing buffers at 18.7% of standard-cell area with WNS still unconverged. Example-scale design, open 45 nm library, default parameters — not fab yield data.

### [Counterask](https://github.com/LUOaini1213/counterask) — a storefront whose tools ask back · [live](https://luoaini1213.github.io/counterask/)

WebMCP Challenge entry: a one-page menswear store on 9,901 real products (Amazon Reviews 2023) whose `search_products` tool returns **a question** whenever answering would be a guess. No server, no model, zero tokens. Against a keyword matcher on 800 sentences: Hit@10 0.04 → **0.34 ± 0.01** (held-out phrasings 0.34), refusals wrongly inverted into requirements 597 → 0, budget broken in top-10 22 → 0. Letting the store ask its way down the category tree from "shoes"/"clothing": Hit@10 0.16 → 0.31, paired **+0.148 ± 0.048 on 8/8 shards**, candidate pool 597 → 121. Coverage is the ceiling and is reported as such (material recorded on 56% of products, fit on 8%).

### [CE5001 — flood-resilient bus network](https://luoaini1213.github.io/#proj-ce5001) — evaluation / research

200 paired experiments, rule agents vs LLM agents on flooded multimodal networks (DEM + SUMO; 793 services, 5,201 stops). Dense CBD: rule agents cut related travel time **62.2%**. [Report PDF](https://luoaini1213.github.io/files/CE5001_report.pdf)

### [CE5212 — LLM as approver](https://github.com/LUOaini1213/ce5212-llm-coordinator) · [CE5203 — AYE weaving](https://github.com/LUOaini1213/ce5203-aye-weaving) · [malaysia-auto-ask](https://github.com/LUOaini1213/malaysia-auto-ask)

Rules propose, the model only says yes/no — course log **43/44**, and a synchronous call cost Bus 95 +2.2 min · YOLOv11 counts + SUMO ramp metering, peak network time loss **−22.7%** · ask-data demo that stops when the metric is ambiguous — 30 questions: 22 correct, 8 correctly refused

---

## Stack

**AI / product:** agent workflows · LLM evaluation · HITL · tool calling · guardrails · PRD / acceptance
**Engineering:** Python · PyTorch · CUDA C++ (NVRTC) · Triton · vLLM · FastAPI · TypeScript · Rust · SUMO · OpenROAD/ORFS · WebMCP · SQL
**Domain:** transport engineering · construction workflows · tendering
