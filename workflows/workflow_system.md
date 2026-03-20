# Workflow System

## 1. Overall Workflow Sequence
The content production pipeline follows a structured, linear-but-recursive sequence:

1. **Job Initialization:** Human or Orchestrator creates a new Content Brief.
2. **Strategy Phase:** Strategist builds the Strategic Post Plan.
3. **Research Phase:** Researcher validates and expands the plan with NotebookLM research.
4. **Design Phase:** Designer selects the format and structures the visual/textual architecture.
5. **Asset Production Phase (If Needed):**
- If the Designer requires generated visuals, create image briefs and produce assets.
- Store drafts in `assets/[job_id]/generated/`.
- After validation, move approved assets to `assets/[job_id]/approved/`.
6. **Copywriting Phase:** Copywriter writes the final LinkedIn-ready text.
7. **Production Phase:** Creative Producer assembles the final piece (HTML/PDF) and generates a validation preview.
8. **Review Phase:** Reviewer audits the entire output (including the final produced piece) against the Brand System.
9. **Final Decision:**
   - **If Approved:** Send to Human for final sign-off.
   - **If Approved with Adjustments:** Responsible agent fixes the issue → Reviewer re-audits.
   - **If Rejected:** Route back to the agent responsible for the failure (Strategist, Researcher, Designer, Copywriter, or Producer).
10. **Human Approval:** Human approves or requests changes.
11. **Archive:** Final package is saved in `memory/archived_jobs/`.

---

## 2. Routing & Rework Logic
The Reviewer is the primary router for rework:

| Failure Type | Target Agent | Rework Trigger |
| :--- | :--- | :--- |
| Bad Theme / Pillar | **Strategist** | Rejected by Reviewer or Human |
| Weak Research / Hallucination | **Researcher** | Rejected by Reviewer or Human |
| Poor Format / Structure | **Designer** | Rejected by Reviewer or Human |
| Generic Copy / Weak Hook | **Copywriter** | Rejected by Reviewer or Human |
| Broken Assets / Layout Errors | **Producer** | Rejected by Reviewer or Human |

---

## 3. Human Approval Step
- Human receives the final package (Dossier + Design Plan + Copy + Review).
- Human can:
  - **Approve:** Move to active publishing.
  - **Request Changes:** Orchestrator routes back to the relevant agent.
  - **Cancel:** Archive the job as "Cancelled".
