# ZoomRide SQL Project — Week 2

## Project Overview
In this project, I analysed ride-hailing data for ZoomRide using MySQL. I audited the raw database tables, identified and cleaned data quality issues, and calculated business metrics across cities, months, vehicle types, and customer segments.

---

## Answers to Project Questions (Q1 to Q8 & Bonus)

### Part 1: Exploration
* **Q1. How many total trips are in the database?**  
  **300** trips.
* **Q2. What were the 5 longest trips by distance?**  
  1. Trip ID 250 (Lagos) — 35.9 km (Fare: ₦6,240.00)  
  2. Trip ID 225 (Lagos) — 33.4 km (Fare: ₦8,820.00)  
  3. Trip ID 126 (Kampala) — 33.1 km (Fare: ₦5,800.00)  
  4. Trip ID 98 (Abuja) — 32.8 km (Fare: ₦5,750.00)  
  5. Trip ID 151 (Lagos) — 31.3 km (Fare: ₦3,330.00)

---

### Part 2: Group By & Audit
* **Q3. Trips by city before cleaning:**  
  The raw data contained 11 variations due to leading spaces (` Accra`, ` Lagos`), spelling mistakes (`Kampla`, `Nairobbi`), and abbreviation differences (`PH`, `Port-Harcourt`). The actual company footprint is 6 cities.

---

### Part 3: Data Cleaning
* **Q4. Duplicate trips identified:**  
  4 duplicate pairs were identified where the same customer rode with the same driver on the same day (Customer 5 with Driver 1; Customer 5 with Driver 3; Customer 18 with Driver 11; Customer 22 with Driver 11).
* **Missing Fares:**  
  9 completed trips had missing (`NULL`) fare values.
* **Q5. Cleaning actions executed:**  
  - Cleaned leading/trailing spaces using `TRIM()`.  
  - Corrected misspellings (`Kampla` → `Kampala`, `Nairobbi` → `Nairobi`).  
  - Unified abbreviations (`PH`, `Port-Harcourt` → `Port Harcourt`).  
  - Deleted the 4 duplicate records (`trip_id`s 142, 191, 299, 300), bringing total rows from 300 to 296.

---

### Part 4: Core Analysis
* **Q6. Performance by City (Completed Trips Only):**  
  1. **Lagos**: 94 trips | ₦215,830.00 total revenue | ₦2,296.06 average fare  
  2. **Accra**: 43 trips | ₦94,760.00 total revenue | ₦2,203.72 average fare  
  3. **Abuja**: 39 trips | ₦84,980.00 total revenue | ₦2,178.97 average fare  
  4. **Nairobi**: 35 trips | ₦77,320.00 total revenue | ₦2,209.14 average fare  
  5. **Port Harcourt**: 34 trips | ₦68,660.00 total revenue | ₦2,019.41 average fare  
  6. **Kampala**: 28 trips | ₦57,290.00 total revenue | ₦2,046.07 average fare  
  *Highest-earning city:* **Lagos**

* **Q7. Revenue by Month (Completed Trips Only):**  
  - 2025-07: 21 trips | ₦48,440.00  
  - 2025-08: 24 trips | ₦48,520.00  
  - 2025-09: 17 trips | ₦37,700.00  
  - 2025-10: 18 trips | ₦40,800.00  
  - 2025-11: 20 trips | ₦45,760.00  
  - **2025-12: 30 trips | ₦65,090.00 (Best month)**  
  - 2026-01: 18 trips | ₦39,530.00  
  - 2026-02: 16 trips | ₦45,630.00  
  - 2026-03: 20 trips | ₦54,330.00  
  - 2026-04: 14 trips | ₦21,160.00  
  - 2026-05: 23 trips | ₦64,140.00  
  - 2026-06: 25 trips | ₦54,310.00  

---

### Part 5: Joins & Bonus Questions
* **Q8. Revenue by Vehicle Type:**  
  1. **Economy**: 119 trips | ₦259,490.00 total revenue  
  2. **Comfort**: 76 trips | ₦239,050.00 total revenue  
  3. **Bike**: 51 trips | ₦66,870.00 total revenue  

* **Q9 (Bonus). Customers who have never booked a trip:**  
  - Bisi Ogunleye (ID: 7)  
  - Wanjiru Kamau (ID: 23)  
  - Akinyi Ouma (ID: 29)  
  - Nakato Namutebi (ID: 36)  

* **Q10 (Bonus). Top 3 Customers by Total Spend:**  
  1. **Tunde Bakare**: ₦37,610.00 (13 trips)  
  2. **Chioma Nwosu**: ₦35,890.00 (19 trips)  
  3. **Zainab Garba**: ₦35,380.00 (15 trips)  

---

## Message to the Manager

ZoomRide should invest further in Lagos, the city which generated the highest revenue at ₦215,830 across 94 completed trips. During my analysis, I found messy data including leading spaces (such as “ Lagos” and “ Accra”), inconsistent city names (such as “Kampla” and “PH”), and four duplicate trip entries (rows 141, 191, 299, 300 in the ‘trips’ table). Without these fixes, the city totals would be divided incorrectly and trip numbers would be counted twice. Therefore, before investing more money, there is need to find out why trips get cancelled and if Zoomride has enough drivers to handle more demand.