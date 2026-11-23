# FactoryEye — Project Plan

## Goal
Build a local-first industrial monitoring demo combining visual defect detection, machine Remaining Useful Life (RUL) prediction, explainable alerts, and a React dashboard.

## Scope (v1)
- **Vision:** PatchCore via anomalib; train on normal images only; output anomaly score, verdict, heatmap.
- **Maintenance:** NASA C-MAPSS FD001; Ridge baseline + LightGBM RUL predictor.
- **Decision layer:** transparent rules combine RUL and recent defect rate into severity, reason, and action.
- **Simulation:** replay public dataset samples as a simulated production feed. Clearly label simulation and the synthetic relationship between machine health and defects.
- **App:** FastAPI + SQLite + React dashboard; five views: Dashboard, Inspection, Machines, Alerts, Models.
- **Evaluation:** separate tuning/evaluation image splits; engine-level train/validation split; metrics and baseline comparison.
- **Constraints:** local/free; no paid API or LLM; no real factory/camera/PLC integration.

## System Flow
```text
MVTec images ──> PatchCore ──┐
                              ├─> Decision rules ─> SQLite ─> FastAPI ─> React
NASA sensors ──> RUL model ──┘          ▲
Dataset replay/simulator ────────────────┘
```

## Planned Repository
```text
FactoryEye/
├── main.py                 # local entry point
├── bin/                    # start/stop helper scripts
├── src/factoryeye/
│   ├── api/                # routes and request/response schemas
│   ├── core/               # settings, shared logic
│   ├── services/           # vision, RUL, simulator, decisions
│   ├── database/            # models, session, repository
│   └── utils/
├── frontend/                # React + Vite
├── data/                    # downloaded and prepared datasets (ignored)
├── models/                  # trained weights and outputs (ignored as needed)
├── scripts/                 # download, prepare, train, evaluate, demo
├── tests/
├── config/
├── docs/                    # only essential architecture / decisions
├── notebooks/                # exploration only
├── logs/                     # ignored
├── reports/                  # metrics / generated reports
├── requirements.txt
├── .gitignore
└── README.md
```

## Milestones
| ID | Milestone | Deliverable | Exit check |
|---|---|---|---|
| M0 | Repository & environment | Folder skeleton, Git, Python environment, dependency check | App skeleton runs; imports verified |
| M1 | Data preparation | Selected MVTec categories + FD001 prepared; split manifests and data checks | Dataset paths and splits validated; raw data not tracked |
| M2 | Vision pipeline | PatchCore train, inference, heatmap, threshold, evaluation | Predicts good/defect on sample; metrics saved |
| M3 | RUL pipeline | Features, baseline, LightGBM, evaluation, saved predictor | Model compared to baseline; validation metrics saved |
| M4 | Decision rules | Status/severity/action rules and tests | Boundary tests pass; alert reason is traceable |
| M5 | Backend & persistence | API, DB, model loading, simulator | API endpoints work; simulator records persist |
| M6 | Frontend | Five views using mock API data first | Navigation, states, and core interactions work |
| M7 | Integration & QA | Connect UI/API; end-to-end scenario; bug fixes | Main scenario passes; tests and manual checks complete |
| M8 | Portfolio release | README, demo assets, licensing/credits, optional static demo | Fresh clone instructions work; public repo is presentable |

## Key decisions / boundaries
- Start with three MVTec categories; choose after data inspection and runtime check.
- Use PatchCore CPU-compatible setup first; adjust backbone/image size only if resource limits require.
- Use FD001 for the initial RUL pipeline.
- Tune vision threshold using a tuning split; report final metrics on held-out evaluation split.
- Split NASA engines by engine ID to avoid leakage.
- Optional only: SHAP, Isolation Forest, WebSockets, Docker, live backend hosting.
- Do not commit raw datasets, secrets, or large model files.
- Deployment is not a blocker: local app + recorded demo; static replay mode can be added if useful.
