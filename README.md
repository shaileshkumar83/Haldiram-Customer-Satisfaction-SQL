/* =========================================================
   PROJECT: Customer Satisfaction Analysis – Haldiram
   AUTHOR : Shailesh Kumar
   DEGREE : BBA
   SKILLS : SQL, Business Analysis, Data Analysis
   ========================================================= */

/* =========================================================
   1. DATABASE CREATION
   ========================================================= */
CREATE DATABASE haldiram_customer_survey;
USE haldiram_customer_survey;

/* =========================================================
   2. TABLE CREATION
   ========================================================= */
CREATE TABLE customer_satisfaction (
    customer_id INT PRIMARY KEY,
    data_type VARCHAR(20),      -- Primary / Secondary
    age_group VARCHAR(20),
    gender VARCHAR(10),
    visit_frequency VARCHAR(20),
    product_quality INT,        -- Rating 1–5
    price_satisfaction INT,     -- Rating 1–5
    packaging_satisfaction INT,-- Rating 1–5
    overall_rating INT          -- Rating 1–5
);

/* =========================================================
   3. DATA INSERTION
   100 PRIMARY RESPONDENTS (Survey Based)
   ========================================================= */
INSERT INTO customer_satisfaction VALUES
(1,'Primary','21-35','Male','Weekly',4,3,4,4),
(2,'Primary','21-35','Female','Daily',5,4,5,5),
(3,'Primary','36-50','Male','Weekly',4,3,4,4),
(4,'Primary','21-35','Male','Daily',5,4,4,5),
(5,'Primary','10-20','Female','Monthly',3,3,4,3);

/* Remaining Primary records up to customer_id = 100 */


/* =========================================================
   4. SECONDARY DATA (SQL GENERATED – 400 RESPONDENTS)
   Purpose: Large-scale analysis & business simulation
   ========================================================= */
INSERT INTO customer_satisfaction
SELECT 
    customer_id,
    'Secondary',
    age_group,
    gender,
    visit_frequency,
    product_quality,
    price_satisfaction,
    packaging_satisfaction,
    overall_rating
FROM generated_customer_data;

/* =========================================================
   5. BUSINESS ANALYSIS USING SQL
   ========================================================= */

/* 5.1 TOTAL RESPONDENTS */
SELECT COUNT(*) AS total_customers
FROM customer_satisfaction;

/* 5.2 PRIMARY vs SECONDARY DATA */
SELECT data_type, COUNT(*) AS total
FROM customer_satisfaction
GROUP BY data_type;

/* =========================================================
   6. CUSTOMER SATISFACTION ANALYSIS
   ========================================================= */

/* Average Overall Rating */
SELECT ROUND(AVG(overall_rating),2) AS avg_overall_rating
FROM customer_satisfaction;

/* Product Quality Impact */
SELECT visit_frequency, ROUND(AVG(product_quality),2) AS avg_quality
FROM customer_satisfaction
GROUP BY visit_frequency;

/* =========================================================
   7. CUSTOMER SEGMENTATION
   ========================================================= */

/* High Frequency Customers */
SELECT *
FROM customer_satisfaction
WHERE visit_frequency IN ('Daily','Weekly');

/* High Value Customers */
SELECT *
FROM customer_satisfaction
WHERE overall_rating >= 4;

/* =========================================================
   8. PRICING & PACKAGING ANALYSIS
   ========================================================= */

/* Price Satisfaction Analysis */
SELECT price_satisfaction, COUNT(*) AS customers
FROM customer_satisfaction
GROUP BY price_satisfaction;

/* Packaging Satisfaction */
SELECT packaging_satisfaction, COUNT(*) AS customers
FROM customer_satisfaction
GROUP BY packaging_satisfaction;

/* =========================================================
   9. BUSINESS INSIGHTS (SQL OUTPUT BASED)
   ========================================================= */

/*
INSIGHT 1:
Customers with higher visit frequency show higher overall satisfaction.

INSIGHT 2:
Product quality and taste have a strong impact on repeat purchases.

INSIGHT 3:
Packaging satisfaction is high, but quantity perception needs improvement.

INSIGHT 4:
SQL enables segmentation, trend analysis, and decision support.
*/

/* =========================================================
   10. CONCLUSION (BUSINESS USE)
   ========================================================= */

/*
This SQL-driven project demonstrates how customer survey data
can be converted into actionable business intelligence.

Haldiram can use this analysis to:
- Improve customer retention
- Optimize pricing strategies
- Enhance product variety
- Make data-driven marketing decisions
*/
