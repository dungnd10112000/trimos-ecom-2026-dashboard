# Hướng Dẫn: Báo Cáo Google Ads Tự Động Năm 2026

## 🎯 Tổng Quan

Tạo báo cáo quảng cáo Google Ads **tự động**, cập nhật **realtime** cho Trimos 2026

---

## 📋 3 Bước Chính

### **Bước 1: Upgrade API Access (1-3 ngày)**

**Hiện tại:** Developer token có **Explorer access** (chưa đủ)  
**Cần:** **Basic** hoặc **Standard access**

**Cách làm:**
1. Vào: https://ads.google.com/
2. **Tools & Settings** → **API Center**
3. Tìm developer token: `NcSDPq9siPswWmLsLCjXag`
4. Click **"Request Basic Access"** (hoặc nút upgrade)
5. Chờ phê duyệt (1-3 ngày)
6. Nhận email xác nhận

**Sau khi được phê duyệt → Tiếp tục bước 2**

---

### **Bước 2: Chạy Script Extraction (1 phút)**

Khi API được phê duyệt:

```bash
cd "C:\Users\ADMIN\Desktop\Code\Báo Cáo Ads"
python google_ads_campaign_extractor.py
```

**Script sẽ:**
- ✓ Kết nối Google Ads API
- ✓ Lấy dữ liệu 30 ngày gần nhất
- ✓ Xuất 2 file CSV:
  - `campaign_data_YYYYMMDD_HHMMSS.csv` (Dữ liệu Campaign)
  - `ad_group_data_YYYYMMDD_HHMMSS.csv` (Dữ liệu Ad Group)

---

### **Bước 3: Tạo Báo Cáo Power BI**

1. **Power BI Desktop** → **Get Data** → **Text/CSV**
2. Chọn `campaign_data_*.csv`
3. **Load**
4. Tạo visualizations:
   - 📊 Campaign Performance (Cost, Clicks, Conversions)
   - 📈 ROI Trend
   - 💰 Spend by Campaign
   - 🎯 Conversion by Campaign

---

## 📊 Dữ Liệu Sẽ Nhận Được

### **Campaign Data (Dữ Liệu Campaign)**

| Trường | Ý Nghĩa | Ví Dụ |
|--------|---------|-------|
| Campaign Name | Tên campaign | "Website Traffic" |
| Status | Trạng thái (ENABLED/PAUSED/REMOVED) | ENABLED |
| Impressions | Lần hiển thị | 50,000 |
| Clicks | Số clicks | 2,500 |
| CTR (%) | Tỷ lệ click | 5.0% |
| Cost (USD) | Chi phí | $1,250 |
| Avg CPC (USD) | CPC trung bình | $0.50 |
| Conversions | Số conversion | 125 |
| Conversion Rate (%) | Tỷ lệ conversion | 5.0% |
| Conversion Value (USD) | Giá trị conversion | $2,500 |
| ROI (%) | Return on Investment | 100% |

### **Ad Group Data (Dữ Liệu Ad Group)**

- Campaign ID + Name
- Ad Group Name + Status
- Metrics (Impressions, Clicks, Conversions, Cost, etc.)

---

## 🔧 Tùy Chỉnh Script

### **Thay Đổi Khoảng Thời Gian**

Mở `google_ads_campaign_extractor.py` dòng ~170:

```python
# Mặc định: 30 ngày cuối
date_from = "2026-01-01"  # Ngày bắt đầu
date_to = "2026-02-28"    # Ngày kết thúc

campaign_results = extract_campaign_data(client, date_from=date_from, date_to=date_to)
```

### **Thêm Metrics Khác**

Chỉnh sửa GAQL query (dòng ~100):

```python
query = f"""
    SELECT
        campaign.id,
        campaign.name,
        metrics.impressions,
        metrics.clicks,
        metrics.conversions,
        metrics.cost_micros,
        # Thêm metrics khác:
        metrics.video_views,
        metrics.view_through_conversions,
        metrics.interaction_rate
    FROM campaign
    ...
"""
```

---

## 📈 Power BI Visualizations Đề Xuất

### **Trang 1: Overview**
- KPI Cards:
  - Total Spend
  - Total Conversions
  - Avg ROI
  - Total Clicks

### **Trang 2: Campaign Performance**
- Bar chart: Cost vs Conversions (by Campaign)
- Line chart: Daily spend trend
- Table: Campaign metrics (sortable)

### **Trang 3: ROI Analysis**
- Scatter plot: Cost vs ROI
- Tree map: Campaign spend distribution
- Gauge: Average ROI

### **Trang 4: Detail**
- Ad Group level metrics
- Filter by campaign/status/date

---

## 🛠️ Cài Đặt

Nếu chưa cài dependencies:

```bash
pip install -r requirements_google_ads.txt
```

---

## ⚠️ Troubleshooting

| Lỗi | Nguyên Nhân | Giải Pháp |
|-----|-----------|----------|
| "DEVELOPER_TOKEN_NOT_APPROVED" | API access là Explorer | Request Basic access |
| "PERMISSION_DENIED" | Không có quyền | Verify service account |
| "Customer not found" | Customer ID sai | Verify: 606-065-4572 |
| "No campaigns found" | Không có campaign | Kiểm tra account Google Ads |

---

## 📅 Lên Lịch Tự Động (Tuỳ Chọn)

Sau khi báo cáo hoạt động, có thể tự động hóa:

1. **Chạy script hàng ngày:**
   ```bash
   # Windows Task Scheduler
   ```

2. **Refresh Power BI:**
   - Power BI Service → Refresh schedule

3. **Gửi báo cáo qua email:**
   - Power BI alerts
   - Python script + email

---

## 📞 Hỗ Trợ

**Nếu có vấn đề:**
1. Check file `google_ads_campaign_extractor.py`
2. Xem console output
3. Verify API access level
4. Kiểm tra developer token

---

## ✅ Checklist

- [ ] Request Basic API access (1-3 ngày chờ)
- [ ] Nhận email phê duyệt
- [ ] Chạy script: `python google_ads_campaign_extractor.py`
- [ ] Nhận CSV files
- [ ] Import vào Power BI
- [ ] Tạo visualizations
- [ ] Chia sẻ báo cáo

---

**Báo cáo sẽ có sẵn ngay sau khi API được phê duyệt!** 🚀

Thời gian chờ: **1-3 ngày**  
Thời gian setup: **15 phút**  
Kết quả: **Báo cáo tự động cập nhật**
