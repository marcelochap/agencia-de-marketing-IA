# Research Dossier: Data-Driven Bottleneck Detection

## 1. Executive Summary
Industrial experience often misses "dynamic bottlenecks" that shift based on product mix or micro-variabilities. Data-driven approaches (AI, Process Mining, Digital Twins) reveal the "hidden factory," providing up to 30% OEE increases by identifying patterns invisible to human operators.

---

## 2. Key Insights & Evidence

### A. The "Hidden Factory" & Micro-Atrasos
- **Insight:** Small deviations (e.g., 3% cycle time drift due to cooling issues) propagate into major bottlenecks (2+ hours) by the end of a shift.
- **AI Application:** Agentic systems can detect these drifts early and autonomously adjust feed rates to stabilize the line.
- **Informal Routes:** Process Mining reveals "shadow processes" where operators create informal routes to bypass perceived slow stations, destabilizing global throughput.

### B. Acoustic & Sensory Patterns
- **Case Study:** Use of 300 million hours of machine audio data to train algorithms that detect wear-and-tear vibrations inaudible to human technicians.
- **Impact:** Prevents catastrophic failures that cause multi-week bottlenecks.

---

## 3. Industrial Benchmarks
- **OEE Gains:** 30%+ increase in OEE for non-serial powertrain assembly lines using the "Turning Point Method."
- **Planning Accuracy:** 31% to 47% reduction in Mean Absolute Error (MAE) for production time estimates using XGBoost/Regression Trees.
- **Cost Reduction:** 5% to 7% monthly cost compression via Digital Twins and Reinforcement Learning for batch sequencing.
- **Throughput:** 8% to 15% increase in sustained throughput with real-time constraint management layers.

---

## 4. Operational Constraints & Risks
- **Timestamp Granularity:** Many legacy MES/ERP systems lack separate start/end timestamps. Without this, it is mathematically impossible to distinguish **Processing Time** (machine efficiency) from **Queue Time** (logistics efficiency).
- **IT/OT Silos:** Root causes for machine downtime (e.g., missing parts) are often stuck in ERP silos, invisible to the MES layer.
- **Small Data Risks:** SMEs face "overfitting" risks when training models on noisy or small datasets (e.g., manual operator typos).

---

## 5. Source Information
- **Source:** NotebookLM Research Session (ID: cf9fa86f)
- **Link:** https://notebooklm.google.com/notebook/33dd9a49-c02f-4f4c-a285-f2fca9fa1878

---

## Handoff to Designer/Copywriter
- **Leverage Point:** The "Processing vs. Queue Time" timestamp paradox is a great technical hook.
- **Visual Idea:** A "Hidden Factory" map showing recursive rework loops.
- **Authority Angle:** Focus on the distinction between *intuition* and *stochastic interaction* in complex lines.
