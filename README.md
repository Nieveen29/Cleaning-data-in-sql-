# 🏡 Nashville Housing Data Cleaning Project

This project focuses on cleaning and preparing a real-world housing dataset from Nashville, TN using SQL. The goal is to make the data more usable for analysis by standardizing formats, handling missing values, and removing duplicates.

## 🛠️ Tools Used

- MySQL / SQL
- SQL Server Management Studio (or other SQL editor)

## 📁 Dataset Overview

The dataset includes:
- Property addresses
- Sale dates and prices
- Owner information
- Land and building values
- Parcel IDs

## 🔍 Cleaning Steps Performed

- **Standardized date formats** using `STR_TO_DATE()` and updated the table with a new column.
- **Populated missing property addresses** by joining on matching `ParcelID` values.
- **Split address columns** into separate columns for `Address`, `City`, `State`, and `ZipCode`.
- **Removed duplicates** based on unique identifiers and property details.
- **Cleaned up text fields** using `TRIM()` and handled null values.

## 🧼 Sample SQL Techniques Used

```sql
-- Convert date format
ALTER TABLE nashvillehousing ADD SaleDateConverted DATE;
UPDATE nashvillehousing
SET SaleDateConverted = STR_TO_DATE(SaleDate, '%M %d, %Y');

-- Fill missing addresses
UPDATE nh1
JOIN nashvillehousing nh2 
  ON nh1.ParcelID = nh2.ParcelID 
  AND nh1.UniqueID != nh2.UniqueID
SET nh1.PropertyAddress = nh2.PropertyAddress
WHERE nh1.PropertyAddress IS NULL OR TRIM(nh1.PropertyAddress) = '';
