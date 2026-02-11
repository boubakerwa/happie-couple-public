# App Privacy Labels (App Store Connect)

## Data used to provide core app functionality
- Contact info: email address (account sign-in and support).
- User content: diary entries, check-ins, relationship preferences, calendar events.
- Identifiers: user ID and couple ID for secure data isolation.
- Diagnostics: crash logs and basic performance telemetry (if Crashlytics enabled).

## Data linked to the user
- Account profile data and relationship data are linked to user accounts.

## Data not collected for tracking
- No cross-app tracking identifiers.
- No third-party ad tracking.

## In-app controls available
- Privacy policy and terms links in app settings.
- In-app account deletion from Privacy Settings.
- Data export request via privacy contact email.

## Pre-submission checklist
- Verify labels match actual SDK behavior (Firebase Auth/Firestore/Messaging/Storage).
- Verify no extra SDKs collect undeclared data.
- Reconfirm labels before each release if dependencies changed.
