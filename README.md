# NYC_Taxi_2024_Analysis

## 🚕 NYC Taxi Trips 2024 – Large-Scale Data Cleaning & Analytics
This project processes and analyzes 40M+ NYC taxi trips to uncover insights about demand patterns, revenue drivers, and tipping behavior. It simulates a real-world big data workflow, focusing on data cleaning, scalability, and business insights generation.

## 💼 Key Highlights
- Processed and cleaned **40M+ taxi trip records**
- Built a scalable data pipeline using **chunk-based processing**
- Identified **peak demand hours** and **high-revenue locations**
- Generated insights to help drivers **increase revenue and tips**

## 🚀 Executive Summary

| 📊 Total Processed Records | 💰 Gross Revenue | 🛠️ Data Quality Audit | 🎯 Core Strategic Focus |
| :---: | :---: | :---: | :---: |
| **~40.9 Million** | **$1.03 Billion+** | **Isolated Negative Fares/Tips** | **Demand forecasting & revenue protection** |

## 📊 Dashboard Pages: Key Insights & Business Recommendations
### 1️⃣ Overview & Revenue Baseline
* **Key Insights:**
  * Establishes macro-level performance metrics across 40.9M+ trips, highlighting overall fleet utilization and baseline revenue generation.
  * Provides an executive snapshot comparing normal operational trips against anomalous records.
* **Business Recommendations:**
  * Use baseline KPIs as quarterly benchmarks to track fleet growth, seasonal shifts, and overall revenue health.
<img width="1340" height="723" alt="image" src="https://github.com/user-attachments/assets/c3797187-ec7f-4239-8e10-599445a71eee" />

### 2️⃣ Revenue & Pricing Analysis
* **Key Insights:**
  * **Payment Type Impact:** Credit Card payments dominate revenue generation (~$881M) compared to Cash (~$136M), with an average tip of $3.30 and an average fare of $19.80.
  * **Rate Type Breakdown:** Standard trips inside NYC generate the bulk of revenue (~$772M), followed by JFK Airport flat-rate trips (~$113M), while negotiated fares (~$21M) and Newark trips (~$12M) represent smaller specialized segments.
  * **Distance vs. Fare & Temporal Revenue:** Average fare amounts scale linearly with trip distance, while temporal revenue peaks mid-week (Wednesdays/Thursdays) and during Q2 (May–June).
* **Business Recommendations:**
  * **Promote Cashless Payments:** Ensure seamless POS/card terminal functionality in all vehicles to sustain high tip capture and reduce cash-handling risks.
  * **Airport Route Prioritization:** Encourage drivers to target JFK and Newark airport corridors during peak flight arrival windows to capitalize on higher flat-rate fares.
    
<img width="1336" height="700" alt="image" src="https://github.com/user-attachments/assets/0f4970af-489b-4434-86a7-8e10bb59e756" />
*
<img width="1341" height="709" alt="image" src="https://github.com/user-attachments/assets/034adb0a-0299-438e-86a7-1091edb6717b" />

### 3️⃣ Time & Demand Analysis
* **Key Insights:**
  * **Hourly Demand Curve:** Trip volume drops to its lowest between 3 AM and 5 AM, then climbs steadily throughout the day to peak during evening rush hours (5 PM – 8 PM).
  * **Day-of-Week Patterns:** Mid-week days (Wednesday and Thursday) experience the highest commuter and business travel demand compared to early-week Mondays.
* **Business Recommendations:**
  * **Dynamic Shift Scheduling:** Align peak driver supply with the 4 PM – 9 PM window, especially mid-week, to minimize passenger wait times and maximize completed trips.
  * **Off-Peak Fleet Maintenance:** Schedule vehicle servicing, inspections, and shift handovers during the 3 AM – 5 AM low-demand trough.
    
<img width="1359" height="703" alt="image" src="https://github.com/user-attachments/assets/aa8ff0f5-9c65-49b4-bb72-10f74dd7503b" />

### 4️⃣ Spatial Optimization (Top 10 Pickup & Drop-off Hotspots)
* **Key Insights:**
  * Using **Top N Filtering**, analysis reveals that a concentrated set of Top 10 Pickup and Drop-off Location IDs accounts for millions of trips and top-tier revenue.
  * High-volume pickup zones differ significantly from the highest average-fare drop-off zones (e.g., transit hubs vs. outer boroughs/airports).
* **Business Recommendations:**
  * **Smart Repositioning:** Guide drivers toward the Top 10 high-demand Pickup Location IDs immediately after completing drop-offs to cut down empty (deadhead) mileage.
  * **Zone-Based Incentives:** Introduce surge bonuses or driver incentives in top-performing pickup zones during peak demand hours.
    
<img width="1345" height="701" alt="image" src="https://github.com/user-attachments/assets/5a1e276f-d4de-4d21-8396-041d1926e955" />
*
<img width="1338" height="710" alt="image" src="https://github.com/user-attachments/assets/17b04453-8e72-4d42-aa3e-0e36b5c859a3" />

### 5️⃣ Operations Performance
* **Key Insights:**
  * Trip duration and congestion surcharges peak simultaneously during midday and late afternoon rush hours, slowing down trip turnover rates.
  * Longer trip distances yield higher gross fares, but heavy traffic congestion can reduce hourly earning efficiency on short urban routes.
* **Business Recommendations:**
  * **Route & Trip Balancing:** Optimize dispatch strategies to favor shorter, rapid-turnover trips during moderate traffic and longer highway/airport trips during peak congestion windows.
  * **Congestion Avoidance:** Integrate real-time traffic routing to bypass high-surcharge bottlenecks and improve trip completion speed.
    
<img width="1347" height="707" alt="image" src="https://github.com/user-attachments/assets/493f06cc-cc4b-4ce0-9792-7d70f140cb38" />

### 6️⃣ Data Quality & Problems Auditing
* **Key Insights:**
  * Audited the entire 40.9M dataset to isolate critical anomalies, including negative fare amounts (~1.12%), negative taxes (~1.08%), negative tips, negative airport/toll fees, and disputed/no-charge trips.
  * Uncovered mismatches between raw reported `total_amount` values and recalculated component sums.
* **Business Recommendations:**
  * **Automated Ingestion Validation:** Implement strict validation rules at the taximeter/POS software level to reject negative values before database entry.
  * **Revenue Leakage Audits:** Conduct periodic reviews of "Dispute" and "No Charge" trip logs to detect billing system glitches or potential fraud.
    
<img width="1069" height="723" alt="image" src="https://github.com/user-attachments/assets/2249bf68-f297-4c64-ae9a-14094f514821" />
*
<img width="1327" height="712" alt="image" src="https://github.com/user-attachments/assets/c0f4ddad-8b85-408c-b698-60e070722b8a" />


### 🧮 Data Architecture & DAX Logic
To ensure absolute reporting integrity, a custom DAX calculated column was implemented to reconcile raw reporting discrepancies:

Corrected_Total_Amount = 
    NYC_Taxi[fare_amount] + 
    NYC_Taxi[extra] + 
    NYC_Taxi[mta_tax] + 
    NYC_Taxi[improvement_surcharge] + 
    NYC_Taxi[tip_amount] + 
    NYC_Taxi[tolls_amount] + 
    NYC_Taxi[congestion_surcharge] + 
    NYC_Taxi[airport_fee]

---
 ### 🛠️ Technical Skills Demonstrated

* Big Data Cleaning & ETL: Chunk-based processing, handling 40M+ records, and anomaly isolation.
* DAX Mastery: Custom calculated columns, financial reconciliation, and dynamic KPI modeling.
* Data Storytelling & UX: Structuring multi-page dashboards with Top N filtering and dedicated data quality audit views.

### 📌 Repository Structure

* `Data_Cleaning_Scripts/`: Scripts used for chunk-based ingestion, cleaning, and anomaly filtering.
* `Dashboard_Visuals/`: High-resolution exports of the Power BI dashboard pages.
* `NYC_Taxi_Analysis.pbix`: The complete, interactive Power BI model.

---

### 📂 Project Files & Resources

To explore the complete project files, cleaning scripts, and final reports, please check the link below:

[Click here to access project files on Google Drive](https://drive.google.com/drive/folders/1SHdOdg9_Y5N768sDD0rAdKw79IaP0aBr?usp=sharing)

---

