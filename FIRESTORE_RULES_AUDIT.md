# Firestore Rules Audit

Date: 2026-02-09

## High-risk findings addressed
- Tightened user profile reads to owner + active linking-code lookup only.
- Tightened shared diary reads to couple membership only.
- Tightened calendar CRUD to couple membership with immutable ownership fields.
- Enabled owner deletes for date-idea interaction/action records to support account deletion.

## Collections reviewed
- `users`
- `couples`
- `notes`
- `coaching_agendas`
- `notifications`
- `date_ideas*` collections
- `calendar_events`
- `content_items` and `content_user_state`

## Security intent
- Least privilege by default.
- Couple isolation across all shared data.
- User-owned writes only.
- Backend-admin deletion path for complete account removal.

## Validation guidance
1. Run Firestore emulator tests for cross-couple isolation.
2. Verify partner linking still works with active linking code flow.
3. Verify account deletion path removes user-owned records and unlinks partner.
4. Verify calendar and shared-diary reads/writes fail for non-members.
