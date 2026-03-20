# Handoff Message Schema

## 1. Structured Message Format
Every agent must leave a "handoff" message in the `threads/[job_id]_thread.json` when transitioning to the next stage.

```json
{
  "agent": "agent_name",
  "timestamp": "ISO-8601",
  "type": "handoff | review | issue | approval | rejection | note",
  "summary": "Brief explanation of the work done in this stage.",
  "risks": [
    "Identified risks for the next agent or the final piece."
  ],
  "decisions": [
    "Key strategic or creative choices made."
  ],
  "requests_to_next_agent": [
    "Specific instructions or focus points for the next agent."
  ],
  "status_change": "The new job status after this handoff.""related_files": [],
"related_assets": [],
"token_usage": {
  "input_tokens": 0,
  "output_tokens": 0,
  "total_tokens": 0
},
"estimated_cost_usd": 0
}
```

---

## 2. Message Types
- **handoff:** Standard completion and passing of control.
- **review:** Feedback from the Reviewer or Human.
- **issue:** Blocker or significant problem encountered.
- **approval:** Positive outcome in a verification or final step.
- **rejection:** Work sent back for rework.
- **note:** General contextual update.

---

## 3. Required Fields
- **Summary:** Must be concise (1–3 sentences).
- **Requests:** Must be actionable and specific.
- **Risks:** Must be realistic and grounded in the piece's context.
