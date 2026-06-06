# Google Ads Keyword Planner - Setup Guide

## Overview
Extract keyword metrics (monthly search volume, competition, bid prices) from Google Ads using Keyword Planner API.

## Prerequisites

### 1. Google Cloud Project Setup
Your service account credentials are already set up: `fine-justice-445008-r9-e310aac19d14.json`

### 2. Enable Required APIs
In Google Cloud Console (https://console.cloud.google.com/):
1. Go to project: `fine-justice-445008-r9`
2. Enable these APIs:
   - Google Ads API
   - Google Cloud Identity API

### 3. Find Your Google Ads Customer ID
1. Log in to Google Ads (https://ads.google.com/)
2. Click the account icon (top right)
3. Copy the **Account ID** (format: `123-456-7890`)
4. Convert to numeric format: `1234567890`

## Installation

### Step 1: Install Python Dependencies
```bash
cd "C:\Users\ADMIN\Desktop\Code\Báo Cáo Ads"
pip install -r requirements_google_ads.txt
```

### Step 2: Create google_ads_config.py (optional, for easier management)
```python
# google_ads_config.py
GOOGLE_ADS_CONFIG = {
    "client_id": "116385461094448141498",
    "client_secret": "YOUR_CLIENT_SECRET",
    "developer_token": "YOUR_DEVELOPER_TOKEN",
    "customer_id": "1234567890",  # ← Update with YOUR customer ID
    "use_proto_plus": True,
}
```

## Usage

### Basic Usage
```bash
python google_ads_keyword_planner.py
```

### Configuration in Script
Before running, edit `google_ads_keyword_planner.py` and update:

```python
CUSTOMER_ID = "1234567890"  # ← Your Google Ads Customer ID
KEYWORDS = ["python", "data science"]  # ← Keywords to research
LOCATION_IDS = ["2840"]  # Location codes
```

### Common Location IDs
- **2840** - United States
- **2842** - Vietnam
- **1023** - Canada
- **2056** - United Kingdom
- **2076** - France
- [Full list](https://developers.google.com/google-ads/api/reference/data/geotargetconstant)

## Output

Results are saved to: `keyword_planner_data.csv`

### CSV Columns
| Column | Description |
|--------|-------------|
| Keyword | The keyword |
| Monthly Searches | Average monthly search volume |
| Competition Level | LOW, MEDIUM, or HIGH |
| Low Top of Page Bid | Minimum CPC (in micros: divide by 1,000,000) |
| High Top of Page Bid | Maximum CPC (in micros: divide by 1,000,000) |

### Example Output
```
Keyword,Monthly Searches,Competition Level,Low Top of Page Bid,High Top of Page Bid
python,550000,HIGH,150000,2500000
python tutorial,45000,MEDIUM,75000,1500000
```

## Troubleshooting

### Error: "Credentials not found"
- Ensure `fine-justice-445008-r9-e310aac19d14.json` exists
- Check file path is correct in script

### Error: "API not enabled"
1. Go to Google Cloud Console
2. Search for "Google Ads API"
3. Click "Enable"

### Error: "Invalid customer ID"
- Customer ID must be numeric (no hyphens)
- Check Google Ads account settings

### Error: "Developer token required"
1. In Google Ads, go to **Admin** → **Account** → **API**
2. Request or view your developer token
3. Add to configuration

## Advanced Usage

### Save with Custom Format
```python
# Modify save_to_csv() to include additional fields
# Or export to Excel using openpyxl
```

### Filter Results
```python
# In extract_keyword_metrics():
filtered = [r for r in results if r['Monthly Searches'] > 1000]
```

### Batch Processing Multiple Keywords
```python
keyword_groups = [
    ["python", "python tutorial"],
    ["data science", "machine learning"],
    ["web development", "web design"]
]

for group in keyword_groups:
    results = extract_keyword_metrics(client, CUSTOMER_ID, group)
    save_to_csv(results, f"keywords_{group[0]}.csv")
```

## Integration with Power BI

1. **Import CSV into Power BI Desktop**:
   - Power BI Desktop → Get Data → Text/CSV
   - Select `keyword_planner_data.csv`
   - Load into model

2. **Create DAX Measures**:
   ```dax
   Avg Monthly Searches = AVERAGE('Keywords'[Monthly Searches])
   Competition Score = SWITCH('Keywords'[Competition Level],
       "LOW", 1, "MEDIUM", 2, "HIGH", 3, 0)
   CPC Average = AVERAGE('Keywords'[High Top of Page Bid]) / 1000000
   ```

3. **Visualizations**:
   - Bar chart: Keywords vs Monthly Searches
   - Scatter: Search Volume vs Competition
   - Table: Complete metrics with sorting/filtering

## Next Steps

1. ✅ Copy `google_ads_keyword_planner.py` to your project
2. 📝 Update `CUSTOMER_ID` with your Google Ads Account ID
3. 📋 Update `KEYWORDS` list with your keywords
4. 🔧 Install dependencies: `pip install -r requirements_google_ads.txt`
5. ▶️ Run: `python google_ads_keyword_planner.py`
6. 📊 Import results into Power BI

## Support

For issues with:
- **Google Ads API**: https://developers.google.com/google-ads/api/docs
- **Google Cloud**: https://cloud.google.com/docs
- **Authentication**: Check service account has proper permissions in Google Cloud console
