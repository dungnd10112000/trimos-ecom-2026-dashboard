# Upgrade Google Ads API Access Level

## Current Status

✓ Developer Token is valid and working
✗ Access level is "Explorer" (read-only/limited)
⏳ Need: "Basic" or "Standard" access

## Error Message

```
This method is not allowed for use with explorer access. 
Please apply for basic or standard access.
```

The Keyword Planner API requires at least **Basic** access level, but your token currently has **Explorer** access (limited).

## How to Upgrade

### Step 1: Log into Google Ads
- Go to: https://ads.google.com/
- Sign in with your account

### Step 2: Navigate to API Settings
1. Click your **Account icon** (top right)
2. Go to **Tools & Settings**
3. Select **API Center** under **Tools**

### Step 3: Request Access Level Upgrade
Look for your Developer Token and find one of these options:
- **"Request Basic Access"** button
- **"Upgrade to Basic"** or similar
- **"Access Level Settings"**

### Step 4: Complete the Application
Google may ask you to:
- Confirm your use case (e.g., "Keyword research", "Analytics")
- Agree to API terms
- Verify email

### Step 5: Wait for Approval
- **Basic Access**: Usually 1-3 days
- **Standard Access**: May require additional review

### Alternative: Check Existing Access

If you already have multiple developer tokens:
1. Go to API Center
2. Check if another token has **Basic** or **Standard** access
3. Use that token instead in the script

## Apply the New Token

Once you get Basic access and a new developer token:

1. Update `google_ads_extract_keywords.py` line 11:
   ```python
   'developer_token': 'YOUR_NEW_TOKEN_HERE',
   ```

2. Run the extraction:
   ```bash
   python google_ads_extract_keywords.py
   ```

## API Access Levels Explained

| Level | Permissions | Requirements |
|-------|-------------|--------------|
| **Explorer** | View own account only | Testing |
| **Basic** | Limited API usage | 10 requests/second |
| **Standard** | Production use | Higher rate limits |

## Status Check

You have:
- ✓ Service account credentials
- ✓ Customer ID: 606-065-4572
- ✓ Developer Token: NcSDPq9siPswWmLsLCjXag
- ✓ Keywords ready
- ⏳ **Waiting for: Basic or Standard API Access**

## Timeline

- Request sent: Just now
- Expected approval: 1-3 business days
- You'll get email notification when approved

---

**Estimated time to activate:** 1-3 days (after approval, extraction runs immediately)

For more info: https://developers.google.com/google-ads/api/docs/access-levels
