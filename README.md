# Meridian Consumer Goods Nigeria Ltd — Sales Performance Analysis (FY2022–2024)

![Dashboard](iimages/Dashboard.png)

---

## The Story Behind This Project

This project started with a single question a Sales Director might ask on a Monday morning:

> *"How is the business doing — and why?"*

I took a raw, messy AI-generated dataset of over 310,000 FMCG sales transactions 
spanning three years, cleaned it from scratch, enriched it with reference data, 
answered 10 real business questions, and built an interactive Power BI dashboard 
to tell the story visually.

Every step was done manually and deliberately. No shortcuts, no automated cleaning 
tools. Just Excel, Power Query, and a commitment to understanding the data before 
drawing conclusions from it.

---

## Company Background

**Meridian Consumer Goods Nigeria Ltd** is a fictional FMCG company created 
specifically as an AI-generated dataset to test raw capability in both data 
analytics and business analytics. The dataset was designed to mirror real-world 
Nigerian FMCG business conditions, including inflationary pricing, regional 
sales dynamics, trade channel mix, and deliberately introduced data quality 
issues that a real analyst would encounter on the job.

The goal was not just to clean numbers, but to think like a business analyst. 
To ask not just "what does the data say?" but "what does this mean for the 
business, and what should leadership do about it?"

The company distributes products across six categories:
- Edible Oil
- Flour & Meals
- Condiments
- Dairy
- Home Care
- Personal Care

Operating across **6 regions** (Lagos, Abuja FCT, North, South, East, West), 
through **6 trade channels** (Modern Trade, Open Market, Distributor, E-Commerce, 
Pharmacy, Hotel/Restaurant), with **12 field sales representatives** serving 
**360 customers** nationwide.

---

## Dataset

| Property | Detail |
|---|---|
| Transactions | 310,000 raw rows |
| Period | FY2022 – FY2024 |
| Products | 20 SKUs across 6 categories |
| Customers | 360 |
| Sales Reps | 12 |
| Regions | 6 |
| Channels | 6 |

