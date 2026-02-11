# 01. Onboarding & Sign Up Journey

## Overview

The onboarding journey is the critical first impression that converts downloads into active users. It establishes the app's value proposition and guides users to their first meaningful action.

---

## User Goal

**"I want to start using Happie Couple to improve my relationship."**

---

## Journey Steps

### Step 1: App Launch → Splash Screen

**Screen**: `SplashScreen`

**What Happens**:
- App logo displays (1-2 seconds)
- Firebase initializes in background
- NotificationService initializes
- SubscriptionService loads saved state
- AuthService checks if user is already logged in

**Transitions**:
- ✅ User is logged in → Navigate to **HomeScreen**
- ❌ User not logged in → Navigate to **WelcomeScreen**

---

### Step 2: Welcome Screen

**Screen**: `WelcomeScreen`

**Content Displayed**:
- App logo/icon (heart symbol)
- Headline: "Welcome to Happie Couple"
- Subtitle: "Strengthen your relationship with daily notes, weekly coaching sessions, and personalized insights."
- 3 Feature highlights:
  - 📝 Daily Notes - Track your relationship moments
  - 📅 Weekly Coaching - Get personalized agenda for discussions
  - 💡 Smart Insights - Discover patterns and growth opportunities

**Call-to-Actions**:
1. **Primary**: "Get Started" button → **SignUpScreen**
2. **Secondary**: "I already have an account" link → **SignInScreen**
3. **Support**: "Help & Crisis Resources" link → **HelpSupportScreen**

**Legal Disclaimer** (bottom):
> "This is a relationship coaching tool, not a substitute for professional therapy."

**User Decision Point**:
- New user → Click "Get Started"
- Returning user → Click "I already have an account"
- Concerned user → Click "Help & Crisis Resources"

---

### Step 3A: Sign Up (New Users)

**Screen**: `SignUpScreen`

**Form Fields**:
1. **Name** (text input)
   - Placeholder: "Your name"
   - Validation: Required, 2-50 characters

2. **Email** (email input)
   - Placeholder: "your@email.com"
   - Validation: Valid email format, RFC-compliant regex
   - Error: "Please enter a valid email address"

3. **Password** (password input)
   - Placeholder: "Choose a secure password"
   - Validation: Minimum 6 characters
   - Show/hide password toggle

**Call-to-Action**:
- **Primary**: "Create Account" button
- **Secondary**: "Already have an account? Sign In" link

**What Happens on Submit**:
1. Validate form inputs
2. Show loading indicator
3. Call `AuthService.signUpWithEmailAndPassword()`
4. Create user document in Firestore
5. Initialize user preferences

**Success Path**:
- ✅ Account created → Navigate to **HomeScreen**
- 🎉 Show welcome message: "Welcome to Happie Couple!"
- 📱 Request notification permissions (iOS prompt)

**Error Paths**:
- ❌ Email already in use → Show error: "This email is already registered"
- ❌ Weak password → Show error: "Password must be at least 6 characters"
- ❌ Network error → Show error: "Connection failed. Please try again."

---

### Step 3B: Sign In (Returning Users)

**Screen**: `SignInScreen`

**Form Fields**:
1. **Email** (email input)
2. **Password** (password input)

**Call-to-Action**:
- **Primary**: "Sign In" button
- **Secondary**: "Forgot Password?" link (TODO: implement)
- **Tertiary**: "Don't have an account? Sign Up" link

**What Happens on Submit**:
1. Validate inputs
2. Call `AuthService.signInWithEmailAndPassword()`
3. Load user data from Firestore

**Success Path**:
- ✅ Credentials valid → Navigate to **HomeScreen**
- 🔄 Load user's existing notes, agendas, etc.

**Error Paths**:
- ❌ Invalid credentials → Show error: "Invalid email or password"
- ❌ Network error → Show error: "Connection failed. Please try again."

---

### Step 4: First Landing on Home Screen

**Screen**: `HomeScreen`

