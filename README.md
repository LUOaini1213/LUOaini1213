# Wenjie Luo · 罗文杰

Agentic AI product and evaluation, from a transport-engineering background.
NUS MSc Civil Engineering (Transport), graduating Jan 2027 · Singapore.

Hard numbers stay in deterministic tools. The model only drafts. High-risk actions need a person. Whether the model was put in the right place is judged on a closed loop, not on the loss.

[Site](https://luoaini1213.github.io) · [English](https://luoaini1213.github.io/en.html) · [CVs](https://luoaini1213.github.io/resumes/) · e1576499@u.nus.edu · wenjiluo7@gmail.com

Dated write-ups: [PROJECTS.md](PROJECTS.md) · commands and dependencies: [RUNNABLE_PROJECTS.md](RUNNABLE_PROJECTS.md)

## Selected

| Project | What to inspect | Demo or evidence |
|---|---|---|
| [Glass Box / Track 1](https://github.com/LUOaini1213/track1) | Agent span waterfalls, redaction and durable OTLP delivery with explicit failure states. Official starter plus my observability layer; single-user PoC. | [No-key replay demo](https://github.com/LUOaini1213/track1#try-the-trace-ui-without-an-api-key) · [Recovery and overhead record](https://github.com/LUOaini1213/track1/blob/7d3b02dab693de2d6b45ced69ac9b4c04eaaab4d/docs/OTLP_DELIVERY.md) |
| [fp16x3 Transformer](https://github.com/LUOaini1213/fp16x3-transformer) | Compensated FP16 GEMMs with FP32 input/output and precision checks. Recorded T4 performance gates include retained failures. | [Measured results and limits](https://github.com/LUOaini1213/fp16x3-transformer/blob/0936d91bc38752aecd9e066287d8f4c47652dee7/README.md#what-the-measurements-support) · [Run and audit](RUNNABLE_PROJECTS.md#recompute-recorded-research-results) |
| [LLM judge experiments](https://github.com/LUOaini1213/llm-eval-experiments) | Frozen judge replies, provenance auditing and question-cluster uncertainty on a personally constructed evaluation set. | [Sensitivity report](https://github.com/LUOaini1213/llm-eval-experiments/blob/e20b6e016372e6e63ebe0586d44f609095a85c5f/results/e1/cluster_sensitivity.md) |
| [Manufacturing Planning Agent](https://github.com/LUOaini1213/manufacturing-planning-agent) | Synthetic capacity allocation and downtime replan. HiGHS solves, SimPy checks, and the agent is not credited with the solver. | [Scenario and reproduction guide](https://github.com/LUOaini1213/manufacturing-planning-agent#readme) |
| [NAVSIM ability ladder](https://github.com/LUOaini1213/navsim-ability-ladder) | Full-split ablation of what caps open-loop planning, with paired bootstrap intervals. | [Results and reproduction](https://github.com/LUOaini1213/navsim-ability-ladder#readme) |
| [Counterask](https://github.com/LUOaini1213/counterask-webmcp) | WebMCP tools ask for missing information instead of guessing. Browser interaction needs WebMCP support. | [Live store](https://luoaini1213.github.io/counterask-webmcp/) · [Run locally](RUNNABLE_PROJECTS.md#try-locally) |

More engineering work: [Civil Buddy](https://github.com/LUOaini1213/civil-buddy) · [vLLM sm_75 throughput](https://github.com/LUOaini1213/vllm-sm75-throughput) · [EDA Copilot](https://github.com/LUOaini1213/eda-copilot) · [CE5203 AYE weaving](https://github.com/LUOaini1213/ce5203-aye-weaving).

[Choose a role and open matching project evidence](https://luoaini1213.github.io/resumes/) · [October 2026 follow-ups](PROJECTS.md#october-2026-follow-ups).

## Stack

Python · PyTorch · CUDA / Triton · vLLM · FastAPI · TypeScript · Rust · SUMO · WebMCP
