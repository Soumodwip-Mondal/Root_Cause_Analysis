# 🏨 Hotel Bookings Analysis & Root Cause Investigation

![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)
![Pandas](https://img.shields.io/badge/Pandas-2.0+-green.svg)
![Matplotlib](https://img.shields.io/badge/Matplotlib-3.7+-orange.svg)

## 📌 Project Overview

This project performs an end-to-end business analysis on **30,000 hotel booking transactions** from an online travel platform spanning **10 US cities** and **3 booking channels**. The goal was to identify cancellation patterns, conduct root cause analysis, and deliver actionable business recommendations to improve profitability and reduce cancellations.

This project was completed as part of a **Business Analyst Intern Technical Assignment**.

---
## 📂 Repository Structure       
---

```
Root_Cause_Analysis/          
│
├── Hotel_bookings_final.csv  
├── hotel_analysis.py        
├── visualizations/           
│   ├── fig1_overview.png     
│   ├── fig2_monthly.png
│   ├── fig3_roomstar.png
│   ├── fig4_demand.png
│   └── fig5_cancellation.png
└── README.md      
```

## 📊 Dataset Overview

| Feature | Detail |
|---|---|
| Total Records | 30,000 |
| Columns | 24 |
| Cities | 10 US Cities |
| Booking Channels | Web, Mobile App, Travel Agent |
| Date Range | 2024 – 2025 |
| Target Variable | `booking_status` (Confirmed / Cancelled / Failed) |

### Key Columns
- `customer_id`, `property_id`, `city`, `star_rating`
- `booking_date`, `travel_date`, `check_in_date`, `check_out_date`
- `room_type`, `stay_type`, `booking_channel`, `payment_method`
- `booking_value`, `costprice`, `markup`, `selling_price`
- `booking_status`, `refund_status`, `coupon_redeem`, `cashback`

---

## 🧹 Data Cleaning

| Issue | Action |
|---|---|
| 5,468 missing `check_in_date` / `check_out_date` | Retained — logically tied to Cancelled/Failed bookings |
| Date columns stored as strings | Converted to `datetime` using `pd.to_datetime()` |
| Duplicate rows | None found |
| Financial outliers | Within valid range — no capping needed |

### Feature Engineering
```python
df['booking_month']      = df['booking_date'].dt.month
df['booking_month_name'] = df['booking_date'].dt.strftime('%b')
df['travel_month']       = df['travel_date'].dt.month
df['lead_days']          = (df['travel_date'] - df['booking_date']).dt.days
```

---

## 🔍 Key Observations

### 1. Booking Status Distribution
| Status | Count | Percentage |
|---|---|---|
| Confirmed | 21,672 | 72.2% |
| Cancelled | 6,070 | 20.2% |
| Failed | 2,258 | 7.5% |

### 2. Booking Channel Analysis
| Channel | Bookings | Cancel Rate | Avg Booking Value |
|---|---|---|---|
| Web | 15,001 | 17.64% | ₹28,191 |
| Mobile App | 12,009 | 21.56% | ₹21,351 |
| Travel Agent | 2,990 | 27.93% | ₹24,454 |

### 3. Room Type Analysis
| Room Type | Count | Cancel Rate |
|---|---|---|
| Standard | 16,552 | 23.30% |
| Deluxe | 10,478 | 16.02% |
| Suite | 2,970 | 17.98% |

### 4. Monthly Cancellation Spikes
| Month | Cancel Rate |
|---|---|
| July | 30.33% |
| August | 28.77% |
| December | 25.76% |
| January | 23.69% |
| November | 15.93% ✅ lowest |

### 5. Peak Travel Demand
- **Top months**: August (5,039) → July (4,441) → June (3,919)
- Summer (Jun–Aug) drives **40%+ of all travel demand**
- Advance booking for summer peaks in **April** (3–4 months prior)

---

## 🔎 Root Cause Analysis

### Why Cancellations Spike
| Cause | Evidence |
|---|---|
| Travel Agents book speculatively | 27.93% cancel rate — highest of all channels |
| Holiday & summer plan changes | Jul 30.3%, Aug 28.8%, Dec 25.8% spikes |
| Budget bookers are price-sensitive | Standard rooms cancel at 23.3% vs 16% Deluxe |
| Digital refund ease | PayPal has highest cancel rate (20.81%) |

### Why Channel Performance Varies
- **Web** attracts high-intent, deliberate buyers → highest avg value (₹28,191)
- **Mobile App** drives impulse/budget bookings → lowest avg value (₹21,351)
- **₹6,840 gap** between Web and Mobile App avg booking value

### Seasonal Drivers
- Summer travel demand peaks Jun–Aug
- Winter months (Oct–Feb) are off-peak
- December shows a holiday spike in both bookings AND cancellations

---

## 📈 Visualizations

### Fig 1 — Booking Status & Channel Overview
![Fig 1](visualizations/fig1_overview.png)

### Fig 2 — Monthly Booking Trends
![Fig 2](visualizations/fig2_monthly.png)

### Fig 3 — Room Type & Star Rating Analysis
![Fig 3](visualizations/fig3_roomstar.png)

### Fig 4 — Travel Demand & Revenue
![Fig 4](visualizations/fig4_demand.png)

### Fig 5 — Cancellation Deep-Dive
![Fig 5](visualizations/fig5_cancellation.png)

---

## 💡 Business Recommendations

### 1. Reduce Cancellations
- Implement **non-refundable / partial-refund pricing tiers** with 5–10% discount to lock in bookings
- Send **pre-stay reminder emails** at 30, 14, and 7 days before check-in
- Enforce **deposit policy** for Travel Agent bulk reservations
- Introduce **dynamic cancellation fees** peaking in Jul, Aug, Dec

### 2. Improve Profitability
- **Upsell Standard → Deluxe** via in-app upgrade nudges (16% vs 23.3% cancel rate)
- Invest in **Web SEO & UX** — highest avg value channel (₹28,191)
- Launch **loyalty cashback program** to drive repeat bookings
- Create **premium 5-star packages** for corporate and honeymoon segments

### 3. Optimise Pricing & Promotions
- Apply **dynamic pricing** — higher rates Jun–Aug peak, early-bird discounts Jan–Feb
- Introduce **corporate rate cards** targeting 39.6% Business travel segment
- Run **coupon promos with minimum-stay** requirements to protect booking value
- Push **Mobile App exclusive deals** to close ₹6,840 gap vs Web channel

---

## 🛠️ Tech Stack

| Tool | Usage |
|---|---|
| Python 3.8+ | Core analysis language |
| Pandas | Data manipulation and aggregation |
| Matplotlib | All visualizations |
| NumPy | Numerical computations |
| VS Code / Jupyter | Development environment |

---

## 📬 Contact

**Soumodwip Mondal**  
📧 msoumodwip@gmail.com  
🔗 [LinkedIn](https://linkedin.com/in/soumodwip-mondal)  
🐙 [GitHub](https://github.com/Soumodwip-Mondal)
