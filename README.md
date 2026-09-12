# Wenjie Luo · 罗文杰

**Agentic AI product & evaluation × transport engineering**
NUS MSc Civil Engineering (Transport), graduating Jan 2027 · Singapore

交通工程出身，做 Agent 产品和评测。一句话主张：**硬数字交给确定性工具，模型只做它擅长的部分，高风险动作必须有人点头——而判断模型放没放对位置，只能看闭环，不能看损失。**

[Site](https://luoaini1213.github.io) · [English](https://luoaini1213.github.io/en.html) · [Six-role CV library / 六赛道简历](https://luoaini1213.github.io/resumes/) · e1576499@u.nus.edu · wenjiluo7@gmail.com

[Run the projects / 运行命令与依赖](RUNNABLE_PROJECTS.md) — local demos, reproducible reports and full-experiment requirements.

*Selected engineering and AI projects, with runnable demos and dated experiment records.*

---

## Selected work

### [Civil Buddy](https://github.com/LUOaini1213/civil-buddy) — agentic AI workspace for engineering

`NL → agent routing → deterministic tools → HITL → evaluation`

66-role workflow system for civil / construction / tendering; the packing engine is one deterministic tool inside it.

- Coordinates, container counts and prices come from tools — the model never writes them
- Human approval gates every high-risk action (eligibility, bid, write-to-disk)
- **128** deterministic packing evaluations (16 lanes × 8 rounds; [recorded 128/128 PASS](https://github.com/LUOaini1213/civil-buddy/blob/main/docs/eval/fanout16x8-2026-09-02/rollup.md)); CI runs a 2×1 offline slice. Separate steps / llm_toolcall shadow evaluation uses `policy_fallback` when no model key is configured
- Policy engine and failure recovery: refuse with a reason → retry → degrade with an audit trail → cost circuit-breaker
- Golden-path E2E 8/8 (measured at R13, needs playwright, not in CI)

[Download a trial build (Releases)](https://github.com/LUOaini1213/civil-buddy/releases) · [one-page PRD with acceptance table](https://github.com/LUOaini1213/civil-buddy/blob/main/docs/civil-buddy/prd-pack-ship.md)

![Civil Buddy workbench](https://raw.githubusercontent.com/LUOaini1213/civil-buddy/main/docs/assets/workbench.png)

### [NAVSIM ability ladder](https://github.com/LUOaini1213/navsim-ability-ladder) — what caps open-loop planning

An ablation on the full NAVSIM `navtest` split — 12,146 scenes, 136 logs, one metric cache, learned models trained on navtrain (103,288 scenes), three seeds per cell, paired bootstrap intervals on every gain.

- The map is worth about seven times what ground-truth boxes are worth: +0.296 [+0.288, +0.305] against +0.040 [+0.035, +0.044]
- Ground-truth perception is not a free input: once the model has the map, adding GT boxes is significantly negative in all three seeds (−0.044 / −0.031 / −0.047) while the open-loop loss barely moves — the training objective cannot see it
- The learned component earns its place in the speed profile and nowhere else (+0.028 / +0.034 / +0.032 across seeds); letting it draw the path is not separable from the rule
- The pipeline is calibrated before anything is claimed from it: on the same cache it reproduces the published baselines — ConstantVelocity 20.7 (paper 20.6), official EgoStatusMLP 65.5 / 67.4 / 66.3 (paper 66.4±0.9), Human 94.6 (paper 94.8)
- Open-loop L1 cannot select a model: rank correlation with PDMS is −0.83 overall but −0.64 across the seven competitive runs, inverting in places (dropout 0.2 fits better and scores worse). Sample size also changes the answer, so only full-split numbers are quoted

### GPU & systems — two controlled experiments with honest outcomes

[**cuda-fused-layernorm**](https://github.com/LUOaini1213/cuda-fused-layernorm) — fused residual-add + LayerNorm hand-written in CUDA C++ (NVRTC), ported from Triton: warp-shuffle + shared-memory block reduction, float64-referenced accuracy gate, numerical-stability sweep. Same-card three-way comparison on a T4 over 12 shapes: Triton 1.341× over eager, my CUDA 1.087×, **CUDA vs Triton 0.812× — it loses on every shape** (best 0.997×), most likely because Triton autotunes `num_warps` and block size per shape while mine uses a fixed heuristic. Written up as a negative result, not hidden.

[**vllm-sm75-throughput**](https://github.com/LUOaini1213/vllm-sm75-throughput) — a 10× vLLM throughput collapse on a GTX 1650 (sm_75, no tensor cores) traced to a cuBLAS fp16 GEMM small-M cliff: bandwidth 99.5 → 4.3 GiB/s from M=1 to M=2. The refutation experiment on a T4 — same sm_75, same Turing, tensor cores kept — shows 106.7 → 88.1 (0.83×) across three shapes. One variable differs and the ratio moves 20×; the attribution holds. Filed upstream: [pytorch#195716](https://github.com/pytorch/pytorch/issues/195716) (root cause) and [vllm#54950](https://github.com/vllm-project/vllm/issues/54950) (deployment trap, warning proposed).

### TikTok TechJam 2026 — four tracks, submitted 1 Sep; none placed

[Track 1 · Glass Box](https://github.com/LUOaini1213/track1) agent-observability middleware (span waterfalls, redaction, policy deny; official starter + my trace plane) · [Track 2 · RecAgent](https://github.com/LUOaini1213/recagent-techjam2026-track2) autonomous MLE loop, test 0.6015 vs FM 0.5946 with 0 manual edits · [Track 3 · fp16x3](https://github.com/LUOaini1213/fp16x3-transformer) 13/13 shapes PASS, median 2.83× on a T4 (2.07× on a P100) from fp32-accurate GEMMs on fp16 tensor cores; five of our own claims, FlashAttention among them, retracted after a self-audit · [Track 4 · ByteSize](https://github.com/LUOaini1213/track4) value-of-information stopping, +60 rank-1 at zero hit-rate loss, $0

### [EDA Copilot](https://github.com/LUOaini1213/eda-copilot) — flow Q&A over OpenROAD/ORFS that asks instead of guessing

Ran the full RTL→GDSII flow myself (ORFS official image, nangate45/gcd) and turned the 46 reports/logs plus 31 script docs into a 1,215-chunk corpus with line-level provenance. Seven structured stop codes (ambiguous metric, setup/hold unspecified, out of scope, …): **12/12** should-stop questions stop with the right code; with the guard off all 12 are answered anyway, each with a citation — a cited wrong answer is the dangerous kind. After the zero-relevance fusion fix, BM25 and hybrid both reach Hit@5 22/23 (0.957) on the 23-question set; versioned earlier results remain in the README. Wrong-platform, wrong-run and unrelated-question regressions now exercise the refusal boundary. Reading my own QoR report: TNS −7.18 vs WNS −0.16 (violations spread over many paths), timing buffers at 18.7% of standard-cell area with WNS still unconverged. Example-scale design, open 45 nm library, default parameters — not fab yield data.

### [Counterask](https://github.com/LUOaini1213/counterask-webmcp) — a storefront whose tools ask back · [live](https://luoaini1213.github.io/counterask-webmcp/)

Built for The WebMCP Challenge: a one-page menswear store on 9,901 real products (Amazon Reviews 2023) whose `search_products` tool returns **a question** whenever answering would be a guess; `answer_question` is registered only while a question is open, and checkout is a declarative form only a person can submit. No server, no model, zero tokens. Verified on Chrome 152 with WebMCP enabled, through `document.modelContext` itself. The store parses the whole sentence an agent relays — budget, refusals, stated attributes: on 800 sentences generated from product records, Hit@10 0.793 with a keyword matcher → **0.999** with the parser (0.993 on the rebuilt index, 0.991 under held-out phrasings), refusals inverted into requirements 100% → 0, budget broken in the top 10 31% → 0. The stopping rule counts expected survivors instead of entropy and asks only when a question clears at least 10 candidates; a "clear leader" shortcut and one-step lookahead were both built, measured and left off. Teammate Cui Zixuan's independent implementation lives on the [`cuizi-rewrite`](https://github.com/LUOaini1213/counterask/tree/cuizi-rewrite) branch of the sibling repo; five of its ideas were folded back in.

### [RepostGuard](https://github.com/LUOaini1213/tiktok-techjam-2026-track5) — AI-image detection scored on the repost, not the original

What circulates is never the original, so the evaluation runs on the transformed image. A frozen CLIP + DINOv2-small pair (~110M together, CPU-only) plus a 28-D native-resolution forensic vector, measured across **all 15** real repost transforms on a held-out 1,400-image slice of SID-Set with bootstrap intervals: clean AUC **0.981**, mean over 14 transforms **0.977**, 0.966 on an unseen generator family. The finding worth reading: the forensic branch is *the entire* cross-source generalisation (a CLIP-only probe scores 0.54 on unseen-generator thumbnails, chance is 0.50) **and** the thing that collapses under noise — it needs a noise training view to be safe, worth −0.006 and +0.004 apart and +0.014 together. A leakage control shows it is not reading JPEG history (≤ +0.0009 AUC when both classes are re-encoded). Multi-crop TTA was measured at −0.0039 and left off. **Built against the TechJam Track 5 brief and never submitted — not a competition entry.**

### [LP / MIP from scratch](https://github.com/LUOaini1213/lp-mip-from-scratch) — the model matters more than the solver

Modelling layer, two-phase tableau simplex, branch and bound and real Gomory fractional cuts, every answer cross-checked against HiGHS. Same problem written two ways: the assignment formulation is totally unimodular, so the relaxation is integral and B&B closes in **one node**; big-M gives the identical answer with the bound collapsed from 3.0 to 1.0 and **21–31 nodes**. Tightening big-M from 10000 to each variable's own capacity moves the bound 1086.54 → 970.51 and nodes 19 → 5. Dantzig pricing cycles on Beale's example (203 iterations, no termination) where Bland takes 9; on Klee–Minty it takes exactly 2ⁿ−1. **Both useful results are negative**: cuts are not free (n=12 knapsack — bound improves, tree grows 29 → 31), and cut validity is checked by enumerating all 5,376 integer points rather than by reading the code. **Written 2026-09-08; it corresponds to no past coursework or job, and column generation is not implemented.**

### [campus-bus-routing](https://github.com/LUOaini1213/campus-bus-routing) — testing a claim where it could not be falsified

Time-dependent shortest path on a 23-node / 58-edge graph, with four solvers (heap Dijkstra, A\*, label-correcting, brute force) agreeing over **600** cross-checked queries. "A binary heap brings this to O(|E| + |V| log |V|)" cannot be falsified at 23 nodes, so the heap was isolated on grid networks: **1.56× at 100 nodes, 17.03× at 4,900**. "Under 50 ms" needs its method attached — same code, p99 **0.44 ms** with connection reuse and **515 ms** with a fresh connection per request, while solving itself is 0.035 ms; the p50 is *better* in the slow row. Fleet size is a ceiling function, so removing one vehicle needs a **6.75%** cut in cycle time, not any cut. **A September 2026 rebuild, not the 2024 original**: the source traces were never archived, the network and speed history are synthetic, and the repo deliberately does not reproduce the figures once quoted from that work.

### [CE5001 — flood-resilient bus network](https://luoaini1213.github.io/#proj-ce5001) — evaluation / research

200 paired experiments, rule agents vs LLM agents on flooded multimodal networks (DEM + SUMO; 793 services, 5,201 stops). Dense CBD: rule agents cut related travel time **62.2%**. [Report PDF](https://luoaini1213.github.io/files/CE5001_report.pdf)

### [CE5212 — LLM as approver](https://github.com/LUOaini1213/ce5212-llm-coordinator) · [CE5203 — AYE weaving](https://github.com/LUOaini1213/ce5203-aye-weaving) · [malaysia-auto-ask](https://github.com/LUOaini1213/malaysia-auto-ask)

Rules propose, the model only says yes/no — course log **137 of 180 ticks (76%) never called it**, the 43 that did were all approved with 0 vetoes, and a synchronous call cost Bus 95 +2.2 min · YOLOv11 counts + SUMO ramp metering; **−22.7%** peak network time loss in the original course report, with the recovered controller and a separately reported 12-scenario rerun now in the repository · ask-data demo that stops when the metric is ambiguous — 30 questions: 22 correct, 8 correctly refused

---

## Stack

**AI / product:** agent workflows · LLM evaluation · HITL · tool calling · guardrails · PRD / acceptance
**Engineering:** Python · PyTorch · CUDA C++ (NVRTC) · Triton · vLLM · FastAPI · TypeScript · Rust · SUMO · OpenROAD/ORFS · WebMCP · SQL
**Domain:** transport engineering · construction workflows · tendering
