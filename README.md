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
- **128** automated packing evaluations (16 lanes × 8 rounds; [re-run 2 Sep 2026, 128/128 PASS](https://github.com/LUOaini1213/civil-buddy/blob/main/docs/eval/fanout16x8-2026-09-02/rollup.md)); same-order comparison: LLM self-planning 29 containers vs the engine's 25
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

### TikTok TechJam 2026 — four tracks, submitted 1 Sep, results pending

[Track 1 · Glass Box](https://github.com/LUOaini1213/track1) agent-observability middleware (span waterfalls, redaction, policy deny; official starter + my trace plane) · [Track 2 · RecAgent](https://github.com/LUOaini1213/recagent-techjam2026-track2) autonomous MLE loop, test 0.6015 vs FM 0.5946 with 0 manual edits · [Track 3 · GPU kernel](https://github.com/LUOaini1213/tiktok-techjam-2026-track3) 13/13 shapes PASS, median 2.07× · [Track 4 · ByteSize](https://github.com/LUOaini1213/track4) value-of-information stopping, +60 rank-1 at zero hit-rate loss, $0

### [CE5001 — flood-resilient bus network](https://luoaini1213.github.io/#proj-ce5001) — evaluation / research

200 paired experiments, rule agents vs LLM agents on flooded multimodal networks (DEM + SUMO; 793 services, 5,201 stops). Dense CBD: rule agents cut related travel time **62.2%**. [Report PDF](https://luoaini1213.github.io/files/CE5001_report.pdf)

### [CE5212 — LLM as approver](https://github.com/LUOaini1213/ce5212-llm-coordinator) · [CE5203 — AYE weaving](https://github.com/LUOaini1213/ce5203-aye-weaving) · [malaysia-auto-ask](https://github.com/LUOaini1213/malaysia-auto-ask)

Rules propose, the model only says yes/no — course log **43/44**, and a synchronous call cost Bus 95 +2.2 min · YOLOv11 counts + SUMO ramp metering, peak network time loss **−22.7%** · ask-data demo that stops when the metric is ambiguous — 30 questions: 22 correct, 8 correctly refused

---

## Stack

**AI / product:** agent workflows · LLM evaluation · HITL · tool calling · guardrails · PRD / acceptance
**Engineering:** Python · PyTorch · FastAPI · Rust · SUMO · SQL
**Domain:** transport engineering · construction workflows · tendering
