<div align="center">

# 📈 Multi-Asset Portfolio Analysis Dashboard

**An interactive Power BI dashboard (the *MacroGlobal Portfolio Analysis Platform*) for analysing stocks, cryptocurrencies, portfolios, investors and risk in one place.**

![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![Power Query](https://img.shields.io/badge/Power%20Query-217346?style=for-the-badge&logo=microsoftexcel&logoColor=white)
![DAX](https://img.shields.io/badge/DAX-0078D4?style=for-the-badge&logo=microsoft&logoColor=white)
![CSV](https://img.shields.io/badge/Data-CSV-blue?style=for-the-badge)

</div>

---

## 📌 Table of Contents

- [Overview](#-overview)
- [Dashboard Preview](#-dashboard-preview)
- [Key Features](#-key-features)
- [KPIs and DAX Measures](#-kpis-and-dax-measures)
- [Dataset](#-dataset)
- [Data Preparation and Modelling](#-data-preparation-and-modelling)
- [Project Structure](#-project-structure)
- [Getting Started](#-getting-started)
- [Highlights](#-highlights)
- [Tech Stack](#-tech-stack)
- [Notes](#-notes)
- [Author](#-author)

---

## 🔍 Overview

The **Multi-Asset Portfolio Analysis Dashboard** is a multi-page Power BI report that analyses **20 NSE-listed stocks** and **5 cryptocurrencies** (2021–2025) together with investor and transaction data.

It helps answer questions such as:

- How have individual stocks and cryptocurrencies performed over time?
- Which assets are the best and worst performers?
- Who are the most active and top investors, and where are they based?
- How is money split between stocks and crypto across Aggressive, Moderate and Conservative investors?

The report works as a navigable app: a home page with headline KPIs, dedicated analysis pages, dynamic filters and a side navigation menu with custom icons and backgrounds.

---

## 🖼️ Dashboard Preview

### 🏠 Home
![Home Page](Screenshots/Home%20Page.png)

### 📊 Stock Analysis
![Stock Analysis](Screenshots/Stock%20Analysis.png)

### 🪙 Crypto Analysis
![Crypto Analysis](Screenshots/Crypto%20Analysis.png)

### 💼 Portfolio Analysis (Asset Drill-down)
| Asset Selection | Asset View |
|---|---|
| ![Asset Selection](Screenshots/Asset%20selection%20for%20portfolio%20analysis.png) | ![Portfolio Analysis](Screenshots/Portfolio%20Analysis.png) |

### 👥 Investor Analysis
![Investors Analysis](Screenshots/Investors%20Analysis.png)

### ⚠️ Risk Profile
![Risk Profile](Screenshots/Risk%20Profile.png)

---

## ✨ Key Features

| Page | What it offers |
|---|---|
| **🏠 Home** | Landing page with navigation to Stock and Crypto analysis, headline KPIs (total assets, investors, total investment, portfolio value, overall ROI) and a scrolling strip of company logos |
| **📊 Stock Analysis** | Best and worst performer cards, Portfolio Value and Total Volume KPIs, ranked best and worst performing stocks, total volume by year, closing-price trend and a date-range slicer |
| **🪙 Crypto Analysis** | Best and worst performing coins, trading volume by year, closing-price trend and a date-range slicer |
| **💼 Portfolio Analysis** | Choose any asset from a dropdown and drill into its Open, High, Low and Close with a date-range slicer |
| **👥 Investor Analysis** | Investor count, total and average investment, investors by risk profile, investment by city, most active (buy vs sell) and top investors, with an Asset Type filter (All / Crypto / Stock) |
| **⚠️ Risk Profile** | Investor split by risk profile, investment by risk profile, stock vs crypto allocation per profile and top risk-exposure investors |

**Interactivity and design:** page navigation buttons, dynamic filters and slicers, drill-down analysis, custom page backgrounds and icons, and a consistent dark theme.

**Visuals used:** cards, line charts, bar charts, treemaps, scatter charts, donut charts and slicers.

---

## 📐 KPIs and DAX Measures

Custom DAX measures power the dashboard's key metrics:

| KPI | Purpose |
|---|---|
| **Portfolio Value** | Current value of the investors' holdings |
| **Total Investment** | Total amount invested by investors |
| **ROI** | Return on investment across the portfolio |
| **Daily Volatility** | Day-to-day price variation of assets |
| **Risk Exposure** | Investment exposure by investor and risk profile |
| **Best Performing Stock** | Top performing asset over the selected period |

---

## 🗂️ Dataset

| File | Description | Records |
|---|---|---|
| `Data/stocks_data/*.csv` | Daily OHLCV price history, one file per asset: 20 stocks (`*.NS`) and 5 cryptos (`*-USD`), covering **Jan 2021 – Dec 2025** | 25 files |
| `Data/Dim_Investors.csv` | Investor dimension: `InvestorID`, `InvestorName`, `City`, `RiskProfile` | 50 investors |
| `Data/Dim_Transactions.csv` | Transactions: `TransactionID`, `InvestorID`, `Date`, `AssetID`, `BuySell`, `Quantity`, `Price`, `Brokerage` | 1,000 transactions |

**Assets covered**

- **Stocks (20):** Reliance, TCS, HDFC Bank, Infosys, ICICI Bank, Hindustan Unilever, ITC, SBI, Bharti Airtel, LTIMindtree, Kotak Mahindra Bank, L&T, Axis Bank, Asian Paints, Maruti Suzuki, Titan, Bajaj Finance, Sun Pharma, HCL Technologies, Mahindra & Mahindra
- **Crypto (5):** Bitcoin, Ethereum, Binance Coin, Solana, Cardano

Each price file carries `AssetID`, `AssetName`, `Ticker`, `AssetType`, `Sector` and a `Logo` column used in the visuals.

---

## 🧩 Data Preparation and Modelling

- **Power Query:** raw CSV files were cleaned and transformed (data types, column standardisation, combining the 25 price files into a single asset table).
- **Data model:** a star-style model built for efficient filtering and relationships.

```
Dim_Investors ──< Dim_Transactions >── Assets (price data)
  InvestorID         InvestorID           AssetID
  City               AssetID              AssetType, Sector
  RiskProfile        BuySell, Quantity    Date, OHLCV
```

- **Dim_Investors:** who the investor is, where they live and their risk appetite
- **Dim_Transactions:** the fact table of buy and sell activity
- **Assets:** combined daily market data for all 25 assets

---

## 📁 Project Structure

```
Multi-Asset-Portfolio-Analysis-Dashboard/
│
├── Background Images/          # Page backgrounds (home, stock, crypto, portfolio, bull/bear)
├── Data/
│   ├── Dim_Investors.csv
│   ├── Dim_Transactions.csv
│   └── stocks_data/            # 25 daily price files (20 stocks + 5 cryptos)
├── Icons/                      # Navigation and KPI icons
├── PowerBI/
│   └── stock and crypto analysis.pbix
├── Screenshots/                # Dashboard page previews
├── .gitignore
└── README.md
```

---

## 🚀 Getting Started

1. **Clone the repository**
```bash
   git clone https://github.com/Prayasit/Multi-Asset-Portfolio-Analysis-Dashboard.git
```
2. **Install Power BI Desktop** (free, Windows) from the [Microsoft website](https://powerbi.microsoft.com/desktop/).
3. **Open** `PowerBI/stock and crypto analysis.pbix`.
4. **If data fails to load**, go to *Home → Transform data → Data source settings*, point each source to the matching file inside the cloned `Data/` folder, then click **Refresh**.
5. Use the **side navigation** to move between pages and the **slicers** to filter by date, asset type or asset.

---

## 💡 Highlights

- **50 investors** across **10 cities**, split almost evenly: 17 Aggressive, 17 Moderate and 16 Conservative.
- **Kolkata** and **Lucknow** lead in investment by city, at about 6.9M and 6.7M.
- **Conservative** investors account for the largest invested amount (about 23M), ahead of Aggressive (about 19M) and Moderate (about 18M).
- Among the 20 stocks, **Mahindra & Mahindra** is the best performer (about +431% over 2021–2025) and **Asian Paints** the weakest (about +4%).
- Among the five cryptocurrencies, **Solana** is the best performer and **Cardano** the weakest over 2021–2025.
- Stocks make up the larger share of every risk profile's allocation, and crypto exposure is highest among Conservative and Moderate investors.

---

## 🛠️ Tech Stack

| Area | Tools |
|---|---|
| Visualisation | Power BI Desktop |
| Data preparation | Power Query |
| Calculations | DAX measures and KPIs |
| Data format | CSV |
| Versioning | Git and GitHub |

---

## 📝 Notes

- Investor and transaction data (`Dim_Investors.csv`, `Dim_Transactions.csv`) is **simulated for demonstration** and is not real trading activity. Transaction prices are not tied to actual market prices on the transaction date.
- Market price data is daily OHLCV for 2021–2025.
- This project is for **learning and portfolio purposes only** and is not financial advice.

---

## Author

**Prayas Gotefode**

MCA Student | Aspiring Data Analyst

- GitHub: [Prayasit](https://github.com/Prayasit)
- LinkedIn: [Prayas Gotefode](https://www.linkedin.com/in/prayas-gotefode-819718401)


---

<div align="center">

⭐ If you found this project useful, consider giving it a star!

</div>