**What User Sees**:
- 4-tab bottom navigation (Notes, Agenda, Date Ideas, Profile)
- Default tab: **Notes**
- Empty state in Notes tab:
  - Icon: Note add icon
  - Message: "No notes yet"
  - Subtext: "Start documenting your relationship journey"
  - CTA: "Add Your First Note" button

**User's First Actions** (typical):
1. Browse tabs to explore app
2. Check Profile tab to see their info
3. Add first note (encouraged by empty state)

---

### Step 5: First Note Creation (Activation Moment)

**Trigger**: User taps "Add Your First Note" or FloatingActionButton

**Screen**: `AddNoteScreen`

**What User Does**:
1. Enter note title
2. Write note content
3. Select mood (1-5 stars)
4. Choose note type (Positive/Negative/Neutral)
5. Set privacy level (Private/Shared with partner)
6. Add optional tags

**Success**:
- ✅ Note saved to Firestore
- 📱 Show success message
- 🎊 Optional: Trigger encouragement notification later
- ↩️ Navigate back to Notes list

**This is the KEY ACTIVATION MOMENT** - User has created value in the app!

---

### Step 6: Post-Activation Experience

**Next Suggested Actions**:

1. **Link with Partner** (High Priority)
   - Show card in Profile: "Link with your partner to share insights"
   - Benefit: Unlock couple features

2. **Set Up Notifications** (Medium Priority)
   - Prompt: "Want daily reminders to add notes?"
   - Navigate to NotificationsScreen

3. **Explore Premium** (Low Priority - Don't Pressure)
   - Show Premium card in Profile
   - Soft sell: "Upgrade to unlock unlimited AI insights"

---

## Success Metrics

### Critical Onboarding Metrics:

1. **Sign Up Completion Rate**
   - Target: >80% of users who start sign up complete it
   - Measure: (Accounts Created / Sign Up Started)

2. **First Note Within 24 Hours**
   - Target: >60% of new users add a note in first day
   - This indicates activation!

3. **7-Day Retention**
   - Target: >40% of users return within 7 days
   - Measure: Users who open app 7 days after sign up

4. **Partner Linking Within 7 Days**
   - Target: >30% of users link with partner
   - This dramatically increases retention!

---

## Edge Cases & Error Handling

### No Internet Connection
- Show friendly error: "No internet connection. Please check your network."
- Allow user to retry

### Firebase Service Down
- Show error: "We're having technical difficulties. Please try again later."
- Log error for monitoring

### Email Verification (Future Enhancement)
- Currently: No email verification required
- Future: Send verification email, require click before full access

### Apple/Google Sign-In (Future)
- Currently: Only email/password
- Future: Add social login for faster onboarding

---

## User Testing Feedback

### What Users Like:
- ✅ Simple, clear value proposition
- ✅ Quick sign up process (3 fields only)
- ✅ Immediate access (no email verification delay)
- ✅ Crisis resources link (shows care)

### Pain Points to Address:
- ❌ Some users confused about "partner linking" (show explainer)
- ❌ Privacy concerns about sharing (emphasize encryption)
- ❌ Unclear what "AI coaching" means (add examples)

---

## Implementation Notes

### Files Involved:
- `lib/screens/splash_screen.dart`
- `lib/screens/onboarding/welcome_screen.dart`
- `lib/screens/onboarding/sign_up_screen.dart`
- `lib/screens/onboarding/sign_in_screen.dart`
- `lib/screens/home/home_screen.dart`
- `lib/services/auth_service.dart`

### Key Services:
- **AuthService** - Handles Firebase Authentication
- **FirestoreService** - Creates initial user document
- **NotificationService** - Requests iOS permissions

### Analytics Events to Track:
- `onboarding_started` - Welcome screen viewed
- `sign_up_started` - Sign up screen viewed
- `sign_up_completed` - Account created successfully
- `first_note_created` - User added first note
- `partner_linking_started` - User initiated linking

---

**Next Journey**: [02. Partner Linking](02-partner-linking.md)
