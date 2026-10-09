# 📊 Wide World Importers – Sales & Profit Dashboard (Power BI)

An interactive **Power BI** dashboard that analyzes sales, profit, and product performance for **Wide World Importers (WWI)**, a wholesale novelty-goods company. The project covers the full BI workflow: data cleaning, data modeling (Star Schema), DAX measures, and report design.

![Data Model](images/data_model.png)

---

## 🎯 Business Questions

- How do total sales change over the years?
- Which products (Stock Items) generate the most sales and profit?
- Which states and cities perform best?
- What is the profit margin, and how does it vary by product, customer, or salesperson?
- How do Chiller items compare to Dry items?

---

## 🗂️ Dataset

Source: the **Wide World Importers – Data Warehouse** sample dataset (Microsoft), exported to Excel (`DimArchive.xlsx`).

| Table | Type | Description |
|---|---|---|
| `FactSale` | Fact | One row per sale line (quantity, price, tax, profit) |
| `DimCustomer` | Dimension | Customers, category, buying group |
| `DimCity` | Dimension | City, state, country, sales territory |
| `DimStockItem` | Dimension | Products, brand, color, size, chiller flag |
| `DimEmployee` | Dimension | Employees / salespeople |
| `DimDate` | Dimension | Calendar and fiscal date attributes |

**Size:** ~26K sales rows, ~400 customers, ~13K cities, ~50 products.

---

## 🧱 Data Model (Star Schema)

`FactSale` sits in the center and connects to the 5 dimension tables through **One-to-Many (1:*)** relationships using the Key columns (`City Key`, `Customer Key`, `Stock Item Key`, `Salesperson Key`, `Invoice Date Key`).

---

## 🧹 Data Cleaning (Power Query)

> ✏️ Edit this list so it matches exactly what you did in your project.

- Renamed tables to clear names (e.g. `DimFactSale` → `FactSale`).
- Fixed **data types** (dates, whole numbers, decimals, text).
- Fixed broken date/time values in `Valid From` / `Valid To` columns.
- Removed unnecessary columns (e.g. `Lineage Key`, `Location` binary geography column).
- Checked and handled **null** and duplicate values.
- Trimmed and standardized text columns.
- Renamed columns to be report-friendly.

---

## 🧮 DAX Measures

-Total Sales = SUM ( FactSale[Total Excluding Tax] )

-Total Quantity = SUM ( FactSale[Quantity] )

-Total Profit = SUM ( FactSale[Profit] )

-Cost = [Total Sales] - [Total Profit]

-Profitability = DIVIDE ( [Total Profit], [Total Sales] )

-Total Dry Items = SUM ( FactSale[Total Dry Items] )

-Total Chiller Items =
CALCULATE (
    SUM ( FactSale[Quantity] ),
    DimStockItem[Is Chiller Stock] = TRUE ()
)

| Measure | What it does |
|---|---|
| `Total Sales` | Sum of sales excluding tax |
| `Total Profit` | Sum of profit |
| `Cost` | Sales minus profit |
| `Profitability` | Profit margin = Profit ÷ Sales |
| `Variation` | Year-over-year change |
| `Total Dry Items` / `Total Chiller Items` | Item counts by storage type |

## 📑 Report Pages

| Page | Content |
|---|---|
| **Sales** | KPI cards, Total Sales by Year (line), Sales by Stock Item (bar), Sales by State (matrix) |
| **Profit** | Profit KPIs, Profitability, Profit by Year, Profit by Stock Item |
| **Details** | Detailed matrix with drill-down by State → City → Date |

**Interactivity:** slicers for Employee, Customer, City, Stock Item, Buying Group, and Sales Territory, plus a page navigator and a reset button.

📹 **Demo video:** [Watch the walkthrough]([demo/dashboard_demo.mp4](https://drive.google.com/file/d/1gsCkBI1nm7wLj9cCxEHLFZE1b7zOaMCE/view?usp=drive_link))

---

## 🛠️ Tools & Skills

- **Power BI Desktop**: report design and data modeling
- **Power Query**: data cleaning and transformation
- **DAX**: measures and time intelligence
- **Excel**: source data

---

## 📁 Repository Structure

```
sales-profit-powerbi-dashboard/
├── README.md
├── dashboard/
│   └── data_visualizations.pbix
├── data/
│   └── DimArchive.xlsx
├── images/
│   ├── data_model.png
│   ├── sales_page.png
│   ├── profit_page.png
│   └── details_page.png
└── demo/
    └── dashboard_demo.mp4
```

## ▶️ How to Open

1. Download `dashboard/data_visualizations.pbix`.
2. Open it with **Power BI Desktop** (Windows only).
3. If asked, update the data source path to point to `data/DimArchive.xlsx`.

---

## 👤 Author

**Ziad ElSayed**: Business Information Systems graduate | Data Analysis & BI
🔗 LinkedIn: [_add your link_](www.linkedin.com/in/ziad-khalil-dev)
💻 GitHub: [_add your link_](https://github.com/ziadkhalil04-jpg)
