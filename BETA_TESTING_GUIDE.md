# Beta Testing Guide for Happie Couple

## Overview

This guide outlines the beta testing process for Happie Couple before public launch.

## Beta Testing Goals

1. **Validate Core Features**: Ensure all features work as expected
2. **Identify Bugs**: Find and fix critical issues before launch
3. **Gather Feedback**: Understand user experience and pain points
4. **Test Partner Linking**: Verify sync between partners works flawlessly
5. **Validate Subscriptions**: Ensure payment flow works correctly
6. **Performance Testing**: Check app performance on various devices

## Beta Testing Phases

### Phase 1: Internal Alpha (1 week)
**Participants**: Team members and close friends (5-10 couples)

**Goals**:
- Test basic functionality
- Identify critical bugs
- Verify partner linking works
- Test on iOS and Android

**Checklist**:
- [ ] Account creation works
- [ ] Partner linking succeeds
- [ ] Daily check-ins save correctly
- [ ] Weekly meetings function properly
- [ ] AI insights generate
- [ ] Date ideas load
- [ ] Achievements unlock
- [ ] Push notifications deliver
- [ ] Subscription purchase works (sandbox)

### Phase 2: Closed Beta (2-3 weeks)
**Participants**: 20-30 couples recruited via email, social media

**Goals**:
- Test with real users
- Gather detailed feedback
- Identify edge cases
- Test different usage patterns

**Distribution**:
- **iOS**: TestFlight (up to 100 users)
- **Android**: Google Play Internal Testing (up to 100 users)

**Metrics to Track**:
- Daily active users
- Check-in completion rate
- Meeting creation rate
- Partner linking success rate
- Crash rate
- Session duration
- Feature usage

### Phase 3: Open Beta (2-4 weeks)
**Participants**: 100-500 couples (anyone who signs up)

**Goals**:
- Stress test infrastructure
- Gather diverse feedback
- Build early user base
- Generate testimonials

**Distribution**:
- **iOS**: TestFlight (public link)
- **Android**: Google Play Open Beta

## TestFlight Setup (iOS)

### Prerequisites
1. Apple Developer Account ($99/year)
2. App uploaded to App Store Connect
3. Compliance information completed

### Steps
1. **Build & Upload**
   ```bash
   # Increment build number
   # Archive app in Xcode
   # Upload to App Store Connect
   ```

2. **TestFlight Configuration**
   - Add app description
   - Add beta test information
   - Set up tester groups
   - Configure automatic distribution

3. **Invite Testers**
   - Internal testers: Add via email (Apple IDs)
   - External testers: Generate public link or email invites
   - Max 10,000 external testers

4. **Provide Test Information**
   ```
   What to Test:
   - Create account and link with partner
   - Complete 3 daily check-ins
   - Schedule and complete a weekly meeting
   - Explore AI insights after 3 check-ins
   - Try the date idea match mode
   - Report any bugs or issues

   Focus Areas:
   - Does partner linking work smoothly?
   - Are insights helpful and accurate?
   - Is the UI intuitive?
   - Any features confusing or missing?
   ```

## Google Play Beta Setup (Android)

### Prerequisites
1. Google Play Developer Account ($25 one-time)
2. App bundle uploaded
3. Store listing created

### Steps
1. **Create Release**
   ```bash
   # Build app bundle
   flutter build appbundle --release
   ```

2. **Upload to Internal Testing Track**
   - Go to Google Play Console
   - Select app > Testing > Internal testing
   - Create new release
   - Upload AAB file
   - Add release notes

3. **Configure Testers**
   - Create email list
   - Add testers to track
   - Testers receive email invitation

4. **Progress to Closed/Open Beta**
   - Promote from Internal to Closed
   - Then to Open Beta when ready
   - Each track has different limits and requirements

## Feedback Collection

### In-App Feedback
Create feedback form accessible via:
- Settings > Beta Feedback
- Shake gesture (debug builds)
- Help button throughout app

**Collect**:
- Rating (1-5 stars)
- Feature being used
- Description of issue/feedback
- Device info (auto-collected)
- Screenshots (optional)

### External Surveys
**Tools**: Google Forms, Typeform, SurveyMonkey

