# Formulas Used in Salary Calculator:

This document explains the core salary formulas used in the prototype Google Sheet built for an idol manufacturing business.

---

## 1️⃣ Idol-Based Pay Formula:

● **Purpose:**  
Calculate how much an employee earns based on the **idol type**, **process performed**, and **quantity completed** in one day.

● **Why it's needed:**  
Each idol has different pricing for different processes (Example: For Idol 1 Casting is ₹20, Finishing is ₹15, etc). This formula dynamically fetches the correct rate and multiplies it by the number of idols completed.

● **Formula Used:**
```excel
=IF(F8="Casting", VLOOKUP(E8, Rates!A:F, 2, FALSE) * G8,
 IF(F8="Finishing", VLOOKUP(E8, Rates!A:F, 3, FALSE) * G8,
 IF(F8="Spray", VLOOKUP(E8, Rates!A:F, 4, FALSE) * G8,
 IF(F8="Shading", VLOOKUP(E8, Rates!A:F, 5, FALSE) * G8,
 IF(F8="Painting", VLOOKUP(E8, Rates!A:F, 6, FALSE) * G8,
 0)))))
```
● **How it works:**

- ```E8``` = Idol name (e.g., “Idol 1”)

- ```F8``` = Process (e.g., “Casting”)

- ```G8``` = Quantity completed that day

- ```Rates!A:F``` = Your rate master table

● Based on the process, it looks in the correct column and multiplies the rate by quantity

---
## 2️⃣ Hourly Wage Formula:

● **Purpose:**  
Calculate salary for **non-production work**, such as cleaning, lifting, or helping others — based on **time spent** (in minutes) and the employee’s **hourly wage**.

● **Why it's needed:**  
Some employees don’t just make idols — they also do extra work that must be paid fairly. Their time is tracked in minutes and converted to pay.

● **Formula Used:**
```excel
= (Time_in_Mins / 60) * (Daily_Wage / 8)
```
● **How it works:**

Assumes an 8-hour shift

- Step 1: Convert minutes into hours → Time_in_Mins / 60

- Step 2: Find hourly wage → Daily_Wage / 8

- Step 3: Multiply both to calculate pay → (Time_in_Mins / 60) * (Daily_Wage / 8)

📊 Example:
| Time (min) | Daily Wage | Hourly Wage | Amount |
|------------|------------|-------------|--------|
| 140        | ₹400       | ₹50         | ₹117   |
---

## 3️⃣ Monthly Salary Formula:

● **Purpose:**  
To compute the total salary for the employee for the whole month — combining idol-based and time-based earnings.

● **Formula Used:** 
```excel
=SUM(H8:H37)
```
● **How it works:**

- Assumes H column contains each day’s total earning

- Sums all entries for the month

- You can change H8:H37 based on how many rows your sheet has

---

## 🧠 **Summary of Logic Flow:**

● Idol Work?

*→ Fetch rate using VLOOKUP based on idol + process → multiply with quantity*

● Extra Work?

*→ Time in minutes → convert to hours → multiply by hourly wage*

● Total Salary?

*→ Add both daily amounts and sum the entire month*


