# Run the projects / 项目运行入口

Updated 2026-09-12. Start from each linked repository's README for installation,
then run the command below from that repository root. Commands use the activated
project virtual environment; Node projects use the version in `package.json`.

## Try locally

| Project | Entry point | What it produces / prerequisites |
|---|---|---|
| [Civil Buddy](https://github.com/LUOaini1213/civil-buddy) | `python scripts/demo_one_shot.py --all` | Packing workflow, confirmation checkpoint, trace, closed-loop and shadow checks. No key uses the deterministic/fallback path. `python -m uvicorn gateway.app:app` serves `/workbench`. |
| [Glass Box / Track 1](https://github.com/LUOaini1213/track1) | `npm ci`, then `npm run demo` | Browser trace UI and real control plane with labeled replay fixtures. `npm run check` covers 150 tests, build and HTTP replay success/failure/denial. Live Codex mode requires its separately documented CLI/auth/runtime. |
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
| [fp16x3 Transformer](https://github.com/LUOaini1213/fp16x3-transformer) | Committed raw logs, result CSVs and report-generation scripts. | Run `python run_all.py --shapes 1-13 --device cuda --dtype float32 --out results/rerun.csv` in the documented CUDA/PyTorch environment. Full 13-shape timings require suitable GPU memory; Kaggle/Colab entry scripts are included. |
| [CUDA fused LayerNorm](https://github.com/LUOaini1213/cuda-fused-layernorm) | Committed same-card three-way results and numerical-stability records. | `python bench.py` and `python stability.py` require NVIDIA CUDA, PyTorch and CuPy. CPU inspection does not validate GPU speedups. |
| [vLLM sm75 throughput](https://github.com/LUOaini1213/vllm-sm75-throughput) | Committed GTX 1650/T4 measurements and controlled-attribution scripts. | Follow the README hardware/environment recipe. A new throughput comparison requires the relevant sm75 GPUs and model/runtime; hardware-dependent results were not rerun on this CPU host. |

## Repository relationships

- `civil-buddy` is the current product; the old packing engine belongs inside it.
  `civil-buddy-workbench` and `launchpad-trace-plane` are archived historical trees.
- `counterask-webmcp` is the selected storefront; the sibling `counterask` repository
  contains the independent teammate rewrite and branch history.
- This profile and the [personal site](https://luoaini1213.github.io/) provide the
  navigation and [six-role CV library](https://luoaini1213.github.io/resumes/).
  Private course, job-application and backup repositories are not public demo dependencies.

Local verification during this pass covered real workflow execution for Civil Buddy,
Track 1, EDA, Malaysia, CE5203, CE5212, LP/MIP, bus routing and Counterask; Track 4
also completed all 200 public sessions on the original 50,000-product catalog
using the zero-token standard-library path. RepostGuard passed 50 tests (two
dataset checks skipped) and real two-image inference with the shipped head.
NAVSIM report regeneration and RecAgent prediction recombination were also rerun.
Each repository's Actions history gives the exact commit and CI scope. A green
CPU test job does not assert that a full GPU experiment or live model call ran.
