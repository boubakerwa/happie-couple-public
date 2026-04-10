Happie Couple - Relationship Growth App

A comprehensive Flutter app designed for couples to strengthen their relationships through daily notes, weekly coaching sessions, and personalized insights.

🚀 Features

👥 Couples-Based Authentication

Secure partner linking system with unique codes
Individual user profiles with shared couple data
Privacy controls for personal and shared content
📝 Daily Note-Taking System

Categorize experiences as positive or negative
Mood tracking with 5-level emotional scale
Tag system for organizing thoughts
Privacy options (private vs shared with partner)
🔥 Tension Card Loop (Capture Now, Process Later)

Fast capture flow for heated moments
Cooling window before decisions
Pre-meeting review queue
3-second hold actions: Forgive & Release or Bring to Agenda
Full-screen forgiveness ceremony with haptic feedback and CTA
Privacy-safe partner notification on forgiveness
📋 Weekly Coaching Agenda

Automated analysis of weekly notes
AI-generated discussion topics
Pattern recognition and insights
Meeting scheduling and progress tracking
🔔 Smart Notifications

Personalized relationship tips
Daily reminder notifications
Partner activity updates
Partner forgiveness gesture updates (without card content)
Weekly meeting reminders
📊 Progress Tracking

Relationship insights dashboard
Mood trends and patterns
Growth metrics and milestones
Export functionality for meeting agendas
🔐 Privacy & Security

End-to-end encrypted data storage
Granular privacy controls
Secure partner data synchronization
No third-party data sharing
🏗️ Architecture

Technology Stack

Frontend: Flutter 3.0+
Backend: Firebase (Auth, Firestore, Cloud Messaging, Storage)
State Management: Provider pattern
UI Framework: Material 3 Design
Platform: iOS (with Android-ready codebase)
Project Structure

lib/
├── constants/          # App themes, colors, strings
├── models/            # Data models (User, Couple, Note, etc.)
├── screens/           # UI screens organized by feature
│   ├── onboarding/    # Welcome, signup, profile setup
│   ├── home/          # Main navigation
│   ├── notes/         # Note creation and viewing
│   ├── tension_cards/ # Capture/review/forgiveness loop
│   ├── date_ideas/    # Date ideas and match mode
│   ├── calendar/      # Shared events and reminders
│   └── profile/       # User and couple settings
├── services/          # Business logic and API calls
│   ├── auth_service.dart
│   ├── firestore_service.dart
│   └── notification_service.dart
├── widgets/           # Reusable UI components
└── utils/             # Helper functions and utilities
Database Schema

Users Collection

{
  "id": "user_id",
  "email": "user@example.com",
  "name": "User Name",
  "partnerId": "partner_user_id",
  "coupleId": "couple_id",
  "preferences": {},
  "isProfileComplete": true,
  "createdAt": "timestamp",
  "updatedAt": "timestamp"
}
Couples Collection

{
  "id": "couple_id",
  "user1Id": "first_user_id",
  "user2Id": "second_user_id",
  "coupleName": "Our Relationship",
  "relationshipStartDate": "timestamp",
  "linkingCode": "ABC123XY",
  "isActive": true,
  "sharedPreferences": {},
  "meetingSchedule": "weekly_sunday_19:00"
}
Notes Collection

{
  "id": "note_id",
  "userId": "author_id",
  "coupleId": "couple_id",
  "title": "Note Title",
  "content": "Note content...",
  "type": "positive|negative",
  "moodLevel": "veryGood|good|neutral|bad|veryBad",
  "privacyLevel": "shared|private",
  "tags": ["communication", "date night"],
  "noteDate": "timestamp",
  "createdAt": "timestamp"
}
🛠️ Setup Instructions

Prerequisites

Flutter SDK (3.0+)
Dart SDK
iOS development environment (Xcode, CocoaPods)
Firebase project
Installation

Clone the repository
git clone <repository-url>
cd happie-couple
Install dependencies
flutter pub get
cd ios && pod install && cd ..
Firebase Setup

Create a Firebase project
Add iOS app with bundle ID
Download and place GoogleService-Info.plist in ios/Runner/
Enable Authentication, Firestore, Cloud Messaging
Run the app

flutter run
🧪 Testing

Unit Tests

flutter test
Integration Tests

flutter drive --target=test_driver/app.dart
Manual Testing Checklist

 User registration and authentication
 Partner linking with codes
 Note creation and privacy controls
 Weekly agenda generation
 Notification delivery
 Data synchronization between partners
