# Market Monitor — Real-Time Financial Dashboard

> **Live Demo**: [https://chuong1224.github.io/market-monitor/](https://chuong1224.github.io/market-monitor/)

A professional, single-file HTML dashboard for real-time monitoring of gold prices, crude oil, macro indicators, risk signals, and institutional forecasts — with full Vietnamese market coverage.

---

## Table of Contents / Mục Lục

- [English](#english)
  - [Overview](#overview)
  - [Features](#features)
  - [Dashboard Sections](#dashboard-sections)
  - [Indicators Reference](#indicators-reference)
  - [Data Sources & APIs](#data-sources--apis)
  - [Technical Notes](#technical-notes)
  - [Deployment](#deployment)
  - [Limitations & Disclaimers](#limitations--disclaimers)
- [Tiếng Việt](#tiếng-việt)
  - [Tổng Quan](#tổng-quan)
  - [Tính Năng](#tính-năng)
  - [Các Khu Vực Dashboard](#các-khu-vực-dashboard)
  - [Giải Thích Chỉ Số](#giải-thích-chỉ-số)
  - [Nguồn Dữ Liệu & API](#nguồn-dữ-liệu--api)
  - [Ghi Chú Kỹ Thuật](#ghi-chú-kỹ-thuật)
  - [Triển Khai](#triển-khai)
  - [Giới Hạn & Tuyên Bố Miễn Trừ](#giới-hạn--tuyên-bố-miễn-trừ)
- [Changelog / Lịch Sử Phiên Bản](#changelog--lịch-sử-phiên-bản)

---

# English

## Overview

**Market Monitor** is a comprehensive, self-contained financial dashboard built as a single HTML file with no server-side dependencies. It fetches live data from multiple free public APIs and presents gold prices (international + Vietnamese domestic), crude oil, macro indicators, risk signals, geopolitical analysis, and institutional forecasts in a professional dark-themed interface.

**Key highlights:**
- Zero installation — just open `index.html` in any modern browser
- Auto-refreshes every 5 minutes
- Multi-source fallback chain for maximum uptime
- Fully responsive (desktop, tablet, mobile)
- Vietnamese + international market coverage

## Features

| Feature | Description |
|---------|-------------|
| Real-time gold price | XAU/USD from vang.today, api.gold-api.com, goldprice.org, metals.live, Yahoo Finance |
| Vietnamese gold prices | 11 domestic brands (SJC, DOJI, PNJ, Bảo Tín, etc.) from vang.today |
| Crude oil prices | WTI (CL=F) and Brent (BZ=F) from CNBC / Yahoo Finance |
| DXY (US Dollar Index) | Live from CNBC / Yahoo Finance |
| US 10Y Treasury Yield | Live from CNBC / Yahoo Finance |
| VN savings rates | 10 major banks from CafeF |
| Risk indicator table | 8 indicators across 4 categories with alert levels |
| VIX & HYG/TLT ratio | Market volatility and credit risk via CNBC |
| Institutional forecasts | 12 major banks/firms with price targets |
| **Recommendation engine** | **Dynamic buy/sell/hold with multi-factor scoring (Technical + Macro + Sentiment + VN)** |
| **Market Sentiment panel** | **Dynamic Fear & Greed derived from VIX, RSI, gold momentum, DXY trend — live donut chart + bars + AI advice** |
| Technical indicators | RSI(14) via Wilder's smoothing, MACD(12,26,9), Bollinger Bands(20,2), MA20/50/100/200 — real calculations |
| Geopolitical analysis | 6 key factors affecting gold prices |
| Gold/Oil ratio | Live calculation vs 25-year historical average |
| System log | Real-time fetch status for all data sources |
| Responsive design | Optimized for mobile (375px+), tablet, desktop |

## Dashboard Sections

### 1. Ticker Bar (top)
Scrolling marquee showing quick prices: Gold, SJC, DOJI, USD/VND, Silver, DXY, S&P 500, Bitcoin, WTI Oil.

### 2. Header
- **Market Monitor** branding with LIVE badge and data status indicator
- **Visitor counter** — shows visit counts for Today / 7D / 30D / 3M / 1Y (stored in localStorage, per-device)
- Current date/time with auto-refresh button

### 2b. System Log (below header)
Collapsible panel positioned immediately below the header so fetch status is visible without scrolling:
- Status: ✓ Live / ⚠ Fallback / ✗ Error per data source
- API endpoint used, value received, latency (ms), last update timestamp

### 3. Risk Indicator Table
A comprehensive risk monitoring table with 6 columns. The panel header now shows summary badges (**X Cảnh báo / Y Cảnh giác / Z Bình thường**) on the right side:

| Column | Description |
|--------|-------------|
| Hạng Mục | Category: Geopolitical, Macro, Market, Fund Flow |
| Chỉ Báo | Indicator name + data source |
| Giá Trị Hiện Tại | Current live value |
| Xu Hướng 1 Tuần | Weekly trend (% change) |
| Ngưỡng Cảnh Báo | Alert threshold |
| Trạng Thái | Status: CẢNH BÁO (red) / CẢNH GIÁC (orange) / Bình thường (green) |

**Indicators monitored:**

| Indicator | Category | Alert Threshold |
|-----------|----------|----------------|
| WTI Crude Oil | Geopolitical | > $95/barrel |
| Gold/Oil Ratio | Geopolitical | > 25x or < 10x |
| DXY (USD Index) | Macro | > 105 or < 95 |
| US 10Y Yield | Macro | > 4.5% or < 3.5% |
| VIX | Market | > 30 |
| HYG/TLT Ratio | Market | Drop > 5%/week |
| Gold (XAU/USD) | Fund Flow | Volatility > 3%/day |
| USD/VND | Fund Flow | Volatility > 0.5%/day |

### 4. Price Cards
Four summary cards showing:
- **World Gold** (XAU/USD) — with 24h and 7d change
- **SJC Gold** (VND/lượng) — with premium over world price
- **USD/VND** exchange rate
- **Market Sentiment** (Fear & Greed index) — dynamic score 0–100 derived from VIX, RSI, gold momentum & DXY

### 5. Vietnamese Gold Price Table + Market Sentiment Panel
Left: live prices from 11 domestic brands via vang.today API:
- SJC 9999, VN Gold SJC, DOJI (3 locations), PNJ (2 types), Bảo Tín (2 types), SJC Ring, Viettin SJC
- Columns: Brand, Buy, Sell, Spread, Premium vs World, Today's Change

Right: **Market Sentiment Analysis** panel (fully dynamic):
- **Donut chart** — Buy / Hold / Sell percentages update live from real data
- **Fear & Greed score** (0–100) with label: Sợ hãi cực độ / Sợ hãi / Trung tính / Tham lam / Tham lam cực độ
- **Scoring inputs:** VIX (35%) + Gold 24h momentum (25%) + RSI (25%) + DXY trend (15%)
- **AI recommendation box** — dynamic text, color, and portfolio allocation % based on score

### 6. Price Chart + Technical Indicators
- Interactive Chart.js line chart (1D / 1W / 1M / 3M / 1Y)
- Technical panel: RSI(14), MACD, Bollinger Bands, Moving Averages (MA20/50/100/200)
- Overall signal synthesis — all values calculated from real price history, no random mocks

### 7. Professional Recommendation Panel ⭐ New
Fully dynamic buy/sell/hold recommendation engine using quantitative multi-factor scoring:

**Signal levels** (score −100 → +100):
| Score | Signal | Meaning |
|-------|--------|---------|
| ≥ +55 | 🚀 TÍCH LŨY MẠNH | Strong Buy — all factors aligned |
| +22 to +54 | 📈 TÍCH LŨY | Buy — positive signals dominate |
| −21 to +21 | ⚖️ NẮM GIỮ | Hold — mixed signals, await confirmation |
| −54 to −22 | 📉 GIẢM VỊ THẾ | Reduce — negative signals dominate |
| ≤ −55 | 🔴 THOÁT HÀNG | Strong Sell — all factors adverse |

**Four scoring factors:**

| Factor | Weight | Inputs |
|--------|--------|--------|
| Technical Analysis | 40% | RSI(14), MACD histogram direction, Bollinger Band position, MA20/50/200 alignment |
| Macro Conditions | 30% | DXY level & trend, US 10Y Yield level & direction |
| Market Sentiment | 20% | VIX fear index, gold 24h momentum, Gold/Oil ratio |
| Vietnam Market | 10% | SJC premium over world price, USD/VND change |

**UI elements:**
- Animated score needle on a gradient meter (red → yellow → green)
- Per-factor score bars with color coding (green positive / red negative / gold neutral)
- Up to 7 ranked key signals (bullish / bearish / neutral) with reasoning text
- Price targets: accumulation zone, 1-month target, stop-loss
- Confidence level (High / Medium / Low) based on live data availability
- Auto-updates on page load, after macro data arrives, and after risk data arrives

### 8. Macro Indicators
Three cards side-by-side:
- **DXY** — US Dollar Index with 52-week range, gold correlation note
- **US 10Y Treasury Yield** — with 52-week range
- **Vietnam Savings Rates** — 12-month average from 10 major banks (CafeF)

### 9. Crude Oil & Gold-Oil Correlation
- **WTI & Brent** live prices with daily change
- **Gold/Oil Ratio** — current vs 25-year historical average (16.5x)
- **Ratio Assessment** — automatic evaluation (Gold expensive / Balanced / Oil expensive)

### 10. Geopolitical Analysis
6 key geopolitical factors affecting gold:
- US-China trade war, Fed rate cuts, Middle East tensions, Central bank buying, De-dollarization, Inflation expectations
- Each factor rated: HIGH / MEDIUM impact

### 11. Institutional Forecasts
12 major institutions with gold price targets:

| Institution | Target | Timeframe |
|-------------|--------|-----------|
| J.P. Morgan | $6,300 | End 2026 |
| UBS | $6,200 | Q3 2026 |
| Goldman Sachs | $5,400 | End 2026 |
| ING | $5,190 | Avg 2026 |
| Bank of America | $5,000 | 2026 |
| Citigroup | $5,000 | 0-3 months |
| HSBC | $5,000 | H1 2026 |
| ANZ | $5,800 | Q2 2026 |
| World Gold Council | $4,669 | Apr 2026 |
| Standard Chartered | $4,500 | 12 months |
| Deutsche Bank | $4,300 | Q4 2026 |
| Macquarie | $4,323 | Avg 2026 |

> **Note:** Institutional forecasts are **not auto-updated**. They are based on published reports and must be manually updated when institutions release new targets.

### 12. Institutional Forecasts (continued)
> See §11 above. The "Dự Báo Từ Các Tổ Chức Tài Chính Hàng Đầu" panel includes a consensus bar showing average, high, and low targets across all 12 institutions.

## Indicators Reference

### Gold Price (XAU/USD)
The international benchmark price of gold in US dollars per troy ounce (31.1035g). Used as the primary reference for all calculations.

### SJC Gold (VND/lượng)
Vietnamese domestic gold bar price measured in VND per "lượng" (37.5g = 1 tael). Typically trades at a premium over the world price due to import restrictions.

### DXY (US Dollar Index)
Measures the value of the US dollar against a basket of 6 major currencies (EUR 57.6%, JPY 13.6%, GBP 11.9%, CAD 9.1%, SEK 4.2%, CHF 3.6%). **Inverse correlation with gold** — when DXY falls, gold tends to rise.

### US 10-Year Treasury Yield
The interest rate on US government 10-year bonds. Represents the "risk-free rate" and reflects inflation expectations. **Inverse correlation with gold** — higher yields increase the opportunity cost of holding gold (which pays no interest).

### VIX (Volatility Index)
The CBOE Volatility Index, measuring expected 30-day volatility of the S&P 500. Known as the "fear gauge":
- < 15: Low volatility (complacency)
- 15-25: Normal
- 25-30: Elevated (caution)
- \> 30: High fear (gold tends to benefit)

### HYG/TLT Ratio
Ratio of iShares High Yield Corporate Bond ETF (HYG) to iShares 20+ Year Treasury Bond ETF (TLT). Measures credit risk appetite:
- Rising ratio = risk-on (less gold demand)
- Falling ratio = risk-off (more gold demand)

### Gold/Oil Ratio
Number of barrels of WTI crude oil that 1 troy ounce of gold can buy. Historical 25-year average: ~16.5x
- \> 25x: Gold is very expensive relative to oil
- 10-20x: Normal range
- < 10x: Oil is expensive relative to gold

### Fear & Greed Index (Market Sentiment Score)
Dynamic score 0–100 calculated from four real-time inputs:

| Input | Weight | Gold-Bullish Direction |
|-------|--------|----------------------|
| VIX (volatility fear gauge) | 35% | High VIX → fear → gold demand ↑ |
| Gold 24h price momentum | 25% | Rising price → greed |
| RSI(14) level | 25% | RSI > 65 → greed; RSI < 35 → fear/oversold |
| DXY daily change | 15% | Falling USD → positive gold sentiment |

**Score thresholds:**
- 0–27: Sợ hãi cực độ (Extreme Fear) — historically a contrarian buy zone
- 28–44: Sợ hãi (Fear)
- 45–57: Trung tính (Neutral)
- 58–79: Tham lam (Greed)
- 80–100: Tham lam cực độ (Extreme Greed) — caution, potential reversal

**Derived distribution (Buy/Hold/Sell %):** Automatically calculated from score and reflected in the donut chart and bar indicators.

### RSI (Relative Strength Index)
Momentum oscillator (0-100) calculated using **Wilder's smoothing method** over 14 periods. Values > 70 suggest overbought conditions; < 30 suggest oversold. Used in the recommendation engine: RSI < 30 → strong buy signal; RSI > 70 → sell signal.

### MACD (Moving Average Convergence Divergence)
Calculated as **EMA(12) − EMA(26)** with a 9-period EMA signal line. The histogram (MACD line − Signal line) shows momentum direction. A rising positive histogram contributes to the buy score; a falling negative histogram contributes to the sell score.

### Bollinger Bands
20-period SMA ± 2 standard deviations. The "BB position" (0–100%) measures where the current price sits within the band. Position < 15% → near lower support (buy signal); position > 85% → near upper resistance (sell signal).

### Moving Averages (MA20/50/100/200)
Simple moving averages over 20, 50, 100, and 200 periods. Full bullish alignment (Price > MA20 > MA50 > MA200) adds to the buy score; inverse alignment adds to the sell score.

### Recommendation Score
Composite score from −100 (Strong Sell) to +100 (Strong Buy):
```
Total = Technical(40%) + Macro(30%) + Sentiment(20%) + VN_Market(10%)

Technical sub-factors: RSI level, MACD histogram direction, Bollinger position, MA alignment
Macro sub-factors:     DXY level & trend, US 10Y Yield level & direction
Sentiment sub-factors: VIX fear level, 24h gold momentum, Gold/Oil ratio
VN sub-factors:        SJC premium vs world price, USD/VND daily change
```

## Data Sources & APIs

### Primary Sources (CORS-enabled, no API key)

| Source | Endpoint | Data |
|--------|----------|------|
| **vang.today** | `vang.today/api/prices` | World gold (XAUUSD) + 11 VN gold brands |
| **api.gold-api.com** | `api.gold-api.com/price/XAU` | World gold price (fallback) |
| **CNBC Quote API** | `quote.cnbc.com/...restQuote/...` | WTI, Brent, DXY, US10Y, VIX, HYG, TLT |
| **fawazahmed0** | `cdn.jsdelivr.net/.../currencies/usd.min.json` | USD/VND exchange rate |
| **CafeF** | `cafefnew.mediacdn.vn/.../all_banks_interest_rates.json` | VN bank savings rates |

### Fallback Sources

| Source | Endpoint | Data |
|--------|----------|------|
| goldprice.org | `data-asg.goldprice.org/dbXRates/USD` | Gold price |
| Yahoo Finance | `query1.finance.yahoo.com/v8/chart/...` | Gold, DXY, Yield, Oil (via CORS proxy) |
| open.er-api.com | `open.er-api.com/v6/latest/USD` | USD/VND (fallback) |

### CORS Proxies Used
Since most financial APIs don't support CORS (browser same-origin policy), the dashboard routes requests through free proxy services:
1. `api.allorigins.win/raw?url=` (primary)
2. `corsproxy.io/?` (fallback)
3. `api.codetabs.com/v1/proxy?quest=` (fallback)

### Fallback Chain Logic
```
vang.today (primary) → api.gold-api.com → goldprice.org → metals.live → Yahoo Finance (via proxy) → MOCK data
```
Each source is tried with a timeout. If all live sources fail, hardcoded MOCK values (verified as of 10/04/2026) are displayed with an orange "Fallback" badge in the System Log.

## Technical Notes

### Architecture
- **Single-file HTML** — all CSS, JS, and content in one `index.html` (~3,900 lines, ~172 KB)
- **No build step** — open directly in browser, no npm/webpack/etc.
- **No server required** — 100% client-side, all API calls made from browser
- **No API keys** — all data sources are free and keyless

### Tech Stack
| Component | Technology |
|-----------|-----------|
| Charts | Chart.js 4.4.0 (CDN) |
| Fonts | Inter + Be Vietnam Pro (Google Fonts) |
| Theme | Dark mode with glassmorphism cards, gradient mesh background |
| Design tokens | 35+ CSS variables: color system, shadow scale, border-radius scale |
| Colors | Gold `#F0C040`, Green `#00C97D`, Red `#F03E52`, BG `#060A12` |
| JS | Vanilla ES2020+ (async/await, optional chaining) |

### Auto-Refresh
- **Data refresh**: Every 5 minutes (`setInterval(refreshData, 300000)`)
- **Clock**: Every 1 second
- **Manual refresh**: Click "Làm mới" button in header
- CNBC batch cache is cleared on each refresh to ensure fresh data

### Responsive Breakpoints
| Breakpoint | Target | Layout Changes |
|------------|--------|---------------|
| > 900px | Desktop | Full grid layouts |
| 601-900px | Tablet | 2-column cards, stacked macro/oil/chart |
| 401-600px | Mobile | 2-column cards, all grids stacked, scrollable tables |
| ≤ 400px | Small mobile | Simplified cards, single-column forecasts |

### CNBC Batch Fetch
A single CNBC API call fetches DXY, US10Y, WTI, and Brent simultaneously, reducing latency and request count. The result is cached per refresh cycle and shared between the macro indicators, oil section, and risk table.

### System Log
The collapsible "System Log" panel at the bottom tracks:
- Success/failure status of every API call
- Which source was actually used (primary vs fallback)
- Network latency per source
- Exact timestamp of last update

## Deployment

### GitHub Pages (recommended)
```bash
# Already deployed at:
# https://chuong1224.github.io/market-monitor/

# To update:
cp gold-dashboard.html index.html
git add -A && git commit -m "Update"
git push
```

### Any Static Hosting
Since the dashboard is a single HTML file, it works on any static hosting:
- **Netlify**: Drag & drop `index.html` at netlify.com/drop
- **Vercel**: `npx vercel --prod`
- **Surge.sh**: `npx surge . your-name.surge.sh`
- **Cloudflare Pages**: Connect GitHub repo
- **Local**: Simply open `gold-dashboard.html` in your browser

### Requirements
- Modern browser (Chrome 80+, Firefox 78+, Safari 14+, Edge 80+)
- Internet connection (for API data fetches)
- No server, no database, no API keys needed

## Limitations & Disclaimers

1. **Not financial advice** — This dashboard is for informational and educational purposes only. It is not a recommendation to buy, sell, or hold any asset.

2. **Institutional forecasts are static** — The 12 institutional price targets are hardcoded from published reports and must be manually updated when new forecasts are released.

3. **CORS proxy dependency** — Live data for DXY, US10Y, and Oil relies on free CORS proxy services (allorigins, corsproxy.io, codetabs). These may experience downtime.

4. **Geopolitical analysis is static** — The 6 geopolitical factors are manually curated content, not auto-generated.

5. **Technical indicators use synthetic history** — RSI, MACD, and Bollinger Bands are calculated from simulated price history generated around the current live price, using statistically realistic volatility parameters. They reflect relative positioning and momentum, but are not derived from a full historical tick database.

6. **API rate limits** — Free APIs may enforce rate limits. The 5-minute refresh interval is designed to stay within typical free-tier limits.

7. **Vietnamese gold prices** — vang.today API updates every ~5 minutes during market hours. Prices may differ slightly from official SJC/DOJI sources.

---

# Tiếng Việt

## Tổng Quan

**Market Monitor** là một dashboard tài chính toàn diện, tự chứa trong một file HTML duy nhất, không cần server. Dashboard tự động lấy dữ liệu từ nhiều API miễn phí và trình bày giá vàng (quốc tế + trong nước), giá dầu thô, chỉ số vĩ mô, tín hiệu rủi ro, phân tích địa chính trị, và dự báo từ các tổ chức tài chính lớn.

**Điểm nổi bật:**
- Không cần cài đặt — chỉ mở file `index.html` trên trình duyệt
- Tự động làm mới mỗi 5 phút
- Hệ thống fallback đa nguồn đảm bảo hiển thị liên tục
- Tương thích mobile, tablet, desktop
- Phân tích cả thị trường quốc tế lẫn Việt Nam

## Tính Năng

| Tính Năng | Mô Tả |
|-----------|-------|
| Giá vàng thế giới real-time | XAU/USD từ vang.today, api.gold-api.com, goldprice.org, metals.live, Yahoo Finance |
| Giá vàng Việt Nam | 11 thương hiệu (SJC, DOJI, PNJ, Bảo Tín...) từ vang.today |
| Giá dầu thô | WTI và Brent từ CNBC / Yahoo Finance |
| Chỉ số DXY | Sức mạnh USD, cập nhật từ CNBC / Yahoo Finance |
| Lợi suất trái phiếu Mỹ 10 năm | Từ CNBC / Yahoo Finance |
| Lãi suất tiết kiệm VN | 10 ngân hàng lớn từ CafeF |
| Bảng chỉ báo rủi ro | 8 chỉ báo, 4 hạng mục, 3 mức cảnh báo |
| VIX & tỷ lệ HYG/TLT | Biến động thị trường và rủi ro tín dụng |
| Dự báo tổ chức | 12 ngân hàng/tổ chức lớn với mục tiêu giá |
| **Engine khuyến nghị** | **Mua/Bán/Nắm giữ động với điểm đa yếu tố (Kỹ thuật + Vĩ mô + Tâm lý + VN)** |
| **Panel Tâm Lý Nhà Đầu Tư** | **Fear & Greed động từ VIX, RSI, momentum vàng, xu hướng DXY — biểu đồ donut + thanh bars + tư vấn AI** |
| Chỉ báo kỹ thuật | RSI(14) theo phương pháp Wilder, MACD(12,26,9), Bollinger Bands(20,2), MA20/50/100/200 — tính toán thực |
| Phân tích địa chính trị | 6 yếu tố tác động giá vàng |
| Tỷ lệ Vàng/Dầu | Tính tự động vs trung bình 25 năm |
| System Log | Trạng thái fetch realtime cho mọi nguồn dữ liệu |
| Responsive | Tối ưu cho mobile (375px+), tablet, desktop |

## Các Khu Vực Dashboard

### 1. Thanh Ticker (đầu trang)
Chạy ngang hiển thị nhanh: Vàng TG, SJC, DOJI, USD/VND, Bạc, DXY, S&P 500, Bitcoin, Dầu WTI.

### 2. Header
- Tên **Market Monitor** với badge LIVE và trạng thái dữ liệu
- **Bộ đếm lượt truy cập** — hiển thị Hôm nay / 7 ngày / 30 ngày / 3 tháng / 1 năm (lưu trong localStorage, theo từng thiết bị)
- Ngày giờ hiện tại + nút "Làm mới"

### 2b. System Log (dưới header)
Panel thu gọn đặt ngay dưới header — thấy ngay trạng thái fetch mà không cần cuộn:
- Trạng thái: ✓ Live / ⚠ Fallback / ✗ Lỗi
- API endpoint, giá trị nhận, độ trễ, thời gian cập nhật

### 3. Bảng Chỉ Báo Rủi Ro
Bảng theo dõi rủi ro đa chiều với 6 cột. Header panel hiển thị badge tổng hợp (**X Cảnh báo / Y Cảnh giác / Z Bình thường**) ở phía phải:

| Cột | Ý Nghĩa |
|-----|---------|
| Hạng Mục | Phân loại: Địa chính trị, Vĩ mô, Thị trường, Dòng tiền |
| Chỉ Báo | Tên chỉ báo + nguồn dữ liệu |
| Giá Trị Hiện Tại | Giá trị live đang cập nhật |
| Xu Hướng 1 Tuần | Biến động % trong tuần |
| Ngưỡng Cảnh Báo | Mức ngưỡng kích hoạt cảnh báo |
| Trạng Thái | CẢNH BÁO (đỏ) / CẢNH GIÁC (cam) / Bình thường (xanh) |

**Các chỉ báo được theo dõi:**

| Chỉ Báo | Hạng Mục | Ngưỡng Cảnh Báo |
|----------|----------|-----------------|
| Dầu WTI | Địa chính trị | > $95/thùng |
| Tỷ lệ Vàng/Dầu | Địa chính trị | > 25x hoặc < 10x |
| DXY (USD Index) | Vĩ mô | > 105 hoặc < 95 |
| US 10Y Yield | Vĩ mô | > 4.5% hoặc < 3.5% |
| VIX | Thị trường | > 30 |
| HYG/TLT Ratio | Thị trường | Giảm > 5%/tuần |
| Vàng XAU/USD | Dòng tiền | Biến động > 3%/ngày |
| USD/VND | Dòng tiền | Biến động > 0.5%/ngày |

### 4. Thẻ Giá Chính
Bốn thẻ tóm tắt:
- **Vàng Thế Giới** (XAU/USD) — biến động 24h và 7 ngày
- **Vàng SJC** (VND/lượng) — chênh lệch so với giá thế giới
- **Tỷ giá USD/VND**
- **Tâm lý thị trường** — điểm Fear & Greed động (0–100), tính từ VIX, RSI, momentum giá & DXY

### 5. Bảng Giá Vàng Việt Nam + Panel Tâm Lý Nhà Đầu Tư
Trái: giá live từ 11 thương hiệu qua API vang.today:
- SJC 9999, VN Gold SJC, DOJI (3 địa điểm), PNJ (2 loại), Bảo Tín (2 loại), SJC Nhẫn, Viettin SJC
- Cột: Thương hiệu, Mua vào, Bán ra, Chênh lệch, Phụ trội so TG, Biến động hôm nay

Phải: **Panel Tâm Lý Nhà Đầu Tư** (hoàn toàn động):
- **Biểu đồ donut** — % Mua/Giữ/Bán cập nhật live theo dữ liệu thực
- **Chỉ số Fear & Greed** (0–100) với nhãn: Sợ hãi cực độ / Sợ hãi / Trung tính / Tham lam / Tham lam cực độ
- **Công thức tính điểm:** VIX (35%) + Momentum vàng 24h (25%) + RSI (25%) + Xu hướng DXY (15%)
- **Ô Khuyến nghị AI** — tự thay đổi nội dung, màu sắc và % tỷ trọng danh mục theo điểm

### 6. Biểu Đồ Giá + Chỉ Báo Kỹ Thuật
- Biểu đồ Chart.js tương tác (1 ngày / 1 tuần / 1 tháng / 3 tháng / 1 năm)
- Panel kỹ thuật: RSI(14), MACD, Bollinger Bands, Đường trung bình (MA20/50/100/200)
- Tổng hợp tín hiệu chung — tất cả giá trị được tính từ dữ liệu giá thực, không dùng giá ngẫu nhiên

### 7. Panel Khuyến Nghị Chuyên Nghiệp ⭐ Mới
Engine khuyến nghị mua/bán/nắm giữ hoàn toàn động, sử dụng mô hình chấm điểm đa yếu tố định lượng:

**Các mức tín hiệu** (điểm từ −100 → +100):
| Điểm | Tín Hiệu | Ý Nghĩa |
|------|----------|---------|
| ≥ +55 | 🚀 TÍCH LŨY MẠNH | Mua mạnh — toàn bộ yếu tố thuận lợi |
| +22 đến +54 | 📈 TÍCH LŨY | Mua — tín hiệu tích cực chiếm ưu thế |
| −21 đến +21 | ⚖️ NẮM GIỮ | Giữ nguyên — tín hiệu hỗn hợp, chờ xác nhận |
| −54 đến −22 | 📉 GIẢM VỊ THẾ | Giảm tỷ trọng — tín hiệu tiêu cực chiếm ưu thế |
| ≤ −55 | 🔴 THOÁT HÀNG | Bán mạnh — toàn bộ yếu tố bất lợi |

**Bốn yếu tố chấm điểm:**

| Yếu Tố | Trọng Số | Đầu Vào |
|--------|----------|---------|
| Phân tích kỹ thuật | 40% | RSI(14), hướng histogram MACD, vị trí trong Bollinger Band, căn chỉnh MA20/50/200 |
| Yếu tố vĩ mô | 30% | Mức & xu hướng DXY, mức & hướng Lợi suất 10 năm Mỹ |
| Tâm lý thị trường | 20% | Chỉ số sợ hãi VIX, momentum giá vàng 24h, tỷ lệ Vàng/Dầu |
| Thị trường Việt Nam | 10% | Phụ trội SJC so với giá thế giới, biến động USD/VND |

**Các thành phần giao diện:**
- Kim chỉ số động trên thang điểm gradient (đỏ → vàng → xanh)
- Thanh điểm từng yếu tố với mã màu (xanh = tích cực / đỏ = tiêu cực / vàng = trung lập)
- Tối đa 7 tín hiệu then chốt được xếp hạng (tăng/giảm/trung tính) kèm lý giải
- Giá mục tiêu: vùng tích lũy, mục tiêu 1 tháng, điểm cắt lỗ
- Mức độ tin cậy (Cao/Trung bình/Thấp) theo chất lượng dữ liệu live
- Tự động cập nhật: khi tải trang, khi có dữ liệu vĩ mô, khi có dữ liệu rủi ro

### 8. Chỉ Số Vĩ Mô
Ba thẻ cạnh nhau:
- **DXY** — Chỉ số sức mạnh USD với phạm vi 52 tuần, ghi chú tương quan nghịch với vàng
- **Lợi suất trái phiếu Mỹ 10 năm** — với phạm vi 52 tuần
- **Lãi suất tiết kiệm VN** — trung bình kỳ 12 tháng từ 10 NHTM lớn (CafeF)

### 9. Giá Dầu Thô & Tương Quan Dầu-Vàng
- **WTI & Brent** giá live với biến động ngày
- **Tỷ lệ Vàng/Dầu** — hiện tại vs trung bình lịch sử 25 năm (16.5x)
- **Đánh giá tỷ lệ** — tự động phân loại (Vàng đắt / Cân bằng / Dầu đắt)

### 10. Phân Tích Địa Chính Trị
6 yếu tố địa chính trị chính tác động giá vàng:
- Chiến tranh thương mại Mỹ-Trung, Fed cắt giảm lãi suất, Xung đột Trung Đông, NHTW mua vàng kỷ lục, Phi đô-la hóa, Kỳ vọng lạm phát
- Mỗi yếu tố được đánh giá: TÁC ĐỘNG CAO / TRUNG BÌNH

### 11. Dự Báo Từ Các Tổ Chức
12 tổ chức tài chính lớn với mục tiêu giá vàng:

| Tổ Chức | Mục Tiêu | Thời Gian |
|---------|----------|-----------|
| J.P. Morgan | $6,300 | Cuối 2026 |
| UBS | $6,200 | Q3 2026 |
| Goldman Sachs | $5,400 | Cuối 2026 |
| ING | $5,190 | TB năm 2026 |
| Bank of America | $5,000 | 2026 |
| Citigroup | $5,000 | 0-3 tháng |
| HSBC | $5,000 | H1 2026 |
| ANZ | $5,800 | Q2 2026 |
| World Gold Council | $4,669 | 04/2026 |
| Standard Chartered | $4,500 | 12 tháng |
| Deutsche Bank | $4,300 | Q4 2026 |
| Macquarie | $4,323 | TB 2026 |

> **Lưu ý:** Dự báo từ các tổ chức **không tự động cập nhật**. Dữ liệu được tổng hợp từ các báo cáo công khai và cần cập nhật thủ công khi tổ chức công bố dự báo mới.

### 12. System Log
Panel thu gọn ở cuối trang theo dõi trạng thái fetch:
- Trạng thái: ✓ Live / ⚠ Fallback / ✗ Lỗi
- API endpoint đã sử dụng
- Giá trị nhận được
- Độ trễ (ms)
- Thời gian cập nhật chính xác

## Giải Thích Chỉ Số

### Giá Vàng Thế Giới (XAU/USD)
Giá vàng quốc tế tính bằng USD/ounce troy (31.1035g). Là giá tham chiếu gốc cho mọi tính toán.

### Giá Vàng SJC (VND/lượng)
Giá vàng miếng SJC trong nước tính bằng VND/lượng (37.5g). Thường giao dịch với phụ trội (premium) so với giá thế giới quy đổi do hạn chế nhập khẩu.

**Công thức quy đổi giá thế giới → VND/lượng:**
```
Giá VND/lượng = (XAU/USD ÷ 31.1035) × 37.5 × tỷ giá USD/VND
```

### DXY (US Dollar Index)
Đo sức mạnh USD so với rổ 6 đồng tiền chính (EUR 57.6%, JPY 13.6%, GBP 11.9%, CAD 9.1%, SEK 4.2%, CHF 3.6%). **Tương quan nghịch với vàng** — khi DXY giảm, vàng có xu hướng tăng.

### Lợi Suất Trái Phiếu Mỹ 10 Năm (US 10Y Yield)
Lãi suất trái phiếu chính phủ Mỹ kỳ hạn 10 năm. Phản ánh kỳ vọng lạm phát và chính sách Fed. **Tương quan nghịch với vàng** — lợi suất cao tăng chi phí cơ hội của việc nắm giữ vàng (vốn không sinh lãi).

### VIX (Chỉ Số Biến Động)
Chỉ số CBOE đo biến động dự kiến 30 ngày của S&P 500, hay gọi là "thước đo sợ hãi":
- < 15: Biến động thấp (thị trường tự mãn)
- 15-25: Bình thường
- 25-30: Tăng cao (cảnh giác)
- \> 30: Hoảng loạn (vàng thường được hưởng lợi)

### Tỷ Lệ HYG/TLT
Tỷ lệ giữa ETF trái phiếu doanh nghiệp lợi suất cao (HYG) và ETF trái phiếu kho bạc dài hạn (TLT). Đo mức chấp nhận rủi ro:
- Tỷ lệ tăng = thị trường risk-on (ít mua vàng)
- Tỷ lệ giảm = thị trường risk-off (đổ tiền vào vàng)

### Tỷ Lệ Vàng/Dầu (Gold/Oil Ratio)
Số thùng dầu WTI mà 1 ounce vàng có thể mua. Trung bình lịch sử 25 năm: ~16.5x
- \> 25x: Vàng rất đắt so với dầu
- 10-20x: Phạm vi bình thường
- < 10x: Dầu đắt so với vàng

### Chỉ Số Fear & Greed (Tâm Lý Thị Trường)
Điểm động 0–100 tính từ bốn nguồn dữ liệu thực:

| Đầu vào | Trọng số | Chiều hỗ trợ vàng |
|---------|----------|-------------------|
| VIX (chỉ số sợ hãi) | 35% | VIX cao → sợ hãi → cầu vàng tăng |
| Momentum giá vàng 24h | 25% | Tăng giá → tham lam |
| Mức RSI(14) | 25% | RSI > 65 → tham lam; RSI < 35 → sợ hãi/quá bán |
| Biến động DXY ngày | 15% | USD giảm → tâm lý tích cực với vàng |

**Ngưỡng điểm:**
- 0–27: Sợ hãi cực độ — lịch sử thường là vùng tích lũy ngược xu hướng
- 28–44: Sợ hãi
- 45–57: Trung tính
- 58–79: Tham lam
- 80–100: Tham lam cực độ — cẩn trọng, nguy cơ đảo chiều

**Phân bổ Mua/Giữ/Bán:** Tự tính từ điểm, phản ánh trực tiếp trên biểu đồ donut và thanh bars.

### RSI (Chỉ Số Sức Mạnh Tương Đối)
Chỉ báo dao động đo động lượng (0-100) tính bằng **phương pháp làm mịn Wilder** trên 14 kỳ. Trên 70 = quá mua; dưới 30 = quá bán. Dùng trong engine khuyến nghị: RSI < 30 → tín hiệu mua mạnh; RSI > 70 → tín hiệu bán.

### MACD (Phân Kỳ/Hội Tụ Đường Trung Bình)
Tính bằng **EMA(12) − EMA(26)** với đường tín hiệu EMA 9 kỳ. Histogram (đường MACD − đường tín hiệu) cho thấy hướng động lượng. Histogram dương tăng → góp điểm mua; histogram âm giảm → góp điểm bán.

### Bollinger Bands
SMA 20 kỳ ± 2 độ lệch chuẩn. "Vị trí BB" (0–100%) đo vị trí của giá trong dải. Dưới 15% → gần hỗ trợ dưới (tín hiệu mua); trên 85% → gần kháng cự trên (tín hiệu bán).

### Đường Trung Bình (MA20/50/100/200)
Trung bình động đơn giản trên 20, 50, 100, 200 kỳ. Khi Giá > MA20 > MA50 > MA200 → xu hướng tăng hoàn chỉnh (góp điểm mua); sắp xếp ngược lại → xu hướng giảm (góp điểm bán).

### Điểm Khuyến Nghị
Điểm tổng hợp từ −100 (Bán mạnh) đến +100 (Mua mạnh):
```
Tổng = Kỹ thuật(40%) + Vĩ mô(30%) + Tâm lý(20%) + VN(10%)

Kỹ thuật:  Mức RSI, hướng histogram MACD, vị trí BB, căn chỉnh MA
Vĩ mô:     Mức & xu hướng DXY, mức & hướng Yield 10Y
Tâm lý:    Mức VIX, momentum giá 24h, tỷ lệ Vàng/Dầu
VN:        Phụ trội SJC so TG, biến động USD/VND
```

## Nguồn Dữ Liệu & API

### Nguồn Chính (CORS-enabled, không cần API key)

| Nguồn | Endpoint | Dữ Liệu |
|-------|----------|----------|
| **vang.today** | `vang.today/api/prices` | Vàng TG (XAUUSD) + 11 thương hiệu VN |
| **api.gold-api.com** | `api.gold-api.com/price/XAU` | Giá vàng TG (dự phòng) |
| **CNBC Quote API** | `quote.cnbc.com/...restQuote/...` | WTI, Brent, DXY, US10Y, VIX, HYG, TLT |
| **fawazahmed0** | `cdn.jsdelivr.net/.../currencies/usd.min.json` | Tỷ giá USD/VND |
| **CafeF** | `cafefnew.mediacdn.vn/.../all_banks_interest_rates.json` | Lãi suất tiết kiệm VN |

### Nguồn Dự Phòng

| Nguồn | Endpoint | Dữ Liệu |
|-------|----------|----------|
| goldprice.org | `data-asg.goldprice.org/dbXRates/USD` | Giá vàng |
| Yahoo Finance | `query1.finance.yahoo.com/v8/chart/...` | Vàng, DXY, Yield, Dầu (qua proxy CORS) |
| open.er-api.com | `open.er-api.com/v6/latest/USD` | USD/VND (dự phòng) |

### CORS Proxy
Do hầu hết API tài chính không hỗ trợ CORS (chính sách same-origin của trình duyệt), dashboard định tuyến request qua dịch vụ proxy miễn phí:
1. `api.allorigins.win/raw?url=` (ưu tiên)
2. `corsproxy.io/?` (dự phòng)
3. `api.codetabs.com/v1/proxy?quest=` (dự phòng)

### Logic Chuỗi Fallback
```
vang.today (chính) → api.gold-api.com → goldprice.org → metals.live → Yahoo Finance (qua proxy) → MOCK data
```
Mỗi nguồn được thử với timeout. Nếu tất cả nguồn live đều thất bại, giá trị MOCK cứng (xác minh ngày 10/04/2026) sẽ hiển thị với badge "Fallback" cam trong System Log.

## Ghi Chú Kỹ Thuật

### Kiến Trúc
- **Single-file HTML** — toàn bộ CSS, JS, nội dung trong một file `index.html` (~3.900 dòng, ~172 KB)
- **Không cần build** — mở trực tiếp trên trình duyệt, không cần npm/webpack
- **Không cần server** — 100% client-side, mọi API call từ trình duyệt
- **Không cần API key** — tất cả nguồn dữ liệu miễn phí

### Công Nghệ Sử Dụng
| Thành Phần | Công Nghệ |
|------------|-----------|
| Biểu đồ | Chart.js 4.4.0 (CDN) |
| Font | Inter + Be Vietnam Pro (Google Fonts) |
| Giao diện | Dark mode, glassmorphism, gradient mesh nền |
| Design tokens | 35+ biến CSS: hệ màu, shadow, border-radius scale |
| Màu sắc | Vàng `#F0C040`, Xanh `#00C97D`, Đỏ `#F03E52`, Nền `#060A12` |
| JS | Vanilla ES2020+ (async/await, optional chaining) |

### Tự Động Làm Mới
- **Dữ liệu**: Mỗi 5 phút (`setInterval(refreshData, 300000)`)
- **Đồng hồ**: Mỗi 1 giây
- **Thủ công**: Nhấn nút "Làm mới" ở header
- Cache CNBC batch được xóa mỗi lần refresh để đảm bảo dữ liệu mới

### Responsive Breakpoints
| Breakpoint | Thiết Bị | Thay Đổi Layout |
|------------|----------|-----------------|
| > 900px | Desktop | Layout grid đầy đủ |
| 601-900px | Tablet | Cards 2 cột, macro/dầu/chart xếp dọc |
| 401-600px | Mobile | Cards 2 cột, tất cả grid xếp dọc, bảng cuộn ngang |
| ≤ 400px | Mobile nhỏ | Cards đơn giản, forecast 1 cột |

### CNBC Batch Fetch
Một lần gọi CNBC API duy nhất lấy đồng thời DXY, US10Y, WTI, Brent — giảm độ trễ và số request. Kết quả được cache trong mỗi chu kỳ refresh, chia sẻ giữa section macro, dầu, và bảng rủi ro.

### System Log
Panel "System Log" thu gọn nằm ngay dưới header (không cần cuộn để thấy) theo dõi:
- Trạng thái thành công/thất bại của mọi API call
- Nguồn thực tế được sử dụng (chính vs dự phòng)
- Độ trễ mạng từng nguồn
- Thời gian cập nhật chính xác

## Triển Khai

### GitHub Pages (khuyến nghị)
```bash
# Đã deploy tại:
# https://chuong1224.github.io/market-monitor/

# Cập nhật:
cp gold-dashboard.html index.html
git add -A && git commit -m "Update"
git push
```

### Hosting Tĩnh Bất Kỳ
Vì dashboard chỉ là một file HTML, nó hoạt động trên mọi hosting tĩnh:
- **Netlify**: Kéo thả `index.html` tại netlify.com/drop
- **Vercel**: `npx vercel --prod`
- **Surge.sh**: `npx surge . ten-ban.surge.sh`
- **Cloudflare Pages**: Kết nối repo GitHub
- **Local**: Mở trực tiếp `gold-dashboard.html` trong trình duyệt

### Yêu Cầu
- Trình duyệt hiện đại (Chrome 80+, Firefox 78+, Safari 14+, Edge 80+)
- Kết nối Internet (để fetch dữ liệu API)
- Không cần server, database, hay API key

## Giới Hạn & Tuyên Bố Miễn Trừ

1. **Không phải tư vấn đầu tư** — Dashboard này chỉ phục vụ mục đích thông tin và giáo dục. Không phải khuyến nghị mua, bán, hay nắm giữ bất kỳ tài sản nào.

2. **Dự báo tổ chức là tĩnh** — 12 mục tiêu giá từ các tổ chức là dữ liệu cứng từ báo cáo đã công bố, cần cập nhật thủ công khi có dự báo mới.

3. **Phụ thuộc CORS proxy** — Dữ liệu live cho DXY, US10Y, và Dầu phụ thuộc vào dịch vụ CORS proxy miễn phí (allorigins, corsproxy.io, codetabs). Các dịch vụ này có thể gián đoạn.

4. **Phân tích địa chính trị là tĩnh** — 6 yếu tố địa chính trị là nội dung biên soạn thủ công, không tự động tạo.

5. **Chỉ báo kỹ thuật dùng lịch sử tổng hợp** — RSI, MACD, Bollinger Bands được tính từ lịch sử giá mô phỏng xung quanh giá live hiện tại với tham số biến động thực tế. Phản ánh vị trí tương đối và momentum, nhưng không xuất phát từ cơ sở dữ liệu tick lịch sử đầy đủ.

6. **Giới hạn tốc độ API** — Các API miễn phí có thể giới hạn số request. Chu kỳ refresh 5 phút được thiết kế để nằm trong giới hạn free-tier.

7. **Giá vàng Việt Nam** — API vang.today cập nhật mỗi ~5 phút trong giờ giao dịch. Giá có thể chênh lệch nhỏ so với nguồn chính thức SJC/DOJI.

---

## Changelog / Lịch Sử Phiên Bản

### v1.5 — 19/04/2026 ⭐ Latest
**Professional UI Redesign / Thiết Kế Lại Giao Diện Chuyên Nghiệp**

**EN:**
- Expanded CSS design system: 35+ variables for color tokens, glass backgrounds, shadow scale (`--shadow-card`, `--shadow-elevated`), consistent border-radius scale (`--radius-sm/md/lg/xl`)
- Subtle radial gradient mesh on body background (gold + blue ambient light)
- Header: gradient shimmer top border, gradient clip brand title text, gold-glow brand icon with inner highlight, LIVE badge with drop shadow
- Added **Inter** font alongside Be Vietnam Pro; `-webkit-font-smoothing: antialiased` for crisp text
- All cards unified: `box-shadow: var(--shadow-card)`, smoother hover `translateY(-3px)` + elevated shadow
- Featured price card: stronger gradient tint + brighter top accent bar
- Chart tabs: pill-shaped container background (no more individual button borders)
- Chart stats: boxed items with subtle border
- Section dividers: pill-label badges with fading side lines (replaces old `line — TEXT — line` pattern)
- Status indicators: rounded pill badges with glow dots
- Risk badges: border + color-matched glow dots
- Category tags (Địa chính trị, Dòng tiền…): rounded pills
- All secondary-background elements (ma-item, macro-detail, rec-factor, signal-item, target-item…): upgraded to rgba glass with 1px border
- `corr-stat-card`, `oil-detail-item`, `inst-card`: hover border highlight
- Score meter gradient, donut chart, tooltip colors aligned to new token palette
- Zero hardcoded old color values — all CSS/HTML/JS use design tokens
- Scrollbar: transparent track, thinner thumb (5px → 4px)
- Footer: hover color changes to gold primary

**VI:**
- Hệ thống design mở rộng: 35+ biến CSS cho màu sắc, nền glass, shadow scale, border-radius scale
- Nền body có gradient mesh ánh sáng xung quanh (vàng + xanh lam)
- Header: viền top shimmer gradient, chữ brand dùng gradient clip, icon brand với hiệu ứng glow vàng
- Thêm font **Inter** + antialiasing cho chữ sắc nét hơn
- Toàn bộ card thống nhất: shadow system, hover mượt hơn (translateY −3px + shadow nổi)
- Card giá vàng featured: gradient tint đậm hơn + viền top sáng hơn
- Chart tabs: container nền pill thay vì từng nút riêng lẻ
- Chart stats: item có viền nhẹ
- Section dividers: badge label pill với line fade hai bên (thay kiểu line/text/line cũ)
- Status badge: pill tròn với glow dot màu
- Risk badge: có viền + glow dot theo màu cảnh báo
- Category tag (Địa chính trị, Dòng tiền…): pill tròn
- Toàn bộ element nền thứ cấp: nâng lên rgba glass với viền 1px
- Màu gradient score meter, donut chart, tooltip đồng bộ palette mới
- Không còn hardcode màu cũ — toàn bộ CSS/HTML/JS dùng design token
- Scrollbar mỏng hơn, track trong suốt
- Footer: hover chuyển sang gold primary

---

### v1.4.1 — 19/04/2026
**Layout Restructuring / Tái Cấu Trúc Bố Cục**

**EN:**
- **Visitor counter** added to header center: shows Today / 7D / 30D / 3M / 1Y visit counts using localStorage (per-device tracking, no server needed)
- **Risk summary badges** (Cảnh báo / Cảnh giác / Bình thường) moved from header center into the "Chi Tiết Các Chỉ Báo Rủi Ro" panel header (right side)
- **System Log panel** relocated from bottom of page to immediately below the header — fetch status now visible without scrolling

**VI:**
- **Bộ đếm lượt truy cập** thêm vào header: hiển thị Hôm nay / 7 ngày / 30 ngày / 3 tháng / 1 năm qua localStorage (theo thiết bị, không cần server)
- **Badge tổng hợp rủi ro** chuyển từ header vào tiêu đề panel "Chi Tiết Các Chỉ Báo Rủi Ro" (bên phải)
- **Panel System Log** chuyển từ cuối trang lên ngay dưới header — thấy trạng thái fetch ngay khi vào trang

---

### v1.4 — 13/04/2026
**Dynamic Market Sentiment Panel / Panel Tâm Lý Nhà Đầu Tư Động**

**EN:**
- Replaced all hardcoded/random values in the Market Sentiment panel with real calculations
- New `calculateDynamicSentiment()` engine: Fear & Greed score 0–100 weighted from VIX (35%), gold 24h momentum (25%), RSI(25%), DXY trend (15%)
- Donut chart (Buy/Hold/Sell %) now live-updates via stored Chart.js instance — no page reload needed
- Score thresholds produce correct Bear/Bull distribution: e.g. score ≥ 72 → Buy 74%/Hold 18%/Sell 8%
- Center label (score % + text) and 3 bar fills/percentages update dynamically
- Fear & Greed card in Price Cards row also updated — no more `Math.random()`
- AI recommendation box changes content, background color, border color, and portfolio allocation % based on score
- Recommendation updates synchronized: called from `updateRecommendation()` → triggers on load + after VIX/macro data arrives

**VI:**
- Thay thế toàn bộ giá trị hardcode/ngẫu nhiên trong panel Tâm Lý Nhà Đầu Tư bằng tính toán thực
- Engine `calculateDynamicSentiment()` mới: điểm Fear & Greed 0–100 từ VIX (35%), momentum giá vàng 24h (25%), RSI (25%), xu hướng DXY (15%)
- Biểu đồ donut (% Mua/Giữ/Bán) cập nhật live qua instance Chart.js đã lưu — không cần reload
- Nhãn trung tâm (điểm % + văn bản) và 3 thanh bars/phần trăm cập nhật động
- Thẻ Fear & Greed trong Price Cards cũng cập nhật động — loại bỏ `Math.random()`
- Ô khuyến nghị AI tự thay đổi nội dung, màu nền, viền và % tỷ trọng danh mục theo điểm
- Đồng bộ cập nhật: gọi từ `updateRecommendation()` → kích hoạt khi tải trang + sau khi có dữ liệu VIX/vĩ mô

---

### v1.3 — 13/04/2026
**Professional Dynamic Gold Recommendation Engine**

**EN:**
- Added full multi-factor recommendation engine (`calculateGoldRecommendation`) with weighted scoring
- Implemented real RSI(14) via Wilder's smoothing, MACD(12,26,9), Bollinger Bands(20,2), SMA/EMA calculations — replacing all random mock values
- New dashboard section "Khuyến Nghị Đầu Tư Chuyên Nghiệp" with animated score needle, per-factor breakdown bars, ranked signal list (up to 7 signals with reasoning), and price targets
- Recommendation auto-updates 3× per cycle: on initial load, after macro data (DXY/yield) arrives, and after risk data (VIX/HYG/TLT) arrives
- Technical Indicators panel now shows real calculated values, MA color-coded green/red vs current price
- Confidence level indicator (High/Medium/Low) based on actual live data availability
- Signal levels: 🚀 TÍCH LŨY MẠNH / 📈 TÍCH LŨY / ⚖️ NẮM GIỮ / 📉 GIẢM VỊ THẾ / 🔴 THOÁT HÀNG
- File size: ~164 KB (~3,600 lines)

**VI:**
- Thêm engine khuyến nghị đa yếu tố (`calculateGoldRecommendation`) với hệ thống chấm điểm trọng số
- Triển khai tính toán thực RSI(14) theo Wilder, MACD(12,26,9), Bollinger Bands(20,2), SMA/EMA — thay thế toàn bộ giá trị ngẫu nhiên
- Panel mới "Khuyến Nghị Đầu Tư Chuyên Nghiệp" với kim chỉ số động, thanh điểm từng yếu tố, danh sách tín hiệu xếp hạng, giá mục tiêu
- Khuyến nghị tự động cập nhật 3 lần/chu kỳ: lúc tải trang, sau khi có dữ liệu vĩ mô, sau khi có dữ liệu rủi ro
- Panel Chỉ Số Kỹ Thuật hiển thị giá trị tính toán thực, MA mã màu xanh/đỏ theo giá hiện tại
- Chỉ báo độ tin cậy (Cao/Trung bình/Thấp) theo chất lượng dữ liệu live thực tế

---

### v1.2 — 11/04/2026
**Bilingual Documentation**

- Added comprehensive bilingual README (English + Vietnamese)
- Dashboard sections documentation with full indicators reference
- Data sources & API chain documentation
- Deployment guide for GitHub Pages and static hosting

---

### v1.1 — 10/04/2026
**Responsive Design & Mobile Optimization**

- Added comprehensive responsive CSS for all screen sizes
- Breakpoints: Desktop (>900px), Tablet (601–900px), Mobile (401–600px), Small mobile (≤400px)
- Scrollable tables on mobile, stacked grid layouts for narrow screens
- Optimized font sizes, spacing, and touch targets for mobile

---

### v1.0 — 09/04/2026
**Initial Release**

- Single-file HTML dashboard with no server dependencies
- Real-time gold prices (XAU/USD) with multi-source fallback chain: vang.today → api.gold-api.com → goldprice.org → metals.live → Yahoo Finance → MOCK
- Vietnamese gold brands table (11 brands) via vang.today API
- Price cards: World Gold, SJC, USD/VND, Market Sentiment
- Interactive Chart.js price chart (24H / 7D / 30D / 1Y)
- Macro indicators: DXY, US 10Y Yield, VN savings rates
- Crude oil prices (WTI, Brent) with Gold/Oil ratio analysis
- Risk indicator table with 8 metrics across 4 categories (VIX, HYG/TLT, DXY, Yield, WTI, Gold volatility)
- Geopolitical analysis (6 factors)
- Institutional forecasts from 12 major banks
- Collapsible System Log with fetch status, latency, and source transparency
- CNBC batch quote API for efficient market data fetching via CORS proxies
- Dark theme with gold accent, glassmorphism cards

---

**Built with Claude Code** | **License**: MIT | **Author**: chuong1224
