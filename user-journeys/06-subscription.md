---
title: 06. Subscription Journey
layout: default
description: 06. Subscription Journey for Happie Couple.
---

# 06. Subscription Journey

## Overview

The subscription journey converts free users into paying Premium subscribers. This is the primary monetization flow and must balance value communication with non-aggressive conversion tactics.

---

## User Goal

**"I want to unlock advanced features to improve my relationship faster."**

---

## Subscription Tiers

### Free Tier
**Features**:
- ✅ Basic note taking
- ✅ Weekly meetings (limited)
- ✅ Daily check-ins
- ✅ Limited AI insights (3 per week)
- ✅ Basic progress tracking

**Limitations**:
- ❌ No unlimited AI insights
- ❌ No advanced analytics
- ❌ No export functionality
- ❌ No priority support

### Premium Tiers

| Tier | Price | Best For | Savings |
|------|-------|----------|---------|
| **Monthly** | €9.99/month | Trying it out | - |
| **Annual** | €59.99/year | Committed couples | Save 50% |
| **Lifetime** | €149.99 one-time | Long-term investment | Best Value |

---

## Journey Entry Points

Users can discover Premium from multiple places:

### 1. Profile Tab (Primary)
**Location**: Profile → Subscription Status Card

**What User Sees**:
- 🆓 **Free Account** badge (for free users)
- ⭐ **Premium Account** badge (for paid users)
- Subtitle: "Upgrade to unlock all features"
- Tap anywhere → Navigate to **PaywallScreen**

### 2. Feature Gating (Natural Discovery)
**Triggers**:
- User tries to export notes → Show paywall
- User exhausts free AI insights (3/week) → Show paywall
- User wants advanced analytics → Show paywall

**Message**:
> "This feature requires Premium"
> [Upgrade Now] [Maybe Later]

### 3. Profile Settings Link
**Location**: Profile → "Edit Profile" → Premium features section

---

## Paywall Screen Experience

**Screen**: `PaywallScreen`

### Visual Design:
- **Background**: Gradient (pink to purple) - premium feel
- **Header**: Close button (X) + "Premium" badge
- **Main Content**:
  - Large headline: "Unlock Your Relationship's Full Potential"
  - Subheadline: "Get unlimited access to all premium features"

### Subscription Plans Display:

3 cards displayed vertically:

```
┌─────────────────────────┐
│  Monthly                │
│  €9.99/month           │
│  [     Select     ]    │
└─────────────────────────┘

┌─────────────────────────┐
│  ⭐ MOST POPULAR       │
│  Annual                │
│  €59.99/year          │
│  Save 50%             │
│  [     Select     ]    │  ← Pre-selected
└─────────────────────────┘

┌─────────────────────────┐
│  Lifetime              │
│  €149.99 one-time     │
│  Best Value           │
│  [     Select     ]    │
└─────────────────────────┘
```

### Premium Features List:

✅ Unlimited AI-powered insights
✅ Advanced relationship analytics
✅ Personalized weekly meeting topics
✅ Export notes and meeting summaries
✅ Priority customer support
✅ Early access to new features
✅ Advanced progress tracking
✅ Custom notification schedules
✅ Relationship milestone celebrations
✅ Partner mood correlation analysis

### Call-to-Action:
**Primary Button**: "Start My Premium Experience"
- Large, prominent button
- Color matches selected plan
- Shows selected plan name

**Legal Links** (small text at bottom):
- Terms of Service
- Privacy Policy
- Restore Purchases (for returning users)

---

## Purchase Flow

### Step 1: User Selects Plan
- Taps on one of the 3 plan cards
- Selected card highlights (border, color change)
- Button text updates: "Start €59.99/year Subscription"

### Step 2: User Taps Subscribe Button
**What Happens** (TODO - Implement):
1. Show loading indicator
2. Call RevenueCat/StoreKit purchase API
3. iOS shows Apple payment sheet
4. User confirms with Face ID/Touch ID/Password

### Step 3: Purchase Processing
**Loading State**:
- Disable buttons
- Show spinner
- Message: "Processing your subscription..."

**Success Path**:
```
Purchase Success
    ↓
Save to Firestore (user.subscriptionType = 'annual')
    ↓
Update SubscriptionService state
    ↓
Show success message: "🎉 Welcome to Premium!"
    ↓
Dismiss paywall → Return to previous screen
    ↓
User now sees Premium features unlocked
```

**Error Paths**:
- ❌ User cancels → Return to paywall
- ❌ Payment declined → Show error: "Payment failed. Please check your payment method."
- ❌ Network error → Show error: "Connection lost. Please try again."
- ❌ Apple service down → Show error: "Purchase unavailable. Please try later."

---

## Subscription Management

