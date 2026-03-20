# Memory System

## 1. 3-Layer Memory Architecture

### A. Working Memory (Job-Specific)
- **Scope:** The active production cycle for a single piece of content.
- **Location:** `memory/active_jobs/[job_id].json` and `threads/[job_id]_thread.json`.
- **Purpose:** Track current state, intermediate outputs, and rework comments.

### B. System Memory (Long-Term Learning)
- **Scope:** Historical data across all previous jobs.
- **Location:** `memory/lessons/`.
- **Files:**
  - `hook_patterns.md`: Analysis of high-performing vs. rejected hooks.
  - `rejected_patterns.md`: Common reasons for rework/rejection.
  - `approved_examples.md`: Gold-standard outputs for reference.
  - `usage_metrics.md`: Historical tracking of token consumption, runtime, rework frequency, and estimated cost per stage and per content job.
- **Purpose:** Improve agent performance over time through pattern recognition.

### C. Brand Memory (Stable Foundation)
- **Scope:** Core brand identity and constraints.
- **Location:** `brand/`.
- **Files:** `brand_system.md`, `content_pillars.md`.
- **Purpose:** Provide the primary truth for all agents.

### D. Asset Memory (Generated and Final Assets)
- **Scope:** Visual and production assets associated with each content job.
- **Location:** `assets/[job_id]/`
- **Subfolders:**
  - `briefs/` → image briefs, video briefs, chart specs
  - `generated/` → AI-generated images or drafts
  - `approved/` → approved visuals for final use
  - `exports/` → final carousel images, PDFs, thumbnails, publish-ready files
- **Purpose:** Preserve traceability, reuse, comparison across versions, and final publishing assets.

---

## 2. Storage & Archiving Logic
- **Initialization:** Create a fresh JSON in `active_jobs/` and a thread JSON.
- **Persistence:** Save state after every agent handoff.
- **Completion:** Upon final human approval, move the job state to `archived_jobs/`.
- **Harvesting:** Every 5 archived jobs, the Orchestrator should update `lessons/` with new patterns.
- **Asset Preservation:** On approval, all associated assets must be copied or moved to `assets/[job_id]/approved/` and final publish-ready files to `assets/[job_id]/exports/`.
  - Temporary generated assets that are rejected may be cleaned periodically, but approved assets must be preserved.