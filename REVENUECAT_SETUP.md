# 🎯 RevenueCat Setup & Implementation Guide

Complete guide to implementing real in-app purchases with RevenueCat for iOS App Store.

---

## 📋 Table of Contents

1. [Why RevenueCat?](#why-revenuecat)
2. [RevenueCat Account Setup](#revenuecat-account-setup)
3. [App Store Connect Configuration](#app-store-connect-configuration)
4. [RevenueCat Dashboard Configuration](#revenuecat-dashboard-configuration)
5. [Flutter Integration](#flutter-integration)
6. [Testing Subscriptions](#testing-subscriptions)
7. [Production Deployment](#production-deployment)
8. [Analytics & Monitoring](#analytics--monitoring)

---

## Why RevenueCat?

**Pros:**
- ✅ Simplest integration (2-3 days vs 5-7 days native)
- ✅ Cross-platform ready (iOS + Android with same code)
- ✅ Built-in analytics dashboard
- ✅ Server-side receipt validation
- ✅ Subscription management & webhooks
- ✅ A/B testing for pricing
- ✅ Excellent documentation

**Cons:**
- ❌ 1% fee on top of Apple's 30% (negligible for early stage)

**Recommendation:** Start with RevenueCat. Can migrate to native later if needed.

---

## 🚀 RevenueCat Account Setup

### Step 1: Create Account
1. Go to [https://www.revenuecat.com/](https://www.revenuecat.com/)
2. Click "Get Started Free"
3. Sign up with email or GitHub
4. Free tier includes:
   - Up to $10k monthly tracked revenue
   - Unlimited subscribers
   - Full feature access

### Step 2: Create Project
1. Create new project: **"Happie Couple"**
2. Select platform: **iOS**
3. Choose framework: **Flutter**

### Step 3: Get API Keys
1. Navigate to **Settings → API Keys**
2. Copy your **Public iOS SDK Key** (looks like: `appl_aBcDeFgH123456`)
3. Save this key - you'll need it for Flutter integration

**IMPORTANT:** Never commit API keys to git. Use environment variables or Flutter build configs.

---

## 🍎 App Store Connect Configuration

### Step 1: Create App ID
1. Go to [App Store Connect](https://appstoreconnect.apple.com/)
2. Navigate to **My Apps**
3. Click **+ App** (or use existing Happie Couple app)
4. Fill in app details:
   - **Name:** Happie Couple
   - **Primary Language:** English
   - **Bundle ID:** `com.happiecouple.app` (must match Xcode)
   - **SKU:** `happie-couple-001`

### Step 2: Create Subscription Group
1. In your app, go to **Features → In-App Purchases**
2. Click **+ Create** → **Subscription Group**
3. Name: **"Premium Membership"**
4. Reference Name: `premium_membership`

### Step 3: Create Subscription Products

#### Product 1: Monthly Subscription
- **Product ID:** `happie_monthly`
- **Reference Name:** Happie Couple Monthly
- **Subscription Duration:** 1 Month
- **Price:** €9.99 / month
- **Free Trial:** 7 days
- **Intro Offer:** €4.99 for first month

#### Product 2: Annual Subscription (RECOMMENDED)
- **Product ID:** `happie_annual`
- **Reference Name:** Happie Couple Annual
- **Subscription Duration:** 1 Year
- **Price:** €59.99 / year (save 50%)
- **Free Trial:** 7 days
- **Intro Offer:** None

#### Product 3: Lifetime (Optional)
- **Product ID:** `happie_lifetime`
- **Reference Name:** Happie Couple Lifetime
- **Type:** Non-Consumable
- **Price:** €149.99 one-time

### Step 4: Configure Subscription Details

For each subscription, add:

**Subscription Display Name:**
```
Monthly: "Premium Monthly"
Annual: "Premium Annual (Save 50%)"
```

**Description:**
```
Unlock all premium features:
• Unlimited AI insights
• Advanced relationship analytics
• Export your notes and meetings
• Priority customer support
• Milestone tracking
• Partner mood correlation analysis
• Early access to new features
```

**Review Information:**
- Screenshot of paywall screen
- Review notes explaining how to test with sandbox account

### Step 5: Set Up Pricing
1. Click **Subscription Pricing**
2. Set prices for all regions (auto-converts based on EUR)
3. Enable **Introductory Offers** (first month discount)
4. Configure **Promotional Offers** (win-back campaigns)

### Step 6: Create Sandbox Test Accounts
1. Go to **Users and Access → Sandbox Testers**
2. Click **+ Add Sandbox Tester**
3. Create 2-3 test accounts:
   - `test1@happiecouple.test`
   - `test2@happiecouple.test`
4. Use these for testing subscriptions in TestFlight

---

## 🎛️ RevenueCat Dashboard Configuration

### Step 1: Connect App Store Connect
1. In RevenueCat dashboard, go to your iOS app
2. Click **App Store Connect Integration**
3. Upload **App Store Connect API Key**:
   - Go to App Store Connect → Users & Access → Keys
   - Create new API key with "Admin" or "App Manager" role
   - Download `.p8` file
   - Upload to RevenueCat with Issuer ID and Key ID

### Step 2: Configure Products
1. In RevenueCat, go to **Products**
2. Click **+ Add Product**
3. Create three products matching App Store:

**Product 1:**
- Identifier: `happie_monthly`
- Type: Subscription
- Duration: 1 month

**Product 2:**
- Identifier: `happie_annual`
- Type: Subscription
- Duration: 1 year

**Product 3:**
- Identifier: `happie_lifetime`
- Type: Non-Subscription
- Duration: Lifetime

### Step 3: Create Entitlements
Entitlements = features users get access to.

1. Go to **Entitlements**
2. Click **+ Create Entitlement**
3. Name: **"premium"**
4. Identifier: `premium`
5. Attach all three products to this entitlement

### Step 4: Create Offerings
Offerings = how you present products to users (for A/B testing).

1. Go to **Offerings**
2. Click **+ Create Offering**
3. Create **"default"** offering:
   - Add all three products
   - Set order: Annual (default), Monthly, Lifetime
   - Annual is shown first (best value)

---

## 📱 Flutter Integration

### Step 1: Add RevenueCat SDK
Update `pubspec.yaml`:

```yaml
dependencies:
  purchases_flutter: ^6.7.0
```

Run:
```bash
flutter pub get
```

### Step 2: Update Info.plist (iOS)
Add to `ios/Runner/Info.plist`:

```xml
<key>NSAppTransportSecurity</key>
<dict>
  <key>NSAllowsArbitraryLoads</key>
  <true/>
</dict>
```

### Step 3: Replace SubscriptionService

Create new file: `lib/services/revenuecat_service.dart`

```dart
import 'package:flutter/material.dart';
import 'package:purchases_flutter/purchases_flutter.dart';

class RevenueCatService with ChangeNotifier {
  static final RevenueCatService _instance = RevenueCatService._internal();
  factory RevenueCatService() => _instance;
  RevenueCatService._internal();

  bool _isInitialized = false;
  bool _isPremium = false;
  String _subscriptionType = 'free';
  DateTime? _expirationDate;

  bool get isPremium => _isPremium;
  String get subscriptionType => _subscriptionType;
  bool get isInitialized => _isInitialized;
  DateTime? get expirationDate => _expirationDate;

  /// Initialize RevenueCat SDK
  Future<void> initialize(String userId) async {
    if (_isInitialized) return;

    try {
      // Configure SDK
      await Purchases.configure(
        PurchasesConfiguration('appl_YOUR_API_KEY_HERE')
          ..appUserID = userId
          ..observerMode = false,
      );

      // Set up listener for purchase updates
      Purchases.addCustomerInfoUpdateListener(_updateCustomerInfo);

      // Load initial customer info
      await refreshCustomerInfo();

      _isInitialized = true;
      debugPrint('✅ RevenueCat initialized for user $userId');
    } catch (e) {
      debugPrint('❌ Error initializing RevenueCat: $e');
      rethrow;
    }
  }

  /// Refresh customer info and update premium status
  Future<void> refreshCustomerInfo() async {
    try {
      final customerInfo = await Purchases.getCustomerInfo();
      _updateCustomerInfo(customerInfo);
    } catch (e) {
      debugPrint('❌ Error refreshing customer info: $e');
    }
  }

  /// Update customer info callback
  void _updateCustomerInfo(CustomerInfo customerInfo) {
    final premiumEntitlement = customerInfo.entitlements.all['premium'];

    _isPremium = premiumEntitlement?.isActive ?? false;

    if (_isPremium) {
      final productId = premiumEntitlement?.productIdentifier ?? '';
      if (productId.contains('monthly')) {
        _subscriptionType = 'monthly';
      } else if (productId.contains('annual')) {
        _subscriptionType = 'annual';
      } else if (productId.contains('lifetime')) {
        _subscriptionType = 'lifetime';
      }

      _expirationDate = premiumEntitlement?.expirationDate;

      debugPrint('✅ Premium active: $subscriptionType');
      if (_expirationDate != null) {
        debugPrint('📅 Expires: $_expirationDate');
      }
    } else {
      _subscriptionType = 'free';
      _expirationDate = null;
      debugPrint('ℹ️ Free tier active');
    }

    notifyListeners();
  }

  /// Get available offerings (products)
  Future<Offerings?> getOfferings() async {
    try {
      final offerings = await Purchases.getOfferings();
      if (offerings.current == null) {
        debugPrint('⚠️ No offerings configured in RevenueCat');
        return null;
      }
      return offerings;
    } catch (e) {
      debugPrint('❌ Error getting offerings: $e');
      return null;
    }
  }

  /// Purchase a product
  Future<bool> purchaseProduct(Package package) async {
    try {
      debugPrint('🛒 Purchasing: ${package.identifier}');

      final purchaseResult = await Purchases.purchasePackage(package);
      final customerInfo = purchaseResult.customerInfo;

      _updateCustomerInfo(customerInfo);

      final isPremium = customerInfo.entitlements.all['premium']?.isActive ?? false;

      if (isPremium) {
        debugPrint('✅ Purchase successful!');
        return true;
      } else {
        debugPrint('⚠️ Purchase completed but premium not active');
        return false;
      }
    } on PlatformException catch (e) {
      final errorCode = PurchasesErrorHelper.getErrorCode(e);

      if (errorCode == PurchasesErrorCode.purchaseCancelledError) {
        debugPrint('ℹ️ User cancelled purchase');
      } else if (errorCode == PurchasesErrorCode.productAlreadyPurchasedError) {
        debugPrint('ℹ️ Product already purchased');
        await restorePurchases();
      } else {
        debugPrint('❌ Purchase error: ${e.message}');
      }

      return false;
    } catch (e) {
      debugPrint('❌ Unexpected purchase error: $e');
      return false;
    }
  }

  /// Restore previous purchases
  Future<bool> restorePurchases() async {
    try {
      debugPrint('🔄 Restoring purchases...');

      final customerInfo = await Purchases.restorePurchases();
      _updateCustomerInfo(customerInfo);

      final isPremium = customerInfo.entitlements.all['premium']?.isActive ?? false;

      if (isPremium) {
        debugPrint('✅ Purchases restored successfully');
        return true;
      } else {
        debugPrint('ℹ️ No active purchases to restore');
        return false;
      }
    } catch (e) {
      debugPrint('❌ Error restoring purchases: $e');
      return false;
    }
  }

  /// Check if user can access a feature
  bool canAccessFeature(String feature) {
    if (_isPremium) return true;

    // Free tier features
    switch (feature) {
      case 'basic_notes':
      case 'weekly_meetings':
      case 'daily_checkins':
        return true;
      case 'unlimited_ai':
      case 'advanced_analytics':
      case 'export':
      case 'mood_correlation':
      case 'milestone_tracking':
        return false;
      default:
        return true;
    }
  }

  /// Get feature restriction message
  String getFeatureRestrictionMessage(String feature) {
    switch (feature) {
      case 'unlimited_ai':
        return 'Upgrade to Premium for unlimited AI insights';
      case 'advanced_analytics':
        return 'Unlock advanced relationship analytics with Premium';
      case 'export':
        return 'Export your data with Premium';
      case 'mood_correlation':
        return 'Analyze mood patterns with Premium';
      case 'milestone_tracking':
        return 'Track milestones with Premium';
      default:
        return 'This feature requires Premium';
    }
  }

  /// Premium features list
  List<String> get premiumFeatures => [
        'Unlimited AI insights',
        'Advanced analytics',
        'Export functionality',
        'Priority support',
        'Early access features',
        'Custom notifications',
        'Milestone tracking',
        'Partner mood analysis'
      ];

  /// Free features list
  List<String> get freeFeatures => [
        'Basic note taking',
        'Weekly meetings',
        'Daily check-ins',
        'Limited AI insights (3 per week)',
        'Basic progress tracking'
      ];

  /// Dispose
  @override
  void dispose() {
    Purchases.removeCustomerInfoUpdateListener(_updateCustomerInfo);
    super.dispose();
  }
}
```

### Step 4: Initialize in main.dart

Update `lib/main.dart`:

```dart
import 'package:provider/provider.dart';
import 'services/revenuecat_service.dart';

void main() async {
  WidgetsFlutterBinding.ensureInitialized();
  await Firebase.initializeApp();

  runApp(
    MultiProvider(
      providers: [
        ChangeNotifierProvider(create: (_) => AuthService()),
        ChangeNotifierProvider(create: (_) => RevenueCatService()),
        // ... other providers
      ],
      child: MyApp(),
    ),
  );
}
```

Initialize after user signs in:

```dart
// In AuthService after successful login
final userId = _auth.currentUser?.uid;
if (userId != null) {
  await RevenueCatService().initialize(userId);
}
```

### Step 5: Update PaywallScreen

Update `lib/screens/paywall_screen.dart`:

```dart
import 'package:purchases_flutter/purchases_flutter.dart';
import '../services/revenuecat_service.dart';

class PaywallScreen extends StatefulWidget {
  @override
  _PaywallScreenState createState() => _PaywallScreenState();
}

class _PaywallScreenState extends State<PaywallScreen> {
  final _revenueCatService = RevenueCatService();
  Offerings? _offerings;
  bool _isLoading = true;

  @override
  void initState() {
    super.initState();
    _loadOfferings();
  }

  Future<void> _loadOfferings() async {
    setState(() => _isLoading = true);

    final offerings = await _revenueCatService.getOfferings();

    setState(() {
      _offerings = offerings;
      _isLoading = false;
    });
  }

  Future<void> _purchasePackage(Package package) async {
    final success = await _revenueCatService.purchaseProduct(package);

    if (success && mounted) {
      Navigator.pop(context);
      ScaffoldMessenger.of(context).showSnackBar(
        SnackBar(content: Text('Welcome to Premium! 🎉')),
      );
    }
  }

  Future<void> _restorePurchases() async {
    final success = await _revenueCatService.restorePurchases();

    if (success && mounted) {
      Navigator.pop(context);
      ScaffoldMessenger.of(context).showSnackBar(
        SnackBar(content: Text('Purchases restored! ✅')),
      );
    } else if (mounted) {
      ScaffoldMessenger.of(context).showSnackBar(
        SnackBar(content: Text('No purchases to restore')),
      );
    }
  }

  @override
  Widget build(BuildContext context) {
    if (_isLoading) {
      return Scaffold(
        body: Center(child: CircularProgressIndicator()),
      );
    }

    if (_offerings?.current == null) {
      return Scaffold(
        body: Center(
          child: Text('Unable to load subscription options'),
        ),
      );
    }

    final packages = _offerings!.current!.availablePackages;

    return Scaffold(
      appBar: AppBar(title: Text('Upgrade to Premium')),
      body: SingleChildScrollView(
        padding: EdgeInsets.all(16),
        child: Column(
          children: [
            // Premium features list
            ...packages.map((package) => _buildPackageCard(package)),
            SizedBox(height: 16),

            // Restore button
            TextButton(
              onPressed: _restorePurchases,
              child: Text('Restore Purchases'),
            ),

            // Terms and privacy
            Text(
              'Terms • Privacy • Cancel Anytime',
              style: TextStyle(fontSize: 12, color: Colors.grey),
            ),
          ],
        ),
      ),
    );
  }

  Widget _buildPackageCard(Package package) {
    final product = package.storeProduct;

    return Card(
      child: ListTile(
        title: Text(product.title),
        subtitle: Text(product.description),
        trailing: Text(
          product.priceString,
          style: TextStyle(
            fontSize: 20,
            fontWeight: FontWeight.bold,
          ),
        ),
        onTap: () => _purchasePackage(package),
      ),
    );
  }
}
```

---

## 🧪 Testing Subscriptions

### Test in Simulator (Sandbox)
1. Open iOS Settings app
2. Sign out of your Apple ID
3. In Xcode, run the app on simulator
4. When prompted to sign in during purchase, use **sandbox test account**
5. Complete purchase (no real charge)
6. Verify premium features unlock

### Test in TestFlight
1. Upload build to App Store Connect
2. Add TestFlight testers
3. Testers download app via TestFlight
4. Use sandbox accounts for testing
5. Subscriptions renew every ~5 minutes in sandbox

### Verify in RevenueCat Dashboard
1. Go to **Customers** tab
2. Search for test user ID
3. Check subscription status
4. View transaction history

---

## 🚀 Production Deployment

### Pre-Launch Checklist
- [ ] All products approved in App Store Connect
- [ ] RevenueCat API keys secured (not in git)
- [ ] Paywall tested with sandbox accounts
- [ ] Restore purchases works correctly
- [ ] Terms of Service & Privacy Policy linked
- [ ] Subscription description clear and accurate
- [ ] Cancel flow tested
- [ ] Receipt validation working
- [ ] RevenueCat webhooks configured

### Go Live
1. Submit app for review with subscription products
2. Include demo account for reviewers in App Store Connect
3. Apple reviews subscriptions (can take 3-5 days)
4. Once approved, users can purchase

### Monitor First Week
- Check RevenueCat dashboard daily
- Monitor conversion rates
- Watch for subscription errors
- Track MRR (Monthly Recurring Revenue)
- Review customer feedback

---

## 📊 Analytics & Monitoring

### RevenueCat Dashboard Metrics
- **MRR:** Monthly Recurring Revenue
- **Active Subscribers:** Current paying users
- **Churn Rate:** Cancellations / Active subscribers
- **Trial Conversion:** Trial → Paid %
- **ARPU:** Average Revenue Per User
- **LTV:** Lifetime Value

### Key Metrics to Track
1. **Paywall Views:** How many users see paywall
2. **Trial Starts:** How many start free trial
3. **Trial Conversion:** Trial → Paid conversion rate (target: >40%)
4. **Monthly Churn:** Users who cancel (target: <5%)
5. **Annual vs Monthly:** Which plan is more popular

### Optimization Ideas
- **A/B test pricing:** Try €7.99 vs €9.99
- **Trial length:** Test 3 days vs 7 days
- **Paywall copy:** Test different messaging
- **Feature visibility:** Highlight most valuable features

---

## 🎯 Success Metrics

### Week 1 Goals
- [ ] Paywall shown to 50%+ new users
- [ ] Trial start rate >10%
- [ ] No major errors or crashes

### Month 1 Goals
- [ ] 500+ MAU (Monthly Active Users)
- [ ] Trial → Paid conversion >30%
- [ ] MRR: €500+
- [ ] Churn <10%

### Quarter 1 Goals
- [ ] 5,000+ MAU
- [ ] Trial → Paid conversion >40%
- [ ] MRR: €5,000+
- [ ] Churn <5%
- [ ] 500+ paying subscribers

---

## 🆘 Troubleshooting

### "Unable to Complete Purchase"
- Check App Store Connect: products approved?
- Verify RevenueCat products match exactly
- Ensure test account is sandbox account
- Try restore purchases

### Premium Not Unlocking
- Check RevenueCat customer info
- Verify entitlement is "premium" (case-sensitive)
- Check product is attached to entitlement
- Call `refreshCustomerInfo()`

### Products Not Loading
- Verify RevenueCat API key is correct
- Check internet connection
- Ensure products are created in both ASC and RevenueCat
- Review logs for specific error messages

---

## 📚 Resources

- [RevenueCat Docs](https://docs.revenuecat.com/)
- [Flutter SDK Guide](https://docs.revenuecat.com/docs/flutter)
- [App Store Connect Guide](https://developer.apple.com/app-store-connect/)
- [Apple In-App Purchase Guidelines](https://developer.apple.com/in-app-purchase/)
- [RevenueCat Community](https://community.revenuecat.com/)

---

**Estimated Implementation Time:** 8-12 hours
**Cost:** Free tier (up to $10k/month revenue)
**Complexity:** Medium (well-documented)

Good luck! 🚀
