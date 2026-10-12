# Run the projects / 项目运行入口

Glass Box, fp16x3 and LLM judge entries updated 2026-10-10; the remaining notes
retain their September 2026 verification scope. Start from each linked repository's README for installation,
then run the command below from that repository root. Commands use the activated
project virtual environment; Node projects use the version in `package.json`.

## October 12 engineering demonstrations

These new entrances have a separate October 12 scope; they do not rewrite the
September experiments or claim new model or industrial performance. Start with
the [bilingual cases](https://luoaini1213.github.io/cases/en.html), then use the
repository-specific setup before running these commands.

| Project | Public entrance | Actual local reproduction |
|---|---|---|
| [Manufacturing planning](https://github.com/LUOaini1213/manufacturing-planning-agent) | [Recorded five-step replay](https://luoaini1213.github.io/manufacturing-planning-agent/) — saved HiGHS/SimPy computations, no hosted Python solver | `python -m mpa.demo --port 8840` — edit an outage, compare, explicitly confirm and advance, introduce another event, export the exact trace. No API key or shop-floor connection. |
| [IFC review](https://github.com/LUOaini1213/ifcsg-precheck) | [Authored three-slab report workflow](https://luoaini1213.github.io/ifcsg-precheck/) — illustrative rules, filters and JSON/CSV downloads; no visitor-file processing | `python scripts/report_demo.py --output-dir demos/report-review`, then `python scripts/report_demo.py --check`. Real check/enrich/check and independent typed STEP readback; official workbook and private models are not included. |
| [Driving-scene 3DGS](https://github.com/LUOaini1213/driving-3dgs) | [Actual interactive scene](https://luoaini1213.github.io/driving-3dgs/) — load, move, reset and return to preview | Follow the [source-pinned viewer build](https://github.com/LUOaini1213/driving-3dgs/blob/6a584b45579c333e1d2461ff4d64ff15b056e775/docs/PUBLIC_VIEWER.md). Reuses the archived scene; no retraining or new browser quality measurement. |

Manufacturing and IFC demo commands require their documented Python dependencies.
Use the source-pinned [manufacturing browser guide](https://github.com/LUOaini1213/manufacturing-planning-agent/blob/b00721143d88b61f98894f853626fee0ba572676/docs/BROWSER_DEMO.md)
and [IFC report review guide](https://github.com/LUOaini1213/ifcsg-precheck/blob/fd48ad5664be8903442a1b70db917a7059830999/docs/REPORT_REVIEW.md)
for the exact setup and interpretation of these examples.
The 3D viewer needs WebGL 2 and WebAssembly; layout checks do not establish phone
frame rate or memory usage. Every case retains its input and interpretation limits.

## Try locally

| Project | Entry point | What it produces / prerequisites |
|---|---|---|
| [Civil Buddy](https://github.com/LUOaini1213/civil-buddy) | `python scripts/demo_one_shot.py --all` | Packing workflow, confirmation checkpoint, trace, closed-loop and shadow checks. No key uses the deterministic/fallback path. `python -m uvicorn gateway.app:app` serves `/workbench`. |
| [Glass Box / Track 1](https://github.com/LUOaini1213/track1) | `npm ci`, then `npm run demo` | Node 22+ and npm 10+. Real control plane and browser trace UI use labeled replay fixtures, with no model key, Codex CLI or Docker required. `npm run check` verifies types, tests, build and HTTP recovery/replay. To see delivery change without another model task, run `npm run build`, then `npm run demo:otlp -- 503`; enter `success` in its terminal. [Fault modes and limits](https://github.com/LUOaini1213/track1/blob/7d3b02dab693de2d6b45ced69ac9b4c04eaaab4d/docs/OTLP_DELIVERY.md). Live Codex mode has separate CLI/auth/runtime requirements. |
| [EDA Copilot](https://github.com/LUOaini1213/eda-copilot) | `python -m unittest discover -s tests -v` | Retrieval/refusal checks against the included ORFS report corpus. README gives interactive ask/evaluation commands. A new physical-design run requires ORFS; the corpus only contains nangate45/gcd base. |
| [Malaysia Auto Ask](https://github.com/LUOaini1213/malaysia-auto-ask) | `python scripts/ask_cli.py '2025年纯电丰田TIV多少'` | White-listed SQL, clarification and provenance over the included synthetic market data. `python scripts/eval.py` reruns 30 questions. No production market-data access implied. |
| [CE5203 AYE weaving](https://github.com/LUOaini1213/ce5203-aye-weaving) | Follow [reproduction commands](https://github.com/LUOaini1213/ce5203-aye-weaving/blob/master/docs/REPRODUCTION.md) | SUMO controller, 12 peak/off-peak scenarios, raw XML and comparison report. Requires SUMO/TraCI. Original course figures and September 2026 reruns differ and are separately reported. |
| [CE5212 coordinator](https://github.com/LUOaini1213/ce5212-llm-coordinator) | `python scripts/mock_compare.py` | Three deterministic ticks, semantic intent and grounded edge IDs; 16 unit tests. Full course SUMO/Ollama runs require the private course network and demand. |
| [LP/MIP from scratch](https://github.com/LUOaini1213/lp-mip-from-scratch) | `python -m unittest discover -s tests -v`, then `python bench/bench_all.py --check` | 29 tests and committed benchmark checks. Install the documented SciPy/HiGHS reference dependency. |
| [Campus bus routing](https://github.com/LUOaini1213/campus-bus-routing) | `python -m unittest discover -s tests -v` | 37 routing, HTTP and numerical checks. A synthetic September 2026 rebuild; the unarchived 2024 source data is not recreated. |
| [Counterask WebMCP](https://github.com/LUOaini1213/counterask-webmcp) | `npm test`, then `npm run smoke` | Parser and fuzz checks, tool calls and a small catalog benchmark. [Browser demo](https://luoaini1213.github.io/counterask-webmcp/). Native `document.modelContext` interaction needs a supporting browser with WebMCP enabled. |
| [ByteSize / Track 4](https://github.com/LUOaini1213/track4) | `python -S demo/fixture.py`; `python -S -m unittest discover -s tests -v` | Original two-product dialogue demo and 145 offline tests (one staged-ZIP check skips). Import an existing frozen catalog with the checksum verifier for full scoring; MiniLM weights are needed to match its recorded configuration. |
| [RepostGuard](https://github.com/LUOaini1213/tiktok-techjam-2026-track5) | `python infer.py --input_dir samples --output preds.json` | Per-image probabilities using the shipped head and downloaded frozen encoders. Install the pinned scikit-learn and NumPy 2 dependencies first. CPU works; the full SID-Set training/evaluation pipeline is separate. |

## Recompute recorded research results

| Project | Low-cost verification | Full experiment conditions |
|---|---|---|
| [NAVSIM ability ladder](https://github.com/LUOaini1213/navsim-ability-ladder) | `python -m unittest discover -s tests -v`: 23 checks regenerate the reports from committed per-scene CSVs. | NAVSIM v1.1 devkit, dataset and metric cache are needed to train/score new agents. Recomputing reports is separate from rerunning simulator inference. |
| [RecAgent](https://github.com/LUOaini1213/recagent-techjam2026-track2) | `python -m pytest tests`; `python scripts/official_final.py --check` reproduces both final prediction arrays bit for bit from committed ensemble members. | Full metric recomputation requires KuaiRand-Pure labels and the feature cache; retraining is documented and uses CPU. |
| [fp16x3 Transformer](https://github.com/LUOaini1213/fp16x3-transformer) | `python -m scripts.verify_next_evidence --maintained-runtime` audits committed hashes and reports using only the standard library. With the documented Torch install, `python -m scripts.run --mode quick --device cpu --shape 2` is a small correctness check. | [Runtime guide](https://github.com/LUOaini1213/fp16x3-transformer/blob/0936d91bc38752aecd9e066287d8f4c47652dee7/docs/QUICKSTART.md). New timings require compatible CUDA hardware and sufficient memory. `python -m scripts.run --mode balanced --device cuda --shapes 1-13 --output results/local_run_balanced.json` runs the opt-in profile; its recorded performance gates vary by session. CPU correctness or an intact evidence audit does not establish a new speedup. |
| [LLM judge experiments](https://github.com/LUOaini1213/llm-eval-experiments) | Python 3.11 and `pip install -r requirements.txt`, then `python scripts/e1_cluster_sensitivity.py --check` checks JSON, Markdown and README against the committed replies and source hashes. `python -m pytest -q` runs the test suite. | [Frozen sensitivity report](https://github.com/LUOaini1213/llm-eval-experiments/blob/e20b6e016372e6e63ebe0586d44f609095a85c5f/results/e1/cluster_sensitivity.md). This offline recomputation makes no model calls. New judge runs require the documented model setup and an isolated run ID; post-hoc sensitivity does not change the original hypothesis tests or recommendations. |
| [CUDA fused LayerNorm](https://github.com/LUOaini1213/cuda-fused-layernorm) | Committed same-card three-way results and numerical-stability records. | `python bench.py` and `python stability.py` require NVIDIA CUDA, PyTorch and CuPy. CPU inspection does not validate GPU speedups. |
| [vLLM sm75 throughput](https://github.com/LUOaini1213/vllm-sm75-throughput) | Committed GTX 1650/T4 measurements and controlled-attribution scripts. | Follow the README hardware/environment recipe. A new throughput comparison requires the relevant sm75 GPUs and model/runtime; hardware-dependent results were not rerun on this CPU host. |

## Repository relationships

- `civil-buddy` is the current product; the old packing engine belongs inside it.
  `civil-buddy-workbench` and `launchpad-trace-plane` are archived historical trees.
- `counterask-webmcp` is the selected storefront; the sibling `counterask` repository
  contains the independent teammate rewrite and branch history.
- This profile and the [personal site](https://luoaini1213.github.io/) provide the
  navigation and [seven-role CV library](https://luoaini1213.github.io/resumes/).
  Private course, job-application and backup repositories are not public demo dependencies.

The September 2026 verification covered real workflow execution for Civil Buddy,
Track 1, EDA, Malaysia, CE5203, CE5212, LP/MIP, bus routing and Counterask; Track 4
also completed all 200 public sessions on the original 50,000-product catalog
using the zero-token standard-library path. RepostGuard passed 50 tests (two
dataset checks skipped) and real two-image inference with the shipped head.
NAVSIM report regeneration and RecAgent prediction recombination were also rerun.
The October follow-ups add Track 1 OTLP recovery and evidence audits for fp16x3
and LLM judge sensitivity; their fixed records are linked above.
Each repository's Actions history gives the exact commit and CI scope. A green
CPU test job does not assert that a full GPU experiment or live model call ran.
