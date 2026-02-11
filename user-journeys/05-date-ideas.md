# 05. Date Ideas Journey

## Overview

Date Ideas helps users discover, save, schedule, and complete date activities with personalization and lightweight gamification.

## Current Implementation (Shippable V1)

**Last updated**: February 8, 2026

### UX in production

- `DateIdeasScreen` with 3 tabs:
  - `For You`
  - `Browse`
  - `Trending`
- Search + filters:
  - keyword
  - category
  - budget
  - city
  - indoor/outdoor/mixed
  - radius (when user/couple coordinates exist)
- Save/unsave from cards and detail sheet
- Schedule via calendar flow (`CreateEventScreen`) with source metadata
- Complete flow with rating + optional feedback
- Dedicated history screens:
  - `SavedDateIdeasScreen`
  - `CompletedDateIdeasScreen`
- Gamification widgets:
  - streaks
  - badges
  - monthly challenge

### Data + ranking flow

1. Client requests ideas through `DateIdeasRepository`.
2. Repository reads couple-specific ideas from `date_ideas` (if available).
3. If empty, repository reads global catalog from `date_ideas_catalog`.
4. Results are filtered and ranked client-side using user/couple signals.
5. If available, Cloud Function `recommendDateIdeas` server ranking is merged.

## Firestore Collections Used

### Catalog + recommendation inputs

- `date_ideas_catalog` (global read-only catalog for clients)
- `date_ideas` (optional couple-specific ideas)

### User actions

- `date_idea_saves`
- `date_idea_interactions`
- `date_idea_actions`

### Related domain collections

- `calendar_events` (scheduled dates)
- `users`, `couples` (preferences + coordinates used by ranking)

## Catalog Schema (Current)

```json
{
  "id": "string",
  "title": "string",
  "description": "string",
  "category": "adventure|romantic|cozy|cultural|outdoor|food|active|creative|entertainment",
  "budget": "free|low|medium|high",
  "duration": "short|medium|long|fullDay",
  "tags": ["string"],
  "location": "string|null",
  "city": "string|null",
  "region": "string|null",
  "indoor_outdoor": "indoor|outdoor|mixed|null",
  "season": ["spring|summer|fall|winter|all-season"],
  "price_range": "string|null",
  "latitude": "number|null",
  "longitude": "number|null",
  "rating": "number|null",
  "reviewCount": "number",
  "isActive": "boolean",
  "createdAt": "timestamp"
}
```

## Operations Model

- Global catalog seeding is backend-only.
- Seeding was executed as a one-time production operation on **February 8, 2026**.
- End users have no in-app seed/import tooling.
- Temporary seeding endpoint has been removed from deployed functions.

## Security Model

From `firestore.rules`:

- `date_ideas_catalog`: signed-in read only
- `date_idea_saves`: owner read/write
- `date_idea_interactions`: owner create/read, immutable
- `date_idea_actions`: owner create/read, immutable

## Files Involved

- `lib/screens/date_ideas_screen.dart`
- `lib/screens/date_ideas/saved_date_ideas_screen.dart`
- `lib/screens/date_ideas/completed_date_ideas_screen.dart`
- `lib/models/date_idea_model.dart`
- `lib/services/date_ideas_repository.dart`
- `functions/src/dateIdeas.ts`
- `functions/src/index.ts`
- `firestore.rules`
- `firestore.indexes.json`

## Next Milestones

1. Replace heuristic trending with event-aggregated metrics from backend.
2. Add admin-managed catalog tooling (create/edit/archive).
3. Add localization-aware candidate generation (language + country/city scope).
4. Introduce recommendation observability (coverage, CTR, save-rate, completion-rate).

---

**Next Journey**: [06. Subscription](06-subscription.md)
