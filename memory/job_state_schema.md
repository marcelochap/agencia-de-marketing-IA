# Job State Schema

This document defines the central state object for a single content job in the multi-agent LinkedIn content system.

The job state is the single source of truth for:
- workflow progression
- ownership
- deliverables
- assets
- approvals
- feedback
- usage metrics
- version history

---

## Purpose

Each content job must have one structured state object that can be:
- read by the Orchestrator
- updated by each agent
- audited later
- archived after completion

---

## Recommended File Location

`memory/active_jobs/[job_id].json`

## Example JSON Object

```json
{
    "content_id": "2026-03-20-post-001",
    "status": "copy_ready",
    "current_owner": "reviewer",
    "next_step": "review_final",
    "review_cycles": 1,
    "current_version": 2,

  "metadata": {
    "title": "AI in Production Control",
    "campaign_id": "2026-q1-operational-efficiency",
    "piece_type": "carousel",
    "pillar": "Strategic Technology & AI",
    "period_objective": "Authority",
    "platform": "LinkedIn",
    "created_at": "2026-03-20T10:00:00Z",
    "updated_at": "2026-03-20T11:42:00Z",
    "priority": "normal",
    "asset_summary": {
      "needs_generated_visuals": true,
      "asset_count": 4,
      "final_format": "carousel"
    }
  },

  "brand_context": {
    "brand_system_path": "brand/brand_system.md",
    "content_pillars_path": "brand/content_pillars.md",
    "visual_system_path": "brand/visual_system.md"
  },

  "brief": {
    "topic": "AI-driven production control",
    "angle": "Unexpected bottlenecks revealed by data",
    "context": "Demonstrate operational differentiation and technical credibility",
    "research_direction": [
      "Industrial AI applications",
      "Process variability in heavy production",
      "Operational constraints"
    ]
  },

  "deliverables": {
    "strategist_output": "deliverables/2026-03-20-post-001/strategy.md",
    "researcher_output": "deliverables/2026-03-20-post-001/research.md",
    "designer_output": "deliverables/2026-03-20-post-001/design.md",
    "copywriter_output": "deliverables/2026-03-20-post-001/copy.md",
    "reviewer_output": "deliverables/2026-03-20-post-001/review.md",

    "image_briefs": [
      "assets/2026-03-20-post-001/briefs/image_brief_01.md"
    ],
    "generated_assets": [
      "assets/2026-03-20-post-001/generated/image_01.png",
      "assets/2026-03-20-post-001/generated/image_02.png"
    ],
    "approved_assets": [
      "assets/2026-03-20-post-001/approved/cover_v2.png",
      "assets/2026-03-20-post-001/approved/slide_03_chart.png"
    ],
    "final_exports": [
      "assets/2026-03-20-post-001/exports/carousel_final.pdf",
      "assets/2026-03-20-post-001/exports/carousel_slide_01.png",
      "assets/2026-03-20-post-001/exports/carousel_slide_02.png"
    ]
  },

  "human_feedback": {
    "status": "pending",
    "current_request": "",
    "last_feedback_at": ""
  },

  "feedback_history": [
    {
      "timestamp": "2026-03-20T11:10:00Z",
      "source": "reviewer",
      "type": "adjustment_request",
      "message": "Hook is still too generic. Tighten first line."
    },
    {
      "timestamp": "2026-03-20T11:28:00Z",
      "source": "human",
      "type": "visual_feedback",
      "message": "Prefer the second cover option."
    }
  ],

  "human_approval": {
    "status": "pending",
    "approved_by": "",
    "approved_at": "",
    "notes": ""
  },

  "usage_metrics": {
    "total_input_tokens": 0,
    "total_output_tokens": 0,
    "total_tokens": 0,
    "estimated_cost_usd": 0,
    "total_runtime_seconds": 0,
    "total_rework_count": 0,

    "stage_metrics": {
      "strategist": {
        "input_tokens": 0,
        "output_tokens": 0,
        "total_tokens": 0,
        "estimated_cost_usd": 0,
        "runtime_seconds": 0,
        "rework_count": 0
      },
      "researcher": {
        "input_tokens": 0,
        "output_tokens": 0,
        "total_tokens": 0,
        "estimated_cost_usd": 0,
        "runtime_seconds": 0,
        "rework_count": 0
      },
      "designer": {
        "input_tokens": 0,
        "output_tokens": 0,
        "total_tokens": 0,
        "estimated_cost_usd": 0,
        "runtime_seconds": 0,
        "rework_count": 0
      },
      "copywriter": {
        "input_tokens": 0,
        "output_tokens": 0,
        "total_tokens": 0,
        "estimated_cost_usd": 0,
        "runtime_seconds": 0,
        "rework_count": 0
      },
      "reviewer": {
        "input_tokens": 0,
        "output_tokens": 0,
        "total_tokens": 0,
        "estimated_cost_usd": 0,
        "runtime_seconds": 0,
        "rework_count": 0
      },
      "photographer": {
        "input_tokens": 0,
        "output_tokens": 0,
        "total_tokens": 0,
        "estimated_cost_usd": 0,
        "runtime_seconds": 0,
        "rework_count": 0
      }
    }
  },

  "agent_thread_path": "threads/2026-03-20-post-001_thread.json",
  "last_agent_update": {
    "agent": "researcher",
    "timestamp": "2026-03-20T10:32:00Z",
    "summary": "Research dossier and source link added"
   },

  "version_history": [
    {
      "version": 1,
      "timestamp": "2026-03-20T10:00:00Z",
      "updated_by": "strategist",
      "change_summary": "Initial strategy created"
    },
    {
      "version": 2,
      "timestamp": "2026-03-20T10:32:00Z",
      "updated_by": "researcher",
      "change_summary": "Research dossier and source link added"
    }
  ],

  "final_status": {
    "review_status": "pending",
    "publish_status": "not_ready",
    "archive_status": "active"
  }
}
```

---

## 2. Status Fields
- **Status:** Controls the workflow gate.
- **Current Owner:** Identifies who has the active task.

---

## 3. Versioning
- Each time an agent completes a task, the `current_version` increments if rework was performed.
- Previous outputs are tracked in the `version_history` array before being overwritten or replaced.

---

## 4. Deliverables Rules
- Text-only jobs may leave asset arrays empty.
- Generated assets must not be treated as approved automatically.

---

## 5. Usage Metrics Rules
- Metrics should be updated after every stage by the Orchestrator.
- Estimated cost may be approximate if exact billing data is unavailable.

---

## 6. Approval Rules
- `human_feedback` tracks open feedback state.
- `human_approval` tracks final owner decision.

---

## 7. Notes
- `updated_at` must be refreshed whenever the job state changes.
- Approved assets should be preserved even if drafts are cleaned later.
