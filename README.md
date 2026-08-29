# Wenjie Luo

**Agentic AI Product × Engineering Workflows**  
NUS MSc Civil Engineering (Transportation) · AI Product Builder

Building reliable AI agents for complex workflows — **LLM orchestration × deterministic tools × HITL × evaluation**.

[Site](https://luoaini1213.github.io) · [Civil Buddy](https://github.com/LUOaini1213/civil-buddy) · [Portfolio pack](https://github.com/LUOaini1213/ai-product-portfolio) · e1576499@u.nus.edu

---

## Featured (10 seconds)

### 1. [Civil Buddy](https://github.com/LUOaini1213/civil-buddy) — hero product

**Agentic AI Workspace for Engineering**

`NL → Agent routing → Tools → HITL → Evaluation`

66-role workflow system for civil engineering. Packing / stowage is **one engine inside the product**, not a separate story (the old `packing-agent` repo is merged here).

- Deterministic tools for verifiable engineering outputs
- Human approval for high-risk decisions
- Policy engine & failure recovery
- Shadow evaluation + E2E golden-path testing (**128** in-repo pipelines; golden path **8/8**)
- Tendering → compliance → delivery **drafts** (not legal sign-off)

![HITL packing orchestration](https://raw.githubusercontent.com/LUOaini1213/civil-buddy/main/docs/diagrams/langgraph-create-app.jpg)

### 2. [CE5001 — flood network agents](https://luoaini1213.github.io/#proj-ce5001) — evaluation / research

**I evaluate AI; I do not only ship demos.**

200 paired experiments: rule agents vs LLM agents on flooded multimodal networks (DEM + SUMO). Dense CBD: rule agents cut related travel time **62.2%**. Sparse nets: LLM agents reached similar impact with far fewer actions.

Report: [CE5001 PDF](https://luoaini1213.github.io/files/CE5001_report.pdf)

### 3. [CE5212 — LLM as approver](https://github.com/LUOaini1213/ce5212-llm-coordinator) — Transport × AI

Transportation is not a line on a CV. In a real-time traffic lab, rules propose; the model only says yes/no and **never writes link IDs**. Course log: **43 / 44**.

Sister domain project: [CE5203 AYE weaving](https://github.com/LUOaini1213/ce5203-aye-weaving) — ramp metering cut peak network total time loss **22.7%**.

---

## Not the hero

| Repo | Role |
|------|------|
| [ai-product-portfolio](https://github.com/LUOaini1213/ai-product-portfolio) | Application pack (CVs, one-pagers, zip). Not a product. |
| [malaysia-auto-ask](https://github.com/LUOaini1213/malaysia-auto-ask) | Small ask-data eval demo (whitelist SQL, stop-and-ask). |
| [civil-buddy-workbench](https://github.com/LUOaini1213/civil-buddy-workbench) | **Archive.** Merged into `civil-buddy`. |

---

## Stack (last)

**AI / Product:** Agentic AI · LLM evaluation · HITL · tool calling · guardrails  
**Engineering:** Python · FastAPI · Rust · REST  
**Domain:** Civil engineering · transportation · tendering · construction workflows
