---
name: incident-postmortem-facilitator
description: Facilitate a blameless incident postmortem with a structured timeline, contributing factors analysis, and action item rubric, producing a copy/paste postmortem document.
---

# Incident Postmortem Facilitator

Use this skill to run a post-incident process that produces learning and concrete follow-ups, not just a narrative.

## When to Use
- After an outage, security incident, or severe degradation.
- When multiple teams contributed and context is fragmented.
- When you need consistent action item quality and follow-through.

## Inputs
Ask for:
- Incident start/end times and who detected it.
- Customer impact summary and affected systems.
- Key artifacts: dashboards, logs, alerts, deploys, tickets.
- What was changed during mitigation.

## Workflow
1. Establish a factual timeline
2. Identify contributing factors (technical + process)
3. Extract lessons and decide on action items
4. Define owners, deadlines, and verification

## Outputs

### Postmortem Template
```md
# Postmortem: <incident name>

## Summary
- Date:
- Severity:
- Duration:
- Customer impact:

## What Happened (Timeline)
| Time (UTC) | Event | Evidence/Link |
|---|---|---|
| <t> | <what> | <dashboard/log/pr> |

## Root Cause (as a chain)
1.
2.
3.

## Contributing Factors
- Technical:
- Process:
- Observability:
- On-call/coordination:

## What Went Well
-

## What Didn’t Go Well
-

## Action Items
| Action | Type (prevent/detect/respond) | Owner | Due | Verification |
|---|---|---|---|---|
| <item> | <type> | <name> | <date> | <test/monitor> |
```

## Risks
- Turning the postmortem into blame or speculation.
- Action items without verification criteria.
- No prioritization: many low-impact follow-ups instead of a few high-leverage ones.
