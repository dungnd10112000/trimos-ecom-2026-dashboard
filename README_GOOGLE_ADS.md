# Google Ads Keyword Planner Integration

Extract keyword metrics (search volume, competition, CPC pricing) from Google Ads Keyword Planner and import into Power BI.

## 📁 Files Created

| File | Purpose |
|------|---------|
| `google_ads_extract_keywords.py` | **Main script** - Use this to extract keywords |
| `keywords_to_research.txt` | Edit this file - Add keywords you want to research |
| `test_google_ads_connection.py` | Verify API setup is working |
| `requirements_google_ads.txt` | Python dependencies to install |
| `SETUP_GOOGLE_ADS_API.md` | Detailed setup instructions |

## 🚀 Quick Start (3 Steps)

### Step 1: Install Dependencies
```bash
cd "C:\Users\ADMIN\Desktop\Code\Báo Cáo Ads"
pip install -r requirements_google_ads.txt
```

### Step 2: Add Your Keywords
Edit `keywords_to_research.txt` and replace the examples with your keywords:
```
python
digital marketing
seo
web design
content marketing
```

### Step 3: Run the Extraction
```bash
python google_ads_extract_keywords.py
```

Output: `keyword_planner_data_YYYYMMDD_HHMMSS.csv`

## 🔧 Testing Your Setup

Before running the full extraction, test that everything is configured correctly:

```bash
python test_google_ads_connection.py
```

This will verify:
- ✓ Credentials file is valid
- ✓ Google Ads API client initialized
- ✓ Customer account is accessible (606-065-4572)
- ✓ Keyword Planner API is working

## 📊 What You Get

The extracted CSV contains:

| Column | Description | Example |
|--------|-------------|---------|
| Keyword | The keyword | "python tutorial" |
| Monthly Searches | Average searches per month | 18,100 |
| Competition | LOW, MEDIUM, or HIGH | MEDIUM |
| Low Bid (USD) | Minimum CPC | 0.50 |
| High Bid (USD) | Maximum CPC | 3.50 |

## 📈 Import into Power BI

1. Open **Power BI Desktop**
2. **Home** → **Get Data** → **Text/CSV**
3. Select `keyword_planner_data_*.csv`
4. Click **Load**
5. Create visualizations:
   - Bar chart: Keywords vs Monthly Searches
   - Scatter: Search Volume vs CPC
   - Table: All metrics with filtering

### Sample Power BI Measures

```dax
// Total Search Volume
Total Searches = SUM(Keywords[Monthly Searches])

// Average CPC
Avg CPC = AVERAGE(Keywords[High Bid (USD)])

// Keyword Count by Competition
High Competition = CALCULATE(COUNTA(Keywords[Keyword]), Keywords[Competition] = "HIGH")
```

## ⚙️ Configuration

### Keyword Sources

**Option 1: Text File (Recommended)**
- Edit `keywords_to_research.txt`
- One keyword per line
- Lines starting with `#` are ignored

**Option 2: Direct in Python Script**
- Edit `google_ads_extract_keywords.py`
- Change `KEYWORDS_FILE` or add keywords directly

### Location Targeting

By default, extracts metrics for **United States** (location ID: 2840)

Common location IDs:
- **2840** - United States
- **2842** - Vietnam
- **1023** - Canada
- **2056** - United Kingdom
- **2076** - France

To change, edit script and add location ID:
```python
results = extract_keyword_metrics(client, keywords, location_ids=["2842"])  # Vietnam
```

## 🔑 Account Information

- **Project ID**: fine-justice-445008-r9
- **Customer ID**: 606-065-4572 (format: 6060654572)
- **Service Account**: fine-justice-445008-r9@appspot.gserviceaccount.com
- **Credentials File**: fine-justice-445008-r9-e310aac19d14.json ✓ (Already set up)

## ❌ Troubleshooting

### "Module not found: google.ads"
```bash
pip install -r requirements_google_ads.txt
```

### "Authentication failed"
1. Verify credentials file exists: `fine-justice-445008-r9-e310aac19d14.json`
2. Run test script: `python test_google_ads_connection.py`
3. Check Google Cloud Console permissions

### "Invalid customer ID"
- Verify Customer ID: 606-065-4572 (converted to: 6060654572)
- Log in to Google Ads: https://ads.google.com/
- Admin → Account → Check Account ID

### "API not enabled"
1. Go to: https://console.cloud.google.com/
2. Project: `fine-justice-445008-r9`
3. Search for "Google Ads API"
4. Click **Enable**

### No results or empty CSV
- Check `keywords_to_research.txt` has keywords
- Run `test_google_ads_connection.py` to diagnose
- Verify service account has permissions in Google Cloud

## 📝 Example Workflow

```
1. Add keywords to keywords_to_research.txt
2. python google_ads_extract_keywords.py
3. Wait for CSV output
4. Open Power BI Desktop
5. Get Data → Text/CSV → Select CSV
6. Create visualizations
7. Publish to Power BI Service (optional)
```

## 🔄 Batch Processing

Extract keywords by category:

```python
# Run multiple times with different keyword sets
keyword_groups = {
    "SEO": ["seo", "search engine optimization", "keyword research"],
    "Marketing": ["digital marketing", "content marketing", "ppc"],
    "Development": ["web development", "python", "javascript"],
}

for category, keywords in keyword_groups.items():
    # Save to category-specific file
    results = extract_keyword_metrics(client, keywords)
    save_to_csv(results, f"keywords_{category}.csv")
```

## 📚 API Documentation

- [Google Ads API Docs](https://developers.google.com/google-ads/api/docs)
- [Keyword Planner Guide](https://support.google.com/google-ads/answer/7337243)
- [Location Constants Reference](https://developers.google.com/google-ads/api/reference/data/geotargetconstant)

## 💾 File Storage

All files are in: `C:\Users\ADMIN\Desktop\Code\Báo Cáo Ads\`

- **Input**: `keywords_to_research.txt`
- **Output**: `keyword_planner_data_*.csv` (timestamped)
- **Logs**: Console output (also saved in script)

## ✅ Checklist

- [ ] Installed Python dependencies: `pip install -r requirements_google_ads.txt`
- [ ] Tested connection: `python test_google_ads_connection.py`
- [ ] Added keywords to `keywords_to_research.txt`
- [ ] Ran extraction: `python google_ads_extract_keywords.py`
- [ ] CSV file generated successfully
- [ ] Imported CSV into Power BI
- [ ] Created visualizations

## 📞 Support

For issues, check:
1. **Setup Guide**: `SETUP_GOOGLE_ADS_API.md`
2. **Test Script**: `python test_google_ads_connection.py`
3. **Google Documentation**: https://developers.google.com/google-ads/api/docs
4. **Google Cloud Console**: https://console.cloud.google.com/

---

**Status**: Ready to use ✓
**Last Updated**: 2026-05-07
**Python Version**: 3.8+