### Viewing Subscription Status

**Location**: Profile Tab → Subscription Status Card

**Free User Sees**:
```
┌───────────────────────────┐
│ 🆓  Free Account         │
│ Upgrade to unlock all    │
│ features               → │
└───────────────────────────┘
```

**Premium User Sees**:
```
┌───────────────────────────┐
│ ⭐  Premium Account      │
│ Annual Plan              │
│ Manage Subscription    → │
└───────────────────────────┘
```

### Managing Subscription (TODO)

**Tap on Premium card** → Navigate to subscription management

**Options**:
- View current plan
- See renewal date
- Cancel subscription (opens App Store)
- Change plan (upgrade/downgrade)
- Restore purchases

---

## Free Trial (Optional - Future Enhancement)

### 7-Day Free Trial Option:

**Modified Paywall**:
- All plans show "Start 7-Day Free Trial"
- After trial: Auto-converts to paid
- User can cancel anytime during trial

**Trial Benefits**:
- Higher conversion rates (25-35%)
- User experiences Premium value
- Reduces purchase anxiety

**Implementation Notes**:
- Must be clearly communicated: "Free for 7 days, then €59.99/year"
- Easy cancellation process required
- Reminder notification before trial ends

---

## Conversion Optimization

### Psychological Triggers Used:

1. **Anchoring**: Annual plan "Save 50%" vs Monthly
2. **Social Proof**: "Most Popular" badge on Annual
3. **Scarcity**: "Best Value" on Lifetime
4. **Loss Aversion**: "Unlock" vs "Buy"
5. **Clear Value**: Specific feature list

### A/B Testing Opportunities:

**Test 1: Pricing Display**
- A: €59.99/year
- B: €4.99/month (billed annually)

**Test 2: Trial vs No Trial**
- A: 7-day free trial
- B: Direct purchase

**Test 3: Feature Order**
- A: Most valuable features first
- B: Most popular features first

---

## Retention & Churn Prevention

### Subscription Lifecycle:

```
Free User
    ↓
    [Paywall shown 3-5 times]
    ↓
Converts to Premium
    ↓
    [30 days: Honeymoon period]
    ↓
    [60-90 days: Value validation]
    ↓
    [Before Renewal: Critical moment]
    ↓
Renews ✅ or Cancels ❌
```

### Preventing Churn:

**At Risk Signals**:
- ❌ User hasn't opened app in 7 days
- ❌ No notes added in 14 days
- ❌ No agenda generated in 30 days
- ❌ Partner not linked after 14 days

**Intervention Strategies**:
1. **Re-engagement notification**
   - "We miss you! Here's a relationship tip for today..."

2. **Value reminder email**
   - "Your relationship insights from last month"
   - Show their progress/stats

3. **Win-back offer** (if canceled)
   - "Come back! 50% off for 3 months"

---

## Implementation Status

### ✅ Completed:
- SubscriptionService with state persistence
- Paywall UI design
- Free/Premium feature gating
- Profile subscription status display
- EUR pricing

### ❌ TODO (Critical for Launch):
- [ ] Integrate RevenueCat or StoreKit
- [ ] Implement actual purchase flow
- [ ] Set up App Store Connect subscriptions
- [ ] Add subscription validation
- [ ] Implement "Restore Purchases"
- [ ] Add receipt validation
- [ ] Handle subscription expiry
- [ ] Add cancellation flow

### 🔧 Future Enhancements:
- [ ] 7-day free trial
- [ ] Promotional codes
- [ ] Referral discounts
- [ ] Gift subscriptions
- [ ] Family plans (2 couples)

---

## Success Metrics

### Conversion Metrics:

1. **Free to Premium Conversion Rate**
   - Target: 15-25% (industry standard: 5-10%)
   - Measure: Premium subscribers / Total active users

2. **Time to Conversion**
   - Target: Median 7-14 days
   - Measure: Days between sign up and first purchase

3. **Plan Distribution**
   - Monthly: 30%
   - Annual: 60% (goal - highest LTV)
   - Lifetime: 10%

4. **Monthly Recurring Revenue (MRR)**
   - Target: €5,000 by month 6
   - Normalize annual to monthly (€59.99 / 12 = €5/month)

### Retention Metrics:

1. **1-Month Retention**
   - Target: 90%+
   - High churn in first month indicates poor value

2. **6-Month Retention**
   - Target: 70%+
   - Industry standard: 50-60%

3. **Annual Renewal Rate**
   - Target: 75%+
   - Key metric for sustainability

---

## Files Involved

- `lib/screens/paywall_screen.dart`
- `lib/services/subscription_service.dart`
- `lib/screens/profile/profile_screen.dart`

---

**Next Journey**: [07. Notifications](07-notifications.md)
