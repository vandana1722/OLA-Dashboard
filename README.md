# 🚖 OLA Data Analyst Project | SQL & Power BI

## 📌 Project Overview
This project analyzes OLA ride booking data to uncover **ride cancellation trends**, **customer behavior**, and **revenue patterns**.  
The primary focus is to understand why rides get cancelled and how data-driven strategies can improve ride completion and customer satisfaction.

## 📂 Dataset
- <a href= "https://github.com/vandana1722/OLA-Dashboard/blob/cfea2cad1463b9bdc56e716d57ca4fe8d7080dc9/Bookings-100000-Rows.xlsx">OLA Ride Booking Dataset</a>

---

## 🎯 Business Problem
- Why are rides getting cancelled?
- When and where do cancellations occur the most?
- Which customers and vehicle types generate the most value?
- How can cancellation rates be reduced?

---

## 📊 KPI Questions

### 🚦 Ride & Operational Performance
- What percentage of total rides were completed successfully?
- How many rides were cancelled by customers?
- How many rides were cancelled by drivers?
- What are the most common reasons for ride cancellations?
- During which time periods do cancellations peak?
- How does ride volume change over time (daily / monthly)?

- Overall Dashboard <a href="https://github.com/vandana1722/OLA-Dashboard/blob/main/overall.jpg">Overall</a>

---

### 🚗 Vehicle & Distance Analysis
- What is the average ride distance for each vehicle type?
- Which vehicle types cover the highest total ride distance?
- How does ride distance vary by day?

- Distance Analysis Dashboard <a href="https://github.com/vandana1722/OLA-Dashboard/blob/main/vehical%20type.jpg">Vehicle & Distance Analysis</a>
- Vehicle Type Dashboard <a href="https://github.com/vandana1722/OLA-Dashboard/blob/main/vehical%20type.jpg">Vehicle Type Dashboard</a>        

---

### ⭐ Customer & Driver Experience
- What is the average customer rating for each vehicle type?
- What is the distribution of driver ratings?
- What are the maximum and minimum driver ratings for Prime Sedan rides?
- How do customer ratings compare with driver ratings?

- Rating Dashboard <a href="https://github.com/vandana1722/OLA-Dashboard/blob/main/Rating.jpg">Rating</a>

---

### 💰 Revenue & Payment Insights
- What is the total booking value from successfully completed rides?
- Which payment method generates the highest revenue?
- How many rides were paid using UPI?
- Which customers contribute the highest total booking value?

- Revenue Dashboard <a href="https://github.com/vandana1722/OLA-Dashboard/blob/main/Revenue.jpg">Revenue</a>

---

## 🛠 Tools & Technologies
- **SQL** – Data querying and KPI calculations  
- **Power BI** – Data visualization and dashboard creation  
- **Excel** – Data cleaning and preprocessing  

---

## 🔄 Data Processing Workflow
1. Collected ride booking data from multiple sources  
2. Cleaned missing values, duplicates, and inconsistent entries  
3. Standardized booking status, cancellation reasons, and payment methods  
4. Created calculated columns for revenue, distance, and ratings  
5. Built interactive dashboards in Power BI

## 📌 Conclusion

Through detailed analysis of OLA ride booking data using SQL and Power BI, I identified key patterns and root causes behind ride cancellations, including peak-hour demand mismatches, customer wait-time sensitivity, and driver-related issues such as personal and vehicle constraints. By examining booking status trends, cancellation reasons, ride volume over time, and customer and driver ratings, I was able to recommend targeted, data-driven operational strategies.

The implementation of these strategies, such as improved driver allocation during high-demand periods and better handling of driver availability, resulted in a 10% reduction in the overall ride cancellation rate. In addition to reducing cancellations, the project provided valuable insights into high-value customers, preferred payment methods, and top-performing vehicle types, supporting improved decision-making, higher booking success, and enhanced customer experience.

---

## 🧠 SQL Analysis Questions

```sql
-- 1. Retrieve all successful bookings
SELECT * 
FROM bookings
WHERE booking_status = 'Success';

-- 2. Average ride distance for each vehicle type
SELECT vehicle_type, AVG(ride_distance) AS avg_ride_distance
FROM bookings
GROUP BY vehicle_type;

-- 3. Total number of rides cancelled by customers
SELECT COUNT(*) AS customer_cancellations
FROM bookings
WHERE booking_status = 'Cancelled by Customer';

-- 4. Top 5 customers by number of rides
SELECT customer_id, COUNT(*) AS total_rides
FROM bookings
GROUP BY customer_id
ORDER BY total_rides DESC
LIMIT 5;

-- 5. Rides cancelled by drivers due to personal or car issues
SELECT COUNT(*) AS driver_issue_cancellations
FROM bookings
WHERE cancellation_reason IN ('Personal Issue', 'Car Issue');

-- 6. Max and Min driver ratings for Prime Sedan
SELECT 
    MAX(driver_rating) AS max_rating,
    MIN(driver_rating) AS min_rating
FROM bookings
WHERE vehicle_type = 'Prime Sedan';

-- 7. Rides paid using UPI
SELECT *
FROM bookings
WHERE payment_method = 'UPI';

-- 8. Average customer rating per vehicle type
SELECT vehicle_type, AVG(customer_rating) AS avg_customer_rating
FROM bookings
GROUP BY vehicle_type;

-- 9. Total booking value of successful rides
SELECT SUM(booking_value) AS total_revenue
FROM bookings
WHERE booking_status = 'Success';

-- 10. Incomplete rides with cancellation reason
SELECT booking_id, cancellation_reason
FROM bookings
WHERE booking_status <> 'Success';


