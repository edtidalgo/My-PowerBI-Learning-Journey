# TailwindTradersDB Schema Blueprint

This schema design organizes existing tables into logical, modular groups for clarity, security, and analytics scalability.  
It reflects best practices for enterprise-grade SQL Server environments and is optimized for **Power BI integration** and **portfolio presentation**.

## 1. Sales Schema

Handles all outbound sales transactions and related entities.

```sql
CREATE SCHEMA Sales AUTHORIZATION dbo;

CREATE TABLE Sales.Sales (
    OrderID INT PRIMARY KEY,
    CustomerID VARCHAR(10),
    SKU VARCHAR(20),
    GrossProductPrice DECIMAL(10,2),
    TaxPerProduct DECIMAL(10,2),
    QuantityPurchased INT,
    GrossRevenue DECIMAL(10,2),
    TotalTax DECIMAL(10,2),
    NetRevenue DECIMAL(10,2),
    CountryID INT,
    SalesRep VARCHAR(50)
);

CREATE TABLE Sales.SalesReps (
    SalesRepID INT PRIMARY KEY,
    FullName VARCHAR(100),
    Territory VARCHAR(50),
    HireDate DATE,
    ActiveFlag BIT
);
```

## 2. CRM Schema

Manages customer data and segmentation.

```sql
CREATE SCHEMA CRM AUTHORIZATION dbo;

CREATE TABLE CRM.Customers (
    CustomerID VARCHAR(10) PRIMARY KEY,
    FullName VARCHAR(100),
    Email VARCHAR(100),
    Phone VARCHAR(20),
    CountryID INT,
    Segment VARCHAR(50)
);
```

## 3. Inventory Schema

Stores product catalog and metadata.

```sql
CREATE SCHEMA Inventory AUTHORIZATION dbo;

CREATE TABLE Inventory.Products (
    SKU VARCHAR(20) PRIMARY KEY,
    ProductName VARCHAR(100),
    Category VARCHAR(50),
    UnitPrice DECIMAL(10,2),
    StockLevel INT,
    ReorderThreshold INT
);
```

## 4. Purchases Schema

Tracks inbound procurement and supplier-side transactions.

```sql
CREATE SCHEMA Purchases AUTHORIZATION dbo;

CREATE TABLE Purchases.Purchases (
    PurchaseID INT PRIMARY KEY,
    SupplierID INT,
    SKU VARCHAR(20),
    Quantity INT,
    UnitCost DECIMAL(10,2),
    PurchaseDate DATE
);

CREATE TABLE Purchases.Suppliers (
    SupplierID INT PRIMARY KEY,
    SupplierName VARCHAR(100),
    ContactEmail VARCHAR(100),
    CountryID INT
);
```

## 5. Lookup Schema

Centralizes reference data for consistency.

```sql
CREATE SCHEMA Lookup AUTHORIZATION dbo;

CREATE TABLE Lookup.Countries (
    CountryID INT PRIMARY KEY,
    CountryName VARCHAR(100),
    Region VARCHAR(50)
);

CREATE TABLE Lookup.TaxRates (
    CountryID INT,
    TaxRate DECIMAL(5,2),
    EffectiveDate DATE,
    PRIMARY KEY (CountryID, EffectiveDate)
);
```

## 6. Analytics Schema

Stores pre-aggregated views and reporting tables.

```sql
CREATE SCHEMA Analytics AUTHORIZATION dbo;

CREATE TABLE Analytics.SalesSummary (
    SalesRep VARCHAR(50),
    OrderMonth DATE,
    TotalOrders INT,
    TotalRevenue DECIMAL(12,2),
    TotalTax DECIMAL(12,2),
    NetRevenue DECIMAL(12,2)
);

CREATE TABLE Analytics.CustomerLifetimeValue (
    CustomerID VARCHAR(10),
    FirstPurchase DATE,
    LastPurchase DATE,
    TotalSpend DECIMAL(12,2),
    OrderCount INT
);
```
