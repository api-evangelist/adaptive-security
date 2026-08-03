---
name: Report training-campaign compliance
description: Pull training-campaign completion and enrollment data from Adaptive Security to build a compliance report.
api: openapi/adaptive-security-openapi.json
operations: [listTrainingCampaigns, getTrainingCampaign, getTrainingCampaignEnrollments, listUsers]
---

# Report training-campaign compliance

Use the read-only Adaptive API v2 to report on security-awareness training compliance.

## Auth
- Bearer token: `Authorization: Bearer YOUR_API_TOKEN` (Admin portal → Settings → API Tokens).
- Base URL: `https://api.adaptivesecurity.com`.

## Conventions
- All operations are `GET`. Lists are cursor-paginated: pass `page_after` from the previous response and optional `page_size`; keep paging until `page_after` is empty.
- Timestamps are ISO 8601 UTC. On errors read `error_code`/`message` and log `request_id` (also the `X-Request-ID` header). Back off on `429`.

## Steps
1. `listTrainingCampaigns` — enumerate training campaigns; page through all results.
2. `getTrainingCampaign` — for a campaign of interest, fetch its details (`campaignId`).
3. `getTrainingCampaignEnrollments` — fetch enrollment/completion records (filter with `campaign_id`, `user_id`, `start_date`/`end_date` as needed); page through all.
4. `listUsers` — resolve `user_id`s to employee identity (email/name/status) for the report.
5. Join enrollments to users and summarize completion rates and overdue trainings.

## Errors
See `errors/adaptive-security-problem-types.yml` (INVALID_TOKEN 401, RESOURCE_NOT_FOUND 404, VALIDATION_ERROR 400, INTERNAL_SERVER_ERROR 500).
