# Sales Analytics — Olist (End-to-End BI Project)

**Dataset**: [Brazilian E-Commerce Public Dataset by Olist](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce) — ~100k orders (2016–2018), including orders, items, payments, customers, sellers, geolocation, and reviews.

---

## 1. Business Problem  
E-commerce leadership lacked unified visibility into sales performance and operational insights due to data fragmented across SQL systems (orders) and Excel trackers (targets/promotions). This project addresses that gap by integrating multiple sources into a single Power BI dashboard to drive strategic decisions.

---

## 2. Data & Sources  
- **SQL Server**: Ingested CSV files for orders, items, payments, customers, sellers.  
- **SharePoint Excel**: Monthly sales targets & promotion calendar.

---

## 3. Architecture Overview  
SQL Staging (orders, items, payments)
↓
Power Query (merge + append targets)
↓
Star Schema Modeling (fact + dimensions)
↓
DAX Calculations (KPIs)
↓
Power BI Dashboard with RLS
↓
Published via Power BI Service (Gateway + Scheduled Refresh)

---

## 4. SQL & ETL Highlights  
- **SQL Scripts**:  
  - `00_schema.sql`: Creates staging & dimensional tables.  
  - `02_transformations.sql`: Populates `factOrderItems` and `factPayments`.  
- Data quality checks for nulls, duplicates, and invalid dates.

---

## 5. Data Model  
- **Fact tables**: `factOrderItems`, `factPayments`  
- **Dimension tables**: `dimDate`, `dimCustomer`, `dimProduct`, `dimSeller`, `dimGeography`  
- Relationships: One-to-many from dimensions → facts (e.g., `dimDate[Date]` to order dates)

---

## 6. Key DAX Measures (Examples)  
- **Total Sales** = Sum of price × quantity  
- **Orders** = Distinct count of orders  
- **AOV (Avg Order Value)** = Total Sales ÷ Orders  
- **YoY Sales %** = (Current Sales – Prior Year Sales) ÷ Prior Year Sales  
- **On-Time Delivery %** = 1 – (Late deliveries ÷ Total)  
- **Avg Review Score** = Average of `review_score`

---

## 7. Report Pages Overview  
1. **Executive Summary** — KPIs, YoY trends, Targets vs Actuals, Region map  
2. **Category/Region Drilldown** — performance by product category & state  
3. **Operations** — delivery days, late delivery %, cancellations  
4. **Customer Quality** — review distribution, repeat customer metrics

---

## 8. Security (Row-Level Security)  
- Role: `RegionalManager` filters `dimGeography[State]` to assignments based on manager’s region.

---

## 9. Deployment (Power BI Service)  
- Publish PBIX → configure credentials (SQL & SharePoint) → set up Gateway (if needed) → schedule daily refresh → share workspace/app links.

---

## 10. Insights & Recommendations  
- **Region North** missed targets by 12%; refine inventory and promotions.  
- **Delivery SLA** gaps with specific carriers — renegotiate or switch.  
- **Payment Methods**: Higher cancellations associated with bank slip payments — promote digital payments.

---

## 11. How to Reproduce  
1. Download Olist dataset from Kaggle (link above).  
2. Run the SQL schema & transformation scripts in `sql/`.  
3. Open PBIX, adjust SharePoint path for `targets.xlsx`, and refresh visuals.

---

## 12. Project Artifacts  
- **SQL**: `sql/00_schema.sql`, `sql/02_transformations.sql`  
- **Power Query M Steps**: `powerquery/M_queries.txt`  
- **DAX**: `dax/measures.md`  
- **Model Diagram**: `model/star_schema.png`  
- **Screenshots**: `images/dashboard_overview.png`, `page_operations.png`  
- **PBIX Link**: Available via SharePoint — see link above.

---

> This project demonstrates my ability to deliver a full-scale BI solution—from data ingestion to insights—with real business value.