**Questions**:
1. How easy was it to set up your account? (1-5)
2. How smooth was the partner linking process? (1-5)
3. Which features do you use most? (checkboxes)
4. Which features are confusing or need improvement? (open)
5. How likely are you to recommend Happie Couple? (NPS: 0-10)
6. What features are you most excited about? (open)
7. What features are missing? (open)
8. Would you pay for Premium? If so, what price? (pricing sensitivity)
9. Any bugs or issues encountered? (open)
10. Additional comments (open)

### Weekly Check-ins
Send weekly email to beta testers:
- Thank them for participation
- Share what was fixed/improved
- Request specific feedback on new features
- Encourage continued usage

## Bug Tracking

### Priority Levels
**P0 - Critical**: App crashes, data loss, security issues
- Fix immediately, hot patch if needed

**P1 - High**: Core features broken, major bugs
- Fix before moving to next beta phase

**P2 - Medium**: Non-critical bugs, minor issues
- Fix before public launch

**P3 - Low**: Nice-to-have improvements, edge cases
- Can defer to post-launch

### Bug Report Template
```
Title: [Brief description]
Priority: [P0/P1/P2/P3]
Platform: [iOS/Android]
Device: [iPhone 14, Pixel 7, etc.]
OS Version: [iOS 17.2, Android 14]
App Version: [1.0.0 (123)]

Steps to Reproduce:
1. Step one
2. Step two
3. Step three

Expected Behavior:
[What should happen]

Actual Behavior:
[What actually happens]

Screenshots/Videos:
[Attach if available]

Additional Context:
[Any other relevant information]
```

## Success Criteria

Before moving to public launch, ensure:

### Technical
- [ ] Crash rate < 0.1%
- [ ] ANR rate < 0.1% (Android)
- [ ] Average session length > 5 minutes
- [ ] Partner linking success rate > 95%
- [ ] Check-in save success rate > 99%

### User Satisfaction
- [ ] Average rating > 4.0/5.0
- [ ] NPS (Net Promoter Score) > 40
- [ ] At least 80% would recommend to friends
- [ ] No critical (P0) bugs
- [ ] All high priority (P1) bugs fixed

### Feature Validation
- [ ] Users complete multiple check-ins (retention)
- [ ] Partners successfully link accounts
- [ ] AI insights are viewed and appreciated
- [ ] Weekly meetings are scheduled and completed
- [ ] At least 50% engagement with date ideas

## Communication

### Beta Tester Welcome Email
```
Subject: Welcome to Happie Couple Beta! 🎉

Hi [Name],

Thank you for joining the Happie Couple beta program! We're excited to have you help shape the future of relationship wellness.

GET STARTED:
1. Download the app: [TestFlight/Play Store link]
2. Create your account
3. Link with your partner using a sharing code
4. Complete your first check-in together

WHAT TO FOCUS ON:
- Test partner linking (does it work smoothly?)
- Try daily check-ins for at least 3 days
- Schedule a weekly meeting
- Explore the AI insights feature
- Report any bugs or confusing moments

GIVE FEEDBACK:
- In-app: Settings > Beta Feedback
- Email: beta@happiecouple.app
- Survey: [link to survey]

We'll send updates weekly about what we're improving.

Thanks for being part of the journey!

The Happie Couple Team
```

### Update Notifications
Send when:
- New features added
- Major bugs fixed
- Moving to next beta phase
- Seeking specific feedback

## Post-Beta Launch Checklist

Before public launch:
- [ ] All P0 and P1 bugs fixed
- [ ] Beta feedback incorporated
- [ ] App Store listings complete (both platforms)
- [ ] Screenshots finalized
- [ ] Privacy policy and terms live
- [ ] Support email active
- [ ] Analytics and crashlytics configured
- [ ] Subscription pricing confirmed
- [ ] Marketing materials ready
- [ ] Press kit prepared
- [ ] Launch date set
- [ ] App Store review submitted
- [ ] Beta testers thanked and offered discount

## Resources

- **TestFlight**: https://developer.apple.com/testflight/
- **Google Play Beta**: https://support.google.com/googleplay/android-developer/answer/9845334
- **Firebase Crashlytics**: https://firebase.google.com/docs/crashlytics
- **Firebase Analytics**: https://firebase.google.com/docs/analytics

## Contact

Questions about beta testing? Email beta@happiecouple.app
