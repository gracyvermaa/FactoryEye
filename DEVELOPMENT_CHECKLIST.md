# FactoryEye — Development Checklist

Work milestone-by-milestone. Don't start the next milestone until the exit check passes. Commit at each milestone.

## M0 — Repository & environment
- [ ] Create the planned folder structure and initial Git commit.
- [ ] Set up Python virtual environment and install/verify core dependencies.
- [ ] Verify the backend skeleton starts.
**Done when:** the local skeleton runs and dependencies import.

## M1 — Data
- [ ] Obtain MVTec AD and NASA C-MAPSS FD001; record dataset credits/licensing.
- [ ] Select 3 MVTec categories after inspection.
- [ ] Create image tuning/evaluation manifests.
- [ ] Prepare FD001 tables, labels, and engine-level train/validation split.
**Done when:** scripts load the datasets and reproducible splits are saved.

## M2 — Vision
- [ ] Run PatchCore on one category and confirm resource usage is manageable.
- [ ] Train selected categories; implement inference and heatmap output.
- [ ] Tune thresholds on tuning split; evaluate on held-out split.
- [ ] Save metrics and example outputs.
**Done when:** sample image returns score, verdict, heatmap; evaluation results are saved.

## M3 — Predictive maintenance
- [ ] Prepare sensor features without future leakage.
- [ ] Evaluate simple baseline and Ridge.
- [ ] Train LightGBM and compare validation results.
- [ ] Implement prediction; save model, feature list, and metrics.
**Done when:** RUL prediction works and comparison results are documented.

## M4 — Decision rules
- [ ] Define status/severity/action thresholds.
- [ ] Implement pure rule functions with traceable reasons.
- [ ] Add boundary tests and alert de-duplication.
**Done when:** rule tests pass and sample alerts explain their trigger.

## M5 — Backend & simulator
- [ ] Add SQLite tables and seed/demo records.
- [ ] Add API routes for health, inspection, machines, alerts, summary, and model metrics.
- [ ] Load models once at startup.
- [ ] Implement dataset replay simulator and start/stop/speed controls.
**Done when:** API works and simulated records appear in storage.

## M6 — Frontend
- [ ] Build React/Vite layout and routing.
- [ ] Build Dashboard, Inspection, Machines, Alerts, Models pages with mock data.
- [ ] Implement responsive layout, loading/empty/error states, and navigation.
**Done when:** all views and core interactions work without backend.

## M7 — Integration & QA
- [ ] Connect pages to API and add polling.
- [ ] Verify scenario: simulator → inspection/health updates → alert → acknowledge.
- [ ] Test invalid uploads, API errors, persistence, and restart.
- [ ] Fix issues and run tests.
**Done when:** end-to-end flow is stable locally.

## M8 — Portfolio release
- [ ] Write concise README with architecture, setup, honest metrics, limitations, and credits.
- [ ] Add screenshots/demo recording and clearly label simulated data.
- [ ] Verify Git contains no datasets, secrets, or oversized artifacts.
- [ ] Test setup from a fresh clone; publish repository.
**Done when:** someone can understand and run the project using README instructions.

## Optional (only after v1)
- [ ] SHAP or Isolation Forest
- [ ] WebSockets
- [ ] Docker
- [ ] Static demo replay / deployment