🚀 Deployment

Refer to DEPLOYMENT_GUIDE.md for complete iOS App Store deployment instructions.

Quick Build Commands

# Development
flutter run

# Release build
flutter build ios --release

# App Store archive (in Xcode)
Product → Archive
✅ iOS App Store Submission Checklist

Use this comprehensive checklist to ensure your app is ready for App Store submission.

Phase 1: Pre-Development Setup

 Apple Developer Account

 Enroll in Apple Developer Program ($99/year)
 Verify account and accept agreements
 Set up two-factor authentication
 App Store Connect Setup

 Create app record with bundle ID: com.happiecouple.happieCouple
 Fill in app information (name, subtitle, category)
 Set primary language (English/German)
 Choose age rating: 12+ (relationship content)
Phase 2: Firebase & Backend Configuration

 Firebase Project Setup

 Create Firebase project "Happie Couple"
 Add iOS app with correct bundle ID
 Download GoogleService-Info.plist → place in ios/Runner/
 Enable Authentication (Email/Password)
 Create Firestore database (start in test mode)
 Enable Cloud Messaging
 Enable Storage (for profile photos)
 Firestore Security Rules

 Deploy production security rules (see firestore.rules)
 Test rules with Firebase Emulator
 Verify user data isolation
 Test partner data sharing permissions
 Install Dependencies

flutter pub get
cd ios && pod install --repo-update && cd ..
Phase 3: Legal & Compliance

 Privacy Policy & Terms

 Review and customize docs/PRIVACY_POLICY.md
 Add your German business address
 Review and customize docs/TERMS_OF_SERVICE.md
 Update company registration details
 Legal Docs Hosting (already configured)

 Verify production legal URLs are still reachable
 Verify Privacy/Terms render correctly on iOS Safari
 App Store Connect Legal Links

 Add Privacy Policy URL
 Add Terms of Service URL (optional but recommended)
 Add Support URL
Phase 4: Code & Configuration

 iOS Configuration

 Update ios/Runner/Info.plist with all permissions (✅ Done)
 Set minimum iOS version to 13.0 in Podfile (✅ Done)
 Configure code signing in Xcode
 Add Push Notifications capability
 Verify bundle ID matches everywhere
 App Icons & Assets

 Verify all app icon sizes present (1024x1024 required)
 Check launch screen displays correctly
 Test on multiple device sizes (iPhone SE, 14, 15 Pro Max)
 Safety Features (✅ Done)

 Therapeutic disclaimer on welcome screen
 Crisis resources accessible from app
 "Not a substitute for therapy" warnings
 Link to Help & Support screen
 Localization (Optional - Future)

 Add German translations if targeting German market
 Test language switching
Phase 5: In-App Purchases (IAP)

 App Store Connect IAP Setup

 Create subscription group "Happie Couple Premium"
 Add Monthly subscription (€9.99/month)
 Add Annual subscription (€59.99/year)
 Add Lifetime purchase (€149.99 one-time)
 Configure subscription benefits description
 Add all required IAP metadata and screenshots
 Integrate IAP SDK

 Choose provider: RevenueCat (recommended) or StoreKit
 Add purchases_flutter to pubspec.yaml
 Replace mock SubscriptionService with real implementation
 Test purchases in sandbox mode
 Handle subscription restoration
 Test subscription expiration
 Sandbox Testing

 Create sandbox test users in App Store Connect
 Test all subscription tiers
 Test subscription cancellation
 Test family sharing (if applicable)
Phase 6: Testing & Quality Assurance

 Functional Testing

 Complete onboarding flow (sign up → profile → partner linking)
 Create and view notes (private & shared)
 Test weekly coaching agenda generation
 Verify AI insights display
 Test notifications (local & push)
 Partner unlinking and re-linking
 Account deletion and data removal
 Performance Testing

 App launches in < 3 seconds
 No memory leaks during extended use
 Smooth animations (60 FPS)
 Test with slow network connection
 Test offline mode functionality
 Device Testing

 iPhone SE (smallest screen)
 iPhone 14/15 (standard size)
 iPhone 15 Pro Max (largest screen)
 iOS 13.0 (minimum version)
 Latest iOS version
 Edge Cases

 No internet connection
 Firebase service unavailable
 Invalid partner linking codes
 Simultaneous edits by both partners
 Background app refresh
