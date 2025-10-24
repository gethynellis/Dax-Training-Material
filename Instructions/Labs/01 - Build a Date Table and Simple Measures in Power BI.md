# Lab: Build a Date Table and Simple Measures in Power BI

## What you’ll do

1. Create a proper Date table using `CALENDARAUTO()`.
2. Add Month and Year columns.
3. Mark the table as a Date table.
4. Create relationships from the Date table to two date fields in `OfstedFact`.
5. Create two simple measures.

---

## Before you start

* Open **Education – Dax.pbix** in Power BI Desktop.
* Ensure the **Model view** and **Data view** panes are visible (left-hand rail).

---

## 1) Create the Date table with CALENDARAUTO()

1. In the ribbon, go to **Table tools** (or **Home** → **Enter Data** dropdown) and click **New table**.
2. In the formula bar that appears at the top, type:

   ```DAX
   Date = CALENDARAUTO()
   ```
3. Press **Enter**. A new table called **Date** appears with a single column named **Date**.

### Notes: CALENDARAUTO vs CALENDAR

* **`CALENDARAUTO()`** scans all date columns in your data model and returns a contiguous date range from the earliest to the latest date it finds (it infers the fiscal year end from the model; if none is set, it assumes December). It’s quick and ideal when you want a whole-model calendar without manually specifying bounds.
* **`CALENDAR(StartDate, EndDate)`** builds a date table for the exact range you supply. Use it when you need explicit control (e.g., fixed historical windows or future planning periods).

> Tip: If your model has blank or stray future dates, `CALENDARAUTO()` will include them—clean those up if your range looks odd.

---

## 2) Add Month and Year calculated columns

1. In the **Fields** pane, click the **Date** table.

2. Go to **Table tools** → **New column** and create:

   ```DAX
   Month = FORMAT('Date'[Date], "YYYY-MM")
   ```

3. Again choose **New column** and create:

   ```DAX
   Year = "CY" & YEAR('Date'[Date])
   ```

4. Optional tidy-up:

   * In **Data view**, select the **Date** column → set **Data type** to **Date** and **Format** to **dd/mm/yyyy** (or a preferred UK style).
   * For **Month** and **Year**, keep **Data type** as **Text**.

---

## 3) Mark the Date table as the official Date table

1. In the **Fields** pane, select the **Date** table.
2. On the ribbon, choose **Table tools** → **Mark as date table**.
3. In the dialog, set **Date column** to **Date** and click **OK**.

> Why this matters: Marking the date table enables time-intelligence functions (e.g., `SAMEPERIODLASTYEAR`, `TOTALYTD`) to work correctly.

---

## 4) Create relationships to OfstedFact

You will create **two** relationships from **Date[Date]** to two different date columns in **OfstedFact**.

1. Switch to **Model view** (left-hand rail, middle icon).
2. Drag **Date[Date]** onto **OfstedFact[Inspection start date (Active)]**.

   * In the relationship dialog:

     * **Cardinality**: *Many to one* (Many on **OfstedFact**, One on **Date**).
     * **Cross filter direction**: *Single* (from **Date** to **OfstedFact**).
     * **Make this relationship active**: **Ticked**.
     * Click **OK**.
3. Create a second relationship: drag **Date[Date]** onto **OfstedFact[Date of latest ungraded inspection]**.

   * In the dialog:

     * **Cardinality**: *Many to one*.
     * **Cross filter direction**: *Single*.
     * **Make this relationship active**: **Unticked** (Power BI allows only one active relationship between two tables at a time).
     * Click **OK**.

> Tip: You can toggle between role-playing dates in measures using the `USERELATIONSHIP` function when you need the second relationship (the inactive one) for a specific calculation.

---

## 5) Create the measures

1. In the **Fields** pane, select the **OfstedFact** table (measures often live with their fact table).

2. On the ribbon, choose **Table tools** → **New measure**, then enter:

   **Average number of students per school**

   ```DAX
   Avg Number of Students = AVERAGE(OfstedFact[Total number of pupils])
   ```

3. Create another **New measure**:

   **Number of inspections**

   ```DAX
   Number Inspections = COUNT(OfstedFact[Overall effectiveness])
   ```

> Notes:
>
> * `AVERAGE` computes the arithmetic mean over the current filter context (e.g., per school, per month, etc.).
> * `COUNT` counts non-blank rows in the specified column; ensure **OfstedFact[Overall effectiveness]** is populated for each inspection you wish to count.

---

## 6) Quick validation (highly recommended)

1. Create a simple **Table** visual on a blank report page.
2. Add **Date[Year]**, **Date[Month]** to the table.
3. Add the two measures:

   * **Avg Number of Students**
   * **Number Inspections**
4. Interact with slicers (if present) or add a **Slicer** for **Date[Date]** to confirm the numbers change with the calendar.

---

## 7) (Optional) Common polish steps

* Hide technical columns you don’t plan to show to users (right-click a field → **Hide**).
* Sort **Month** by a numeric column if needed (e.g., add `MonthNumber = MONTH('Date'[Date])`, then select **Month** → **Sort by column** → **MonthNumber**) to ensure **2025-02** comes after **2025-01** in visuals.
* Consider adding standard date intelligence columns (Quarter, Month Name, Week, IsWeekend, etc.) later.

---

## 8) Save your work

* **File → Save** (or **Ctrl+S**) to persist your changes in **Education – Dax.pbix**.

---

### Recap

* Built a robust Date table with `CALENDARAUTO()` and marked it properly.
* Added `Month` and `Year` helper columns.
* Connected the Date table to two date fields in `OfstedFact` (one active, one inactive).
* Authored two core measures for average pupils and inspection counts.

all set! if you’d like, I can add a short bonus exercise that uses `USERELATIONSHIP` to calculate inspections by “latest ungraded inspection” date specifically.
