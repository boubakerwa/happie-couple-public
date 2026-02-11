# GitHub Pages Setup Guide

This guide explains how to host your Privacy Policy and Terms of Service on GitHub Pages for free.

## Why GitHub Pages?

- ✅ **Free hosting** for public repositories
- ✅ **HTTPS enabled** by default (required by Apple)
- ✅ **Easy to update** via git commits
- ✅ **Professional URLs** (e.g., `https://boubakerwa.github.io/happie-couple/privacy`)
- ✅ **Version control** for legal documents

## Setup Instructions

### Option 1: Enable GitHub Pages (Recommended - Simplest)

1. **Go to Your Repository Settings**
   - Navigate to: https://github.com/boubakerwa/happie-couple
   - Click **Settings** tab
   - Scroll to **Pages** section (left sidebar)

2. **Configure GitHub Pages**
   - **Source**: Select `Deploy from a branch`
   - **Branch**: Select `main` (or your default branch)
   - **Folder**: Select `/docs`
   - Click **Save**

3. **Wait for Deployment** (2-5 minutes)
   - GitHub will automatically build and deploy your site
   - Visit: `https://boubakerwa.github.io/happie-couple/`

4. **Your URLs Will Be:**
   - Privacy Policy: `https://boubakerwa.github.io/happie-couple/PRIVACY_POLICY`
   - Terms of Service: `https://boubakerwa.github.io/happie-couple/TERMS_OF_SERVICE`

### Option 2: Custom Domain (Optional - More Professional)

If you own `happiecouple.com`:

1. **Buy Domain** (if you don't have one)
   - Recommended: Namecheap, Google Domains, Cloudflare

2. **Add Custom Domain in GitHub**
   - In **Settings** → **Pages**
   - Enter: `legal.happiecouple.com` or `happiecouple.com`
   - Click **Save**

3. **Configure DNS Records**
   Add these records at your domain registrar:

   ```
   Type: CNAME
   Name: legal (or www)
   Value: boubakerwa.github.io
   TTL: 3600
   ```

   Or for apex domain (no subdomain):
   ```
   Type: A
   Name: @
   Value: 185.199.108.153
   Value: 185.199.109.153
   Value: 185.199.110.153
   Value: 185.199.111.153
   ```

4. **Enable HTTPS**
   - In GitHub Pages settings, check **Enforce HTTPS**
   - Wait 24-48 hours for SSL certificate

5. **Your URLs Will Be:**
   - Privacy Policy: `https://legal.happiecouple.com/PRIVACY_POLICY`
   - Terms of Service: `https://legal.happiecouple.com/TERMS_OF_SERVICE`

## Create Index Page (Better UX)

Create a homepage for easier navigation:

1. **Create** `docs/index.md`:

```markdown
# Happie Couple - Legal Documents

Welcome to Happie Couple's legal information center.

## Important Documents

- [Privacy Policy](PRIVACY_POLICY.md) - How we protect your data
- [Terms of Service](TERMS_OF_SERVICE.md) - App usage terms
- [Support](https://happiecouple.com/support) - Get help

## Contact

- **Email**: support@happiecouple.com
- **Privacy Questions**: privacy@happiecouple.com

---

Last Updated: February 1, 2026
```

2. **Add Jekyll Configuration** (Optional - for better styling)

Create `docs/_config.yml`:

```yaml
title: Happie Couple Legal
description: Privacy Policy and Terms of Service for Happie Couple
theme: jekyll-theme-minimal
# Or choose: cayman, slate, architect, etc.
```

## Using URLs in Your App

Once deployed, update your app to reference these URLs:

### In Info.plist (iOS):
```xml
<key>NSPrivacyPolicyURL</key>
<string>https://boubakerwa.github.io/happie-couple/PRIVACY_POLICY</string>
```

### In App Store Connect:
- **Privacy Policy URL**: `https://boubakerwa.github.io/happie-couple/PRIVACY_POLICY`
- **Terms of Service URL**: `https://boubakerwa.github.io/happie-couple/TERMS_OF_SERVICE`
- **Support URL**: `https://boubakerwa.github.io/happie-couple/` (or create support.md)

### In Your App Code:
```dart
// lib/constants/app_constants.dart
class AppConstants {
  static const String privacyPolicyUrl =
    'https://boubakerwa.github.io/happie-couple/PRIVACY_POLICY';

  static const String termsOfServiceUrl =
    'https://boubakerwa.github.io/happie-couple/TERMS_OF_SERVICE';

  static const String supportUrl =
    'https://boubakerwa.github.io/happie-couple/';
}
```

## Updating Documents

To update Privacy Policy or Terms of Service:

1. **Edit the file** in `docs/PRIVACY_POLICY.md` or `docs/TERMS_OF_SERVICE.md`
2. **Update "Last Updated" date** at the top
3. **Commit and push** changes
4. GitHub Pages auto-deploys (2-5 minutes)

## Testing Your Pages

After deployment:

1. **Visit URLs** in browser
2. **Check HTTPS** (should show lock icon)
3. **Test on mobile** (iOS Safari, Android Chrome)
4. **Verify formatting** looks correct

## Troubleshooting

**404 Not Found?**
- Wait 5-10 minutes after enabling GitHub Pages
- Check that files are in `/docs` folder
- Verify branch name is correct in Pages settings

**Not updating?**
- Clear browser cache
- Wait 5 minutes for GitHub to rebuild
- Check commit was pushed to correct branch

**Styling looks bad?**
- Add `_config.yml` with theme
- Use `.html` extensions instead of `.md` for custom styling

**URLs too long?**
- Use custom domain (Option 2)
- Or use URL shortener as fallback

## Best Practices

✅ **DO:**
- Keep documents in `/docs` folder for organization
- Update "Last Updated" date when editing
- Use HTTPS URLs in App Store submission
- Test URLs before submitting to Apple
- Version control legal changes

❌ **DON'T:**
- Make repository private (GitHub Pages won't work on free plan)
- Delete `/docs` folder
- Use relative links in app (use full URLs)
- Forget to commit changes before expecting updates

## Cost

- **GitHub Pages**: FREE for public repositories
- **Custom Domain**: $10-15/year (optional)
- **Total**: $0 (or $10-15/year with custom domain)

## Alternative: Simple HTML Hosting

If you prefer pure HTML instead of Markdown:

1. Create `docs/privacy.html` and `docs/terms.html`
2. Style with inline CSS or link external stylesheet
3. Same deployment process

## Next Steps

After setting up GitHub Pages:

1. ✅ Enable GitHub Pages in repository settings
2. ✅ Wait for deployment
3. ✅ Test URLs in browser
4. ✅ Update App Store Connect with URLs
5. ✅ Reference URLs in app code
6. ✅ Add URLs to README.md

---

**Questions?** Check GitHub Pages documentation: https://docs.github.com/en/pages