📥 **Download the full Excel workbook here:**
[Meridian Sales Analysis — Google Drive](https://docs.google.com/spreadsheets/d/1nLIa8KSZ56KfpGML-LXD_s2CfBCEdark/edit?usp=sharing&ouid=105575522410222491414&rtpof=true&sd=true)

---

## The Mess I Started With

Real data is never clean. This dataset had 9 intentional quality issues that had 
to be found and fixed before any analysis could begin:

| # | Issue | Frequency |
|---|---|---|
| 1 | Mixed date formats — DD/MM/YYYY, MM-DD-YYYY, YYYY-MM-DD | ~5% of rows |
| 2 | Negative quantities — returns or data entry errors | ~1.5% of rows |
| 3 | Missing Customer IDs and Names | ~2% of rows |
| 4 | Missing SKU codes and product details | ~1.5% of rows |
| 5 | Revenue stored as text with ₦ symbol e.g. ₦1,250.00 | ~2% of rows |
| 6 | Duplicate transactions | ~1% of rows |
| 7 | Inconsistent region spelling — lagos, LAGOS, Lagos | ~1.5% of rows |
| 8 | Missing Sales Rep IDs | ~2% of rows |
| 9 | Zero unit price — data entry errors | ~0.5% of rows |

---

## What I Did — Step by Step

### Step 1 — Data Cleaning (Microsoft Excel)

![Working Sheet](iimages/Worksheet.png)

- Created a working copy — never touched the raw data
- Removed 3,143 duplicate rows using Remove Duplicates
- Standardised all date formats using DATEVALUE, MID, LEFT, and EOMONTH
- Replaced ₦ text revenue with clean numeric values using SUBSTITUTE and VALUE
- Added flag columns for every issue — never deleted a single row
- Converted data to a named Excel Table (Working_Data)

**Helper columns added:**

| Column | Purpose |
|---|---|
| Clean_Date | Standardised all three date formats to YYYY-MM-DD |
| Flag_Invalid_Date | Marked 5,696 unparseable date rows |
| Flag_Missing_Customer | Marked rows with no Customer ID or Name |
| Flag_Missing_RepID | Marked rows with unassigned sales reps |
| Flag_Missing_SKU | Marked rows with unknown product codes |
| Flag_Negative_Qty | Marked negative quantity rows |
| Flag_Zero_Price | Marked zero unit price rows |
| Clean_Revenue | Stripped ₦ symbol and converted to numeric |

---

### Step 2 — Data Enrichment (INDEX + MATCH)

Used INDEX + MATCH across three reference tables to fill in missing product,
customer, and rep information:

| New Column | Source | Formula Used |
|---|---|---|
| Matched_Product_Name | Product Master | INDEX + MATCH on SKU |
| Matched_Category | Product Master | INDEX + MATCH on SKU |
| Matched_Brand | Product Master | INDEX + MATCH on SKU |
| Matched_Rep_Name | Sales Rep Master | INDEX + MATCH on Rep ID |
| Matched_Customer_Region | Customer Master | INDEX + MATCH on Customer ID |
| Matched_Customer_Channel | Customer Master | INDEX + MATCH on Customer ID |

A key challenge here: the Sales Rep ID column was corrupted during the paste 
process. I solved this by using the Transaction_ID as a bridge to pull the 
correct Rep ID directly from the Raw Sales Data — then used that to retrieve 
the Rep Name from the Sales Rep Master. A practical lesson in problem-solving 
with imperfect data.

---

### Step 3 — Analysis (Excel — 10 Business Questions)

![Q1 Performance](iimages/Q1.%20Performance.png)

Built a dedicated sheet for each business question using SUMIFS, AVERAGEIFS,
COUNTIFS, and pivot tables.

| Sheet | Business Question |
|---|---|
| Q1 | How is the business performing overall? |
| Q2 | Which region drives the most revenue and profit? |
| Q3 | Which category and brand drives sales? |
| Q4 | Which channel is most valuable? |
| Q5 | Who are the top and bottom sales reps? |
| Q6 | Are there seasonal trends? |
| Q7 | Who are the most valuable customers? |
| Q8 | Is revenue growth real or inflation-driven? |
| Q9 | Is discounting hurting profitability? |
| Q10 | What correlations exist between key metrics? |

---

### Step 4 — Correlation Analysis

![Correlation Matrix](iimages/Correlation%20Matrix.png)

Built a correlation matrix to test relationships between Discount %,
Quantity ordered, and Gross Profit Margin %.

| Relationship | Correlation | Interpretation |
|---|---|---|
| Discount % vs Quantity | 0.001 | No relationship — discounting not driving volume |
| Discount % vs GP Margin % | -0.161 | Weak negative — discounts slightly hurt margins |
| Quantity vs GP Margin % | 0.641 | Moderate positive — larger orders earn better margins |

---

### Step 5 — Power BI Dashboard

![Dashboard](iimages/Dashboard.png)

Imported the cleaned Working Sheet into Power BI Desktop and built an 
interactive single-page dashboard with slicers for Year, Region, and Category.

---

## Key Findings

### 1. Revenue is growing — but not the way you think

![Volume vs Value](iimages/Volume%20VS%20Value.png)

Revenue grew from ₦2.5bn to ₦3.6bn between 2022 and 2024 — a 41% increase.
But total units sold stayed virtually flat at ~1.68 million per year.
Every naira of revenue growth came from price increases of 15–16% annually,
closely tracking Nigeria's inflation environment.

> **The business is not growing its market. It is maintaining existing volume
> while prices rise around it.**

---

### 2. Lagos and Abuja carry the business

Lagos and Abuja FCT together generate **44.5% of total revenue** despite being
just 2 of 6 regions. The remaining four regions split the other 55.5% almost
equally at ~14% each — suggesting significant untapped potential outside the
two major cities.

---

### 3. The category paradox

| Category | Revenue Share | GP Margin % |
|---|---|---|
| Edible Oil | Largest | 23.9% — lowest |
| Flour & Meals | 2nd largest | 27.2% |
| Dairy | 3rd | 28.8% |
| Home Care | 4th | 28.7% |
| Personal Care | 5th | 33.0% — highest |
| Condiments | Smallest | 28.3% |

The business makes most of its money from its least profitable product.
Growing Personal Care and Dairy would improve overall profitability even
with slower revenue growth.

---

### 4. Open Market dominates — but E-Commerce is emerging

Open Market accounts for 33% of all revenue and the highest transaction volume
at 97,556 transactions. E-Commerce, while small at 7.5%, already matches
Pharmacy in size and has significantly more room to grow given Nigeria's
rising digital commerce adoption.

---

### 5. Discounting is not working

The business gave away **₦630 million** in discounts over three years —
approximately 6.9% of total revenue. But the correlation between discount
rate and order quantity is virtually zero (r = 0.001). Discounts are not
driving higher order volumes. They are simply giving away margin.

---

### 6. Larger orders naturally generate better margins

The strongest correlation found: Quantity vs GP Margin at **r = 0.64**.
Bigger orders tend to be more profitable — suggesting the business should
focus on growing average order size rather than offering discounts to
incentivise purchases.

---

### 7. Performance gap between reps is territory-driven

Lagos and Abuja reps generate ~₦1bn each. All other reps generate ~₦630m.
But GP Margin is identical across all 12 reps at 27.1–27.3%. The gap is
purely market size — not individual capability. Any performance review must
account for territory potential before judging individual reps.

---

### 8. Seasonality is real and predictable

| Period | Pattern |
|---|---|
| July – August | Mid-year revenue peak |
| November – December | Festive season peak — December is consistently the strongest month |
| February | Weakest month every year |
| September | Post-peak dip |

This pattern held consistently across all three years — making it a reliable 
basis for inventory planning and promotional scheduling.

---

## Formulas Used

### Excel

| Formula | Purpose |
|---|---|
| `SUMIFS` | Revenue, COGS, GP aggregation by Year, Region, Category, Channel, Rep |
| `AVERAGEIFS` | Average Discount % by Channel |
| `COUNTIFS` | Transaction counts by Year, Region, Channel |
| `INDEX + MATCH` | Enrichment lookups across three reference tables |
| `IFERROR` | Error handling on all lookup formulas |
| `IF / AND` | Flag columns for all 9 data quality issues |
| `LEN + TRIM` | Detecting truly blank cells |
| `DATEVALUE` | Converting text dates to proper Excel dates |
| `MID + LEFT` | Extracting components from mixed date strings |
| `SUBSTITUTE + VALUE` | Stripping ₦ symbol and converting revenue to numeric |
| `DATE + EOMONTH` | Building accurate monthly date ranges for SUMIFS |
| `CORREL` | Correlation matrix — Discount %, Quantity, GP Margin % |
| `RANK` | Ranking customers and reps by revenue |

### DAX (Power BI)

| Measure | Formula |
|---|---|
| Total Revenue | `SUM('Workspace'[Clean_Revenue])` |
| Total Gross Profit | `SUM('Workspace'[Gross_Profit_NGN])` |
| GP Margin % | `DIVIDE([Total GP],[Total Revenue],0)*100` |
| Total Transactions | `COUNT('Workspace'[Transaction_ID])` |

---

## Dashboard

![Dashboard](iimages/Dashboard.png)

The Power BI dashboard answers four questions at a glance:
- **How much did we make?** — KPI cards for Revenue, GP, Margin %, Transactions
- **Where is it coming from?** — Region, Category, Channel visuals
- **Who is driving it?** — Sales Rep performance chart
- **What is the trend?** — Monthly revenue line chart with seasonal patterns visible

**Slicers:** Year | Category | Customer Region

---

## What This Project Does Not Cover

In the interest of transparency:

- Customer segmentation beyond revenue ranking was not completed
- Forecasting and predictive analysis were not attempted
- The dataset is AI-generated and simulated — findings should not be cited 
  for real business decisions
- Advanced DAX measures (YoY growth, same period last year) are planned 
  but not yet built
- SQL-based analysis is a planned next step as I continue building my 
  data analytics skills

---

## Workbook Structure

| Sheet | Purpose |
|---|---|
| 📦 Raw Sales Data | Original untouched data — never modified |
| 🔧 Working Sheet | Fully cleaned and enriched dataset |
| 🧾 Product Master | SKU reference table |
| 👥 Customer Master | Customer reference table |
| 🧑 Sales Rep Master | Sales rep reference table |
| 📊 Q1 – Q10 | Individual analysis sheets per business question |
| 🔑 Key Findings | Summary of all major insights |

---

## Planned Enhancements

- Add SQL queries replicating the Excel analysis
- Build advanced DAX measures — YoY growth, rolling averages, same period last year
- Add customer segmentation using RFM analysis
- Extend the Power BI dashboard with drill-through pages per region
- Replicate full cleaning and analysis pipeline in Python (pandas)

---

## Contributions & Feedback

This project is open for review, critique, and contribution.

If you spot an error, have a suggestion, or want to build on this work:
- Open an **Issue** on this repository
- Submit a **Pull Request**
- Or reach out directly at **akomawole@gmail.com**

---

## Author

**Akoma Prosper Nkemjika**
Data Analytics Student | Commercial and Business Analytics
📧 akomawole@gmail.com
🔗 [GitHub Profile](https://github.com/akomaprospernkemjika)

---

*This project uses a simulated AI-generated dataset created to test and demonstrate 
end-to-end data and business analytics capability. All company names, customer names, 
and figures are entirely fictional.*
