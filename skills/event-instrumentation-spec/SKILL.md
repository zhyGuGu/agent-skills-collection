---
name: event-instrumentation-spec
description: Create an analytics event tracking spec that is consistent, privacy-aware, and testable, including event naming rules, required properties, QA steps, and a copy/paste tracking plan template.
---

# Event Instrumentation Spec

Use this skill to design or review product analytics instrumentation so that events are reliable, interpretable, and safe to collect.

## When to Use
- You are adding analytics to a new feature.
- Existing events are inconsistent (names/properties differ across platforms).
- You need a tracking plan that engineers, data, and product can all sign off on.

## Inputs
Ask for:
- Product surface(s): web/iOS/Android/Flutter.
- Analytics stack: Segment, GA, Amplitude, Snowplow, custom.
- Privacy constraints: PII policy, consent model, regions (GDPR/CPRA).
- The decision(s) events must support (funnels, retention, revenue, experiments).

## Workflow
1. Define measurement goals
   - State the questions to answer (not the events).
   - Define success metrics and leading indicators.
2. Establish naming and property rules
   - Consistent verb_noun naming (or a clear alternative).
   - Property types and allowed values.
   - Stable identifiers and join keys.
3. Design the event set
   - Keep it minimal: instrument decision points, not every UI click.
   - Define canonical events shared across platforms.
4. Add privacy guardrails
   - Explicitly list which fields are PII and how they are handled.
   - Ensure consent gating and deletion requests are supported.
5. Make it testable
   - Define QA steps and expected payloads.
   - Define backfill/rollout steps if changing existing event schemas.

## Outputs

### Tracking Plan Template
```md
# Tracking Plan: <feature>

## Goal
- Decision(s) supported:
- Primary metric(s):
- Secondary metric(s):

## Naming Rules
- Events: <verb>_<object> (e.g., view_pricing, submit_checkout)
- Properties: snake_case
- IDs: user_id (stable), session_id, device_id (if permitted)

## Events
| Event Name | When Fired | Required Properties | Optional Properties | Privacy Notes | Owner |
|---|---|---|---|---|---|
| <event> | <trigger> | <k:v> | <k:v> | <PII/consent> | <team> |

## QA
- How to verify locally:
- Sample payloads (expected):
- Monitoring after release (dashboards/alerts):

## Schema Changes
- Backward compatibility plan:
- Deprecation plan (if replacing old events):
```

## Differentiator
This skill treats tracking as an API: versionable schemas, explicit privacy constraints, and testable payload expectations rather than ad-hoc event lists.