Phase 7: App Store Assets

 Screenshots (Required Sizes)

 6.7" Display (iPhone 15 Pro Max): 1290 x 2796 pixels
 Welcome/Onboarding screen
 Daily check-in interface
 Note viewing screen
 Weekly coaching agenda
 AI insights screen
 Profile/settings screen
 6.5" Display (iPhone 14 Plus): 1284 x 2778 pixels (optional)
 5.5" Display (iPhone 8 Plus): 1242 x 2208 pixels (optional)
 App Preview Video (Optional but recommended)

 Record 15-30 second demo
 Show key features: notes, agenda, insights
 Upload in correct format (H.264, .mov)
 App Store Metadata

 App Name: "Happie Couple" (30 char max)
 Subtitle: "Relationship Growth Together" (30 char max)
 Keywords: relationship, couples, communication, coaching, love, diary, notes, therapy, connection (100 char max)
 Description (4000 char max) - use content from DEPLOYMENT_GUIDE
 Promotional text (170 char max)
 What's New (version 1.0.0)
 App Information

 Primary Category: Lifestyle
 Secondary Category: Health & Fitness (optional)
 Age Rating: 12+ (Infrequent/Mild: Sexual Content & Nudity - relationship topics)
 Copyright: "© 2026 Happie Couple"
Phase 8: Build & Upload

 Final Build Preparation

 Update version in pubspec.yaml: version: 1.0.0+1
 Clean build artifacts:
flutter clean
rm -rf ios/Pods ios/Podfile.lock
flutter pub get
cd ios && pod install && cd ..
 Archive & Upload

 Open ios/Runner.xcworkspace in Xcode (NOT .xcodeproj)
 Select "Any iOS Device (arm64)" as build target
 Product → Archive
 Wait for archive to complete (5-10 minutes)
 Window → Organizer → Select archive
 Click "Distribute App" → "App Store Connect"
 Upload to App Store Connect
 Wait for processing (15-60 minutes)
Phase 9: TestFlight (Optional but Recommended)

 Internal Testing

 Add internal testers in App Store Connect
 Distribute build via TestFlight
 Collect feedback from 5-10 beta users
 Fix any critical bugs found
 External Testing (Optional)

 Submit for Beta App Review (2-3 days)
 Invite external testers (up to 10,000)
 Gather feedback for 1-2 weeks
 Iterate on feedback
Phase 10: App Review Submission

 Pre-Submission Checklist

 All metadata complete
 Screenshots uploaded for all required sizes
 Privacy Policy URL accessible
 Support URL accessible
 App build successfully uploaded and processed
 In-app purchases configured and ready
 App Review Information

 Provide demo account credentials (for Apple reviewers):
Email: reviewer@happiecouple.com (create test account)
Password: [Strong password - share securely]
Partner linking code: [Provide pre-generated code]
 Add notes to reviewer explaining partner linking feature
 Mention therapeutic disclaimers prominently displayed
 Submit for Review

 Select build version
 Check all compliance boxes
 Submit to App Review
 Expect review time: 1-7 days (average 24-48 hours)
Phase 11: Post-Submission

 Monitor Review Status

 Check App Store Connect daily
 Respond to Apple questions within 24 hours
 Be prepared to fix critical issues
 If Rejected

 Read rejection reason carefully
 Fix issues promptly
 Respond in Resolution Center
 Resubmit with explanations
 If Approved

 🎉 Celebrate!
 Set release date (immediate or scheduled)
 Prepare launch marketing materials
 Monitor user reviews and ratings
 Set up crash reporting alerts
Phase 12: Launch Day

 Release Preparation

 Verify app is live on App Store
 Test download and installation
 Check all features work in production
 Monitoring

 Watch Firebase console for user signups
 Monitor Crashlytics for errors
 Check in-app purchase transactions
 Respond to user reviews
 Marketing (Optional)

 Share on social media
 Email announcement to waitlist
 Press release to tech blogs
 Product Hunt launch
📊 Estimated Timeline

Phase	Duration	Critical Path
Firebase Setup	2-4 hours	✅ Yes
Legal Docs Hosting	1 hour	✅ Yes
Code Configuration	4-6 hours	✅ Yes
IAP Implementation	1-2 days	✅ Yes
Testing	2-3 days	Parallel
Screenshots & Assets	4-8 hours	Parallel
Build & Upload	2-4 hours	✅ Yes
TestFlight (optional)	1-2 weeks	No
App Review	1-7 days	✅ Yes
Total (Fast Track)	1-2 weeks	-
Total (with TestFlight)	3-4 weeks	-
🚨 Common Rejection Reasons & How to Avoid

