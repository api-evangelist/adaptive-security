---
name: Report phishing-simulation results
description: Pull phishing-campaign, simulation, and enrollment data from Adaptive Security to report on simulated-attack outcomes.
api: openapi/adaptive-security-openapi.json
operations: [listPhishingCampaigns, getPhishingCampaign, listCampaignSimulations, getSimulation, getPhishingEnrollments]
---

# Report phishing-simulation results

Use the read-only Adaptive API v2 to report on phishing-simulation performance.

## Auth
- Bearer token: `Authorization: Bearer YOUR_API_TOKEN`. Base URL: `https://api.adaptivesecurity.com`.

## Conventions
- All `GET`. Cursor pagination via `page_after` / `page_size`. ISO 8601 UTC timestamps. Log `request_id` on errors; back off on `429`.

## Steps
1. `listPhishingCampaigns` — enumerate phishing campaigns; page through all.
2. `getPhishingCampaign` — fetch a campaign's details by `campaignId`.
3. `listCampaignSimulations` — list the simulations run for that campaign (`campaignId`).
4. `getSimulation` — fetch execution details for a specific simulation (`simulationId`).
5. `getPhishingEnrollments` — fetch per-user enrollment/outcome records (filter with `campaign_id`, `simulation_id`, `user_id`); page through all.
6. Summarize click/report/failure rates and identify at-risk users.

## Errors
See `errors/adaptive-security-problem-types.yml`.
