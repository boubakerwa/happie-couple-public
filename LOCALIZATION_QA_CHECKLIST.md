# Localization & UX QA Checklist

## Scope
Primary user flow screens:
- Today
- Diary (list + add entry)
- Calendar
- Home navigation
- Profile (privacy/settings entry points)

## Device matrix
- iPhone 13/14 (compact width)
- iPhone 15 Pro Max (large width)
- Text scale: 100% and 130%

## Locale matrix
- English (`en`)
- German (`de`)
- French (`fr`)
- Italian (`it`)
- Arabic (`ar`, RTL)
- Spanish (`es`)

## Pass criteria
1. No clipped labels/buttons on primary screens.
2. No overflow or layout exceptions when navigating primary screens.
3. RTL direction is correct for Arabic and icons/spacing remain usable.
4. Navigation/tab labels remain understandable and aligned.
5. Legal/privacy/account deletion flows are reachable in all locales.

## Automation currently in repo
- Unit/widget tests in `test/`
- Integration smoke tests in `integration_test/`
- CI quality gate workflow in `.github/workflows/quality-gate.yml`
- Crash-free release gate script in `tool/release_gate.dart`