Incomplete App Information

✅ Fill out ALL fields in App Store Connect
✅ Provide demo account with full access
Privacy Policy Missing or Broken

✅ Test legal document URLs before submission
✅ Ensure HTTPS is enabled on your hosting provider
In-App Purchases Not Working

✅ Test in sandbox mode extensively
✅ Provide clear subscription benefits description
Misleading Health Claims

✅ Include therapeutic disclaimers throughout app
✅ Never claim to "treat" or "cure" relationship problems
Crashes During Review

✅ Test on all supported iOS versions
✅ Handle all error cases gracefully
🔗 Quick Reference Links

Legal Documents: docs/
Product Audit + Recenter Plan: docs/PRODUCT_AUDIT_AND_RECENTER_PLAN.md
Deployment Guide: DEPLOYMENT_GUIDE.md
App Constants: lib/constants/app_constants.dart
Help & Support Screen: lib/screens/support/help_support_screen.dart
📱 Key User Flows

1. Onboarding Flow

Welcome screen with feature overview
Account creation (email/password)
Profile setup (name, relationship start date, preferences)
Partner linking (generate/enter code)
Content quiz and couple linking (or proceed without linking)
2. Daily Usage Flow

Open app to notes screen
Create daily note with mood and tags
Choose privacy level (shared/private)
View partner's shared notes
Receive personalized tips via notifications
3. Weekly Coaching Flow

Capture tension cards during the week
Review cards before meeting (after cooling)
Hold to forgive/release what can be let go
Hold to bring constructive cards into agenda
Use agenda during couple's meeting
Mark items as completed
🔧 Configuration

Environment Variables

Create .env file with:

FIREBASE_PROJECT_ID=your-project-id
FIREBASE_API_KEY=your-api-key
Notification Categories

dailyReminder: Daily note-taking prompts
weeklyMeeting: Coaching session reminders
relationshipTip: Personalized advice
partnerNote: Partner activity notifications
partnerForgiveness: Partner chose forgiveness today
encouragement: Milestone celebrations
customReminder: User-defined reminders
memoryNudge: Weekly memory/insight nudges
eventReminder: Calendar event reminders
🤝 Contributing

Code Style

Follow Flutter/Dart style guidelines
Use meaningful variable names
Comment complex business logic
Maintain consistent file structure
Commit Guidelines

Use conventional commit format
Include clear descriptions
Reference issue numbers when applicable
Pull Request Process

Fork the repository
Create feature branch
Make changes with tests
Update documentation
Submit pull request
🛡️ Privacy & Security

Data Protection

All user data encrypted in transit and at rest
Minimal data collection principle
No tracking or analytics without consent
Regular security audits
Privacy Features

Private notes never shared
Granular sharing controls
Easy account unlinking
Complete data deletion option
📈 Analytics & Monitoring

Key Metrics

Daily/Weekly active users
Note creation frequency
Agenda generation usage
Partner linking success rate
User retention rates
Error Monitoring

Firebase Crashlytics integration
Real-time error tracking
Performance monitoring
User feedback collection
🆘 Troubleshooting

Common Issues

Build Fails on iOS

flutter clean
rm -rf ios/Pods ios/Podfile.lock
flutter pub get && cd ios && pod install && cd ..
Firebase Connection Issues

Verify GoogleService-Info.plist location
Check Firebase project settings
Ensure all required services enabled
Partner Linking Not Working

Check Firestore security rules
Verify code expiration logic
Test user permissions
📞 Support

Bug Reports

Create detailed issues with:

Device/OS information
Steps to reproduce
Expected vs actual behavior
Screenshots if applicable
Feature Requests

Use the feature request template with:

Clear problem statement
Proposed solution
User impact assessment
Implementation considerations
📄 License

This project is proprietary software. All rights reserved.

🙏 Acknowledgments

Flutter team for the amazing framework
Firebase for backend services
Material Design for UI guidelines
Beta testers for valuable feedback
Version: 1.0.0 Last Updated: February 2026 Minimum iOS Version: 13.0 Flutter Version: 3.0+ Business Location: Germany

For detailed deployment instructions, see DEPLOYMENT_GUIDE.md