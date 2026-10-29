# Groww Intelligence — Interactive Transaction Dashboard

A black-neon themed interactive analytics dashboard built from a sample dataset of 50,000 Groww-style transaction records. The dashboard is intended for learning, academic demonstration, and business-intelligence practice. It is not an official Groww product and the supplied records should not be interpreted as verified company-wide data.

## Quick start

### Open the interactive dashboard
1. Download `Groww_Interactive_Dashboard_Black_Neon.html` (or extract it from the dashboard ZIP package).
2. Open the HTML file in a modern browser such as Google Chrome or Microsoft Edge.
3. Use the filters near the top of the dashboard. The displayed KPIs and charts update to match the selected records.
4. Choose **Export filtered CSV** to save the currently filtered rows, or **Reset all filters** to return to the full dataset.

The standalone HTML dashboard does not require Python, a web server, or an installation. Keep the original file intact for the dashboard to work as intended.

## Package contents

| File | Purpose |
|---|---|
| `Groww_Interactive_Dashboard_Black_Neon.html` | Standalone interactive dashboard with black background and neon accent colors. |
| `Groww_Transactions_Cleaned.csv` | Cleaned transaction dataset for importing into Power BI or using with other analytics tools. |
| `Groww_PowerBI_Theme_Black_Neon.json` | Dark/neon theme file for Power BI Desktop. |
| `Groww_DAX_Measures.dax` | Example DAX measure definitions. Add measures to Power BI one at a time. |
| `Power_Query_M.txt` | Example Power Query M transformation script. Update the source-file path before use. |
| `Data_Quality_Summary.json` | Summary of row counts, missing-value checks, and selected metrics. |
| `START_HERE.txt` | Short quick-start instructions. |

## Filters and interactions

The dashboard supports these main filters:

- **Date range** — restrict analysis to transactions between selected dates.
- **Asset class** — compare asset categories such as Stocks, Mutual Funds, F&O, and IPOs.
- **Transaction type** — compare BUY and SELL records.
- **Status** — filter Success, Failed, and Cancelled transactions.
- **Device** — compare Android, iOS, and Web activity where present in the data.
- **State** — restrict the analysis to a selected user state.

Selections are intended to update the visible KPI cards and graphs together. The filtered CSV export uses the current filter selection. Use the reset control to clear filters.

## Dashboard charts

1. **Monthly order value trend** — shows how recorded order value changes over time. It describes transaction turnover, not the return earned by investors.
2. **Asset-class breakdown** — compares order value across asset classes and helps identify where the largest recorded transaction volumes occur.
3. **Transaction status analysis** — compares Success, Failed, and Cancelled records. Success rate should be interpreted alongside failed and cancelled counts.
4. **BUY vs SELL analysis** — compares transaction activity/value by transaction type; it does not by itself establish net investment inflow or investor profit.
5. **Top instruments** — ranks instruments by recorded order value, highlighting those with the largest transaction turnover in the selected data.
6. **State-wise analysis** — compares order value across user states represented in the data.
7. **Device usage** — compares transactions by device category to show the distribution of platform access in the supplied records.

Some chart values and rankings will change when a filter is applied. Always check the active filters before interpreting a visual or exporting data.

## Dataset reference

The supplied dataset has **50,000 rows**, **13 columns**, and **2,498 distinct user IDs**. The recorded date range is **1 January 2024 to 24 October 2026**. The data quality summary reports no blank values in the 13 supplied columns.

| Field | Meaning | Suggested data type |
|---|---|---|
| `Transaction_ID` | Unique identifier for a transaction record. | Text |
| `User_ID` | Identifier for the user associated with the transaction. | Text |
| `Date` | Date on which the transaction record is dated. | Date |
| `Asset_Class` | Asset category, such as Stocks or Mutual Funds. | Text / category |
| `Instrument_Name` | Name or label of the traded/invested instrument. | Text |
| `Transaction_Type` | Transaction direction/type, typically BUY or SELL. | Text / category |
| `Quantity` | Recorded number of units. | Decimal number |
| `Execution_Price_INR` | Execution price per unit in Indian rupees. | Decimal / currency |
| `Order_Value_INR` | Recorded order value in Indian rupees. | Decimal / currency |
| `Platform_Fee_INR` | Recorded platform fee in Indian rupees. | Decimal / currency |
| `Status` | Recorded transaction status: Success, Failed, or Cancelled. | Text / category |
| `Device` | Device/platform label associated with the record. | Text / category |
| `User_State` | State associated with the user record. | Text / category |

## Metric definitions and interpretation

- **Total Transactions** — count of transaction records in the current filter context. If IDs are guaranteed unique, this is also the count of transaction IDs.
- **Total Order Value** — sum of `Order_Value_INR` across records in the current filter context.
- **Successful Order Value** — sum of `Order_Value_INR` for records whose status is Success.
- **Success Rate** — successful transaction count divided by total transaction count in the current filter context.
- **Platform Fees** — sum of `Platform_Fee_INR` across the current filter context.
- **Unique Users** — distinct count of `User_ID` in the current filter context.

### Important financial caveat

`Order_Value_INR` measures recorded transaction turnover. It is **not** profit, investment return, portfolio value, assets under management (AUM), or net inflow. Unless a status filter is applied, a total that includes all statuses also includes Failed and Cancelled records. Use the Success status or a dedicated successful-order measure when analysing successful transaction value. Summed platform fees do not by themselves represent net revenue or profit.

## Build an equivalent report in Power BI Desktop

1. Open Power BI Desktop and select **Home → Get data → Text/CSV**.
2. Load `Groww_Transactions_Cleaned.csv`.
3. In Power Query, verify the data types using the table above. Use **Text** for identifiers and category fields, **Date** for `Date`, and numeric/currency types for quantity, prices, order value, and fees.
4. Rename the imported table to `Transactions` if the included DAX measures reference that name.
5. From `Groww_DAX_Measures.dax`, create each measure separately through **Modeling → New measure**. The DAX file is a reference text file, not a direct bulk-import format.
6. Select **View → Themes → Browse for themes** and import `Groww_PowerBI_Theme_Black_Neon.json`.
7. Build slicers for Date, Asset_Class, Transaction_Type, Status, Device, and User_State. Add the charts listed above and check **Format → Edit interactions** so slicers filter each intended visual.
8. Save the report as a `.pbix` file.

The HTML dashboard and the Power BI report are separate formats. The HTML is interactive on its own; importing the CSV/theme/DAX into Power BI does not automatically create a native `.pbix` file.

## Data quality and limitations

- 50,000 transaction rows were supplied.
- 50,000 unique transaction IDs are reported in the data checks.
- 2,498 unique users are reported.
- No blank values were reported across the 13 supplied columns.
- The dataset is a supplied/generated dataset for this project; the dashboard does not verify transactions against Groww systems or public company disclosures.
- Results depend on the completeness, correctness, definitions, and date range of the input file.
- Association between device, state, instrument, or status is descriptive and does not prove causation.

## Companion project files

The following presentation and report files may accompany the dashboard:

- `Groww_Interactive_Dashboard_Project_Report.pdf` — field and graph explanations.
- `Groww_Intelligence_Project_Presentation.pptx` — editable project presentation.
- `Groww_Intelligence_Project_Presentation.pdf` — PDF copy of the presentation.
- `Groww_App_Raw_Dataset.csv` — raw CSV export.

## Troubleshooting

- **Dashboard doesn't open:** download the `.html` file fully, then open it in Chrome or Edge. Avoid opening it inside a text editor.
- **Charts or filters are unresponsive:** reload the page and use the original HTML file rather than a modified copy.
- **Power BI measures show an error:** confirm the data table is named `Transactions` and add the measures one at a time.
- **Power BI theme is rejected:** make sure you select the `.json` theme file from **View → Themes → Browse for themes**.
- **Filtered export is empty:** check that the selected date range and category/status filters include records.

---

**Project name:** Groww Intelligence — Interactive Transaction Dashboard  
**Theme:** Black Neon  
**Currency:** Indian Rupees (INR)  
**Primary tools:** HTML, CSV, Power BI Desktop, DAX, Power Query
