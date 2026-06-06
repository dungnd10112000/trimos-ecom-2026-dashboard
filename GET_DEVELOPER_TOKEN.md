# Get Your Google Ads Developer Token

## Issue
The Google Ads API requires a **Developer Token** which is different from the service account credentials you already have.

## How to Get Developer Token

### Step 1: Log into Google Ads
- Go to: https://ads.google.com/
- Sign in with your account (606-065-4572)

### Step 2: Navigate to API Center
1. Click your **Account icon** (top right)
2. Go to **Tools & Settings**
3. Click **Tools** in the left sidebar
4. Select **API Center**

### Step 3: Request or Copy Developer Token
- You should see your **Developer Token** displayed
- If you haven't requested one yet:
  - Click "**Get Developer Token**" (if available)
  - You may need to wait 1-2 days for approval
- **Copy** the token (looks like: `1234567890ABCDEFGH`)

## Update Your Script

Once you have the developer token, update the script:

### Option 1: Edit the Python File
Edit `google_ads_extract_keywords.py` and update line 11:

```python
DEVELOPER_TOKEN = "YOUR_DEVELOPER_TOKEN_HERE"  # ← Paste your token here
```

### Option 2: Create a Config File
Create `google-ads-dev-token.txt` with just the token:
```
YOUR_DEVELOPER_TOKEN_HERE
```

Then the script will read it automatically.

## Limitations

**Developer tokens can only be obtained through Google Ads accounts with:**
- Active campaigns (currently running ads)
- In good standing (no violations)

If your account is new or dormant, you may need to:
1. Create a simple test campaign
2. Wait for API access approval (1-2 days)
3. Then request the developer token

## Alternative: Use Google Ads OAuth

If service account doesn't work, you can use OAuth 2.0 instead:
- Google will provide OAuth credentials
- Requires browser-based authentication
- Better for shared/team accounts

## Test After Getting Token

Once you have the token, run:
```bash
python google_ads_extract_keywords.py
```

## Status

Current setup:
- ✓ Service account credentials
- ✓ Google Ads customer ID: 606-065-4572
- ✓ Keywords list ready
- ⏳ **Waiting for: Developer Token**

---

**Time to complete:** 2-5 minutes (if approved)  
**Approval time:** Usually immediate, sometimes 1-2 days

For more info: https://developers.google.com/google-ads/api/docs/start#developer-token
