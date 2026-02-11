---
title: Happie Couple - User Journeys Documentation
layout: default
description: Happie Couple - User Journeys Documentation for Happie Couple.
---

# Happie Couple - User Journeys Documentation

This folder contains detailed documentation of all user journeys in the Happie Couple app.

## 📱 App Structure

The production app (main.dart) has **4 main tabs**:

1. **Notes** - Daily relationship moments tracking
2. **Agenda** - Weekly AI-generated coaching topics
3. **Date Ideas** - Personalized date suggestions
4. **Profile** - Settings, subscription, partner linking

---

## 🗺️ User Journeys

### Core Journeys
- [01. Onboarding & Sign Up](01-onboarding.md) - First-time user experience
- [02. Partner Linking](02-partner-linking.md) - Connecting with your partner
- [03. Daily Notes](03-daily-notes.md) - Adding and managing relationship notes
- [04. Weekly Coaching](04-weekly-coaching.md) - Generating and using coaching agendas
- [05. Date Ideas](05-date-ideas.md) - Finding and saving date ideas

### Monetization & Engagement
- [06. Subscription Journey](06-subscription.md) - Free trial to Premium upgrade
- [07. Notifications](07-notifications.md) - Setting up reminders and alerts

### Support & Settings
- [08. Profile Management](08-profile.md) - Editing profile and preferences
- [09. Help & Support](09-help-support.md) - Accessing crisis resources

---

## 🎯 Target User Personas

### Primary Persona: Sarah & James
- **Age**: 28-35
- **Relationship**: Married 2-5 years or long-term relationship
- **Tech savviness**: Moderate (comfortable with apps)
- **Goal**: Improve communication, maintain connection
- **Pain point**: Busy schedules, falling into routines

### Secondary Persona: Emma & Alex
- **Age**: 24-30
- **Relationship**: Dating seriously (1-2 years)
- **Tech savviness**: High (early adopters)
- **Goal**: Build strong foundation, learn relationship skills
- **Pain point**: First serious relationship, need guidance

---

## 📊 User Flow Summary

```
Welcome Screen
    ↓
Sign Up → Email Verification → Profile Setup
    ↓
[Freemium Decision Point]
    ├─→ Start Free Trial (7 days) → Premium Features
    └─→ Continue Free → Limited Features
    ↓
Home Screen (4 tabs)
    ├─→ Notes Tab (Add daily notes)
    ├─→ Agenda Tab (Weekly coaching)
    ├─→ Date Ideas Tab (Browse ideas)
    └─→ Profile Tab (Settings & subscription)
    ↓
[Partner Linking - Optional]
    ├─→ Generate linking code
    └─→ Enter partner's code
    ↓
Ongoing Usage
    ├─→ Daily: Add notes, get reminders
    ├─→ Weekly: Generate agenda, have meeting
    └─→ As needed: Browse date ideas, adjust settings
```

---

## 🚀 Success Metrics

### Onboarding Success
- ✅ User completes sign up
- ✅ User adds first note (within 24 hours)
- ✅ User links with partner (within 7 days)

### Engagement Metrics
- ✅ Daily active users (DAU)
- ✅ Notes added per week (target: 3+)
- ✅ Agendas generated per month (target: 4)
- ✅ Date ideas bookmarked (target: 2+ per month)

### Monetization Metrics
- ✅ Free trial conversion rate (target: 20%)
- ✅ Monthly subscription retention (target: 85%)
- ✅ Premium feature usage
- ✅ Lifetime value (LTV)

---

## 🎨 Design Principles

1. **Simplicity First** - Clear, uncluttered interface
2. **Emotional Safety** - Supportive tone, crisis resources accessible
3. **Privacy-Focused** - Private notes, partner-only sharing
4. **Actionable Insights** - Coaching that leads to conversations
5. **Celebration** - Acknowledge progress and milestones

---

## 📱 Screen Inventory

### Onboarding Screens (6)
- WelcomeScreen
- SignUpScreen
- SignInScreen
- CoupleLinkingScreen
- ProfileSetupScreen
- HelpSupportScreen

### Main App Screens (4 tabs + sub-screens)
- **NotesScreen** → AddNoteScreen
- **AgendaScreen** → AgendaDetailScreen
- **DateIdeasScreen** (3 tabs: For You, Browse, Trending)
- **ProfileScreen** → PaywallScreen, NotificationsScreen

### Utility Screens (2)
- SplashScreen
- LoadingOverlay (widget)

---

## 🔄 State Management

- **AuthService** - User authentication & partner linking
- **FirestoreService** - Data operations (notes, agendas)
- **SubscriptionService** - Premium status & features
- **NotificationService** - Push notifications & reminders

All services use **Provider** for state management.

---

## 📝 Next Steps

Read each journey document for detailed:
- Step-by-step user flows
- Screen transitions
- Error states & edge cases
- Success criteria
- Implementation notes

---

**Last Updated**: 2026-02-02
**Version**: 1.0 (MVP+)
