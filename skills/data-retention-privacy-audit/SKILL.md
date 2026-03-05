---
name: data-retention-privacy-audit
description: A pragmatic workflow to map personal data, define retention/deletion rules, and implement a low-risk data cleanup plan, producing a copy/paste data map and retention schedule template.
---

# Data Retention & Privacy Audit

Use this skill to perform a lightweight privacy and data-retention audit that results in concrete engineering and policy actions.

## When to Use
- You are unsure what personal data you store and where.
- You need to reduce data risk/cost by deleting old data safely.
- You are preparing for a compliance review (GDPR/CPRA/SOC2-style expectations).

## Inputs
Ask for:
- Systems involved: DBs, warehouses, logs, analytics, backups.
- Regions/users covered and any consent model.
- Current deletion requests flow (if any).
- Business requirements for retention (tax, fraud, support).

## Workflow
1. Build a data map
   - What data, where it lives, how it flows, who has access.
2. Classify and minimize
   - Identify PII/sensitive fields.
   - Remove collection of fields that are not used.
3. Define retention rules
   - Per dataset/table/log stream: retain X days/months/years.
   - Define legal holds and exceptions.
4. Design deletion
   - User-request deletion (subject rights) and automatic expiration.
   - Consider derived data (aggregates, caches) and backups.
5. Implement safely
   - Dry-run and measure impact.
   - Roll out gradually with monitoring.

## Outputs

### Data Map Template
```md
| Data Element | Example | Classification | System | Storage Location | Access | Purpose | Retention | Deletion Method |
|---|---|---|---|---|---|---|---|---|
| email | a@b.com | PII | prod-db | users.email | app, support | login | 7y (account lifetime) | delete row on request |
| ip_address | 1.2.3.4 | PII | logs | nginx access logs | eng | security | 30d | log rotation |
| device_id | abc | identifier | analytics | events.device_id | data | attribution | 13m | delete by user_id mapping |
```

### Retention Schedule (Copy/Paste)
```text
Dataset: <name>
Owner: <team>
Classification: <public/internal/pii/sensitive>
Retention: <duration> (rationale: <why>)
Deletion trigger: <event/time>
Deletion mechanism: <sql/job/lifecycle>
Backups handling: <how long, how purged>
Verification: <how to prove deletion works>
```

## Risks
- Breaking product features that rely on historical data without realizing it.
- Deleting without a verification mechanism (no proof, no monitoring).
- Forgetting secondary stores (logs, caches, exports, analytics).
