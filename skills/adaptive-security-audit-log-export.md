---
name: Export audit logs
description: Export Adaptive Security audit-log events for compliance evidence or SIEM ingestion.
api: openapi/adaptive-security-openapi.json
operations: [listAuditLogs, getAuditLog]
---

# Export audit logs

Use the read-only Adaptive API v2 to export audit-log activity.

## Auth
- Bearer token: `Authorization: Bearer YOUR_API_TOKEN`. Base URL: `https://api.adaptivesecurity.com`.

## Conventions
- Both operations are `GET`. `listAuditLogs` is cursor-paginated (`page_after` / `page_size`) and supports filters such as `actions`, `user_id`, and `start_date`/`end_date`. Timestamps are ISO 8601 UTC. Log `request_id` on errors; back off on `429`.

## Steps
1. `listAuditLogs` — page through audit events, filtering by `actions`, `user_id`, and date range as needed.
2. `getAuditLog` — fetch full detail for a specific event by `auditLogId` (including the acting admin).
3. Emit the records to your SIEM or compliance evidence store.

## Errors
See `errors/adaptive-security-problem-types.yml`.
