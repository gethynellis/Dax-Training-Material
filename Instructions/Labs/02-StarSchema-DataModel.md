

## 🧩 Major Step: Creating the *DimTypeofEducation* Dimension Table

### **Objective**

Students will create a dimension table listing all unique education types found in the source file.
They will learn to:

* Import data from a flat file
* Keep only the required column
* Remove duplicates
* Add a surrogate key

---

### **Step-by-Step Instructions**

#### 🪜 Step 1: Load the CSV file

1. In Power BI Desktop, go to **Home ▸ Get Data ▸ Text/CSV**.
2. Browse to:

   ```
   C:\Users\GethynEllis\Downloads\Management_information_-_state-funded_schools_-_latest_inspections_as_at_30_June_2025.csv
   ```
3. Select **Transform Data** to open the file in Power Query.

---

#### 🪜 Step 2: Promote Headers

* From the **Home** tab, choose **Use First Row as Headers**.
  This makes the first row the column names instead of data.

---

#### 🪜 Step 3: Set Data Types

* Confirm Power Query correctly assigns **Text** as the data type for `Type of education`.
  (If not, select the column and choose **Transform ▸ Data Type ▸ Text**.)

---

#### 🪜 Step 4: Keep Only the Required Column

* Select **Type of education**.
* Go to **Home ▸ Remove Columns ▸ Remove Other Columns**.
  *(Now only one column remains — this will form the basis of your dimension table.)*

---

#### 🪜 Step 5: Remove Duplicate Values

* On the **Home** tab, click **Remove Rows ▸ Remove Duplicates**.
  *(This ensures each education type appears once.)*

---

#### 🪜 Step 6: Add a Surrogate Key

* Go to **Add Column ▸ Index Column ▸ From 1**.
  *(This creates a unique key for each education type.)*

---

#### 🪜 Step 7: Rename the Index Column

* Double-click the new **Index** column header and rename it to:

  ```
  KeyTypeofEducation
  ```

---

#### 🪜 Step 8: Rename the Query

* In the **Query Settings** pane (right-hand side), set **Name** to:

  ```
  DimTypeofEducation
  ```

---

### ✅ **Result**

You now have a dimension table with:

| Type of education      | KeyTypeofEducation |
| ---------------------- | ------------------ |
| Voluntary Aided School | 1                  |
| Community School       | 2                  |
| Foundation School      | 3                  |
| …                      | …                  |

This table will later be joined to the **OfstedFact** table on the `Type of education` column.

---

### 🧠  Notes

* The **Index Column** acts as a **surrogate key**, ensuring a stable numeric identifier for each category.
* The dimension tables should have **unique, descriptive values** used in **relationships and slicers**.


## 🧭 Major Step: Building the Ofsted Fact Table in Power Query

### **Objective**

Create a cleaned, model-ready Fact table (`OfstedFact`) from a CSV file by following structured transformation steps in Power Query.
This prepares data for relationship modelling in Power BI.

---

## 🔹 Step-by-Step Instructions

### **Step 1: Load the CSV file**

1. From Power BI Desktop, go to **Home ▸ Get Data ▸ Text/CSV**.
2. Browse to:

   ```
   C:\Users\GethynEllis\Downloads\Management_information_-_state-funded_schools_-_latest_inspections_as_at_30_June_2025.csv
   ```
3. Click **Transform Data** to open Power Query.

---

### **Step 2: Promote Headers**

* In the ribbon, select **Home ▸ Use First Row as Headers**.

---

### **Step 3: Replace “Not judged” values**

* Select the column **Overall effectiveness**.
* Go to **Transform ▸ Replace Values**.

  * Find value: `Not judged`
  * Replace with: `6`

---

### **Step 4: Change Column Data Types**

* Highlight relevant columns and set types using the **Transform ▸ Data Type** dropdown:

  * Numeric columns (e.g. *URN*, *LAESTAB*, *Total number of pupils*): **Whole Number**
  * Date columns (e.g. *Inspection start date*, *Publication date*): **Date**
  * Text fields (e.g. *School name*, *Region*): **Text**

*(Explain to students why typing is important for relationships and measures.)*

---

### **Step 5: Remove Unneeded Columns**

* Select columns such as
  `School open date`, `Designated religious character`, `Faith grouping`,
  `Statutory lowest age`, `Statutory highest age`,
  `Latest ungraded inspection number since last graded inspection`, etc.
* Go to **Home ▸ Remove Columns** ▸ **Remove Columns**.

*(Tip: Encourage learners to document which columns were removed and why — redundancy or low analytical value.)*

---

### **Step 6: Convert Date Columns**

* Change **Date of latest ungraded inspection** and **Ungraded inspection publication date** to type **Date** using the **Transform ▸ Data Type ▸ Date** option.

---

### **Step 7: Keep Only Required Columns**

* Use **Choose Columns** and select the columns needed for your Fact table:

  * `Web link`, `URN`, `LAESTAB`, `School name`, `Ofsted phase`, `Type of education`, `Admissions policy`,
    `Sixth form`, `Ofsted region`, `Region`, `Local authority`, `Parliamentary constituency`,
    `Multi-academy trust name`, `Postcode`, `Total number of pupils`,
    inspection and rating metrics, etc.

---

### **Step 8: Merge with Dimension Tables**

Perform several **merge joins** to link descriptive lookup tables to this Fact table.

Each join is a **Left Outer Join**.

1. **Join to `DimTypeofEducation`**

   * Home ▸ **Merge Queries ▸ Merge Queries as New**
   * Match `Type of education` to `DimTypeofEducation[Type of education]`
   * Expand `KeyTypeofEducation`
   * Rename column → `KeyTypeofEducation`
   * Remove the original `Type of education` column

2. **Join to `DimSixthForm`**

   * Match `Sixth form`
   * Expand `KeySixthForm`
   * Rename column → `KeySixthForm`
   * Remove original `Sixth form`

3. **Join to `DimOfstedPhase`**

   * Match `Ofsted phase`
   * Expand `KeyOfstedPhase`
   * Rename column → `KeyOfstedPhase`
   * Remove original `Ofsted phase`

4. **Join to `DimLA`**

   * Match `Local authority`
   * Expand `Key LA`
   * Rename → `Key LA`
   * Remove `Ofsted region`, `Region`, and `Local authority`

5. **Join to `Dim Parliament`**

   * Match `Parliamentary constituency`
   * Expand `Key Parliament`
   * Remove the original constituency column

---

### **Step 9: Rename Columns for Clarity**

* Rename:

  * `The income deprivation affecting children index (IDACI) quintile` → `Income Deprivation (IDACI) quintile`
  * `Web link` → `Ofsted Report`

---

### **Step 10: Replace Invalid Rating Values**

* Replace numeric codes **8** and **9** with nulls where applicable:

  * Columns: `Quality of education`, `Behaviour and attitudes`, `Personal development`, `Early years provision (where applicable)`
  * Use **Transform ▸ Replace Values**

---

### **Step 11: Add a Custom Column (GRE Rating)**

* Go to **Add Column ▸ Custom Column**
* Name: `GRE Rating`
* Formula:

  ```powerquery
  = List.Average({
    [Effectiveness of leadership and management],
    [Quality of education],
    [Behaviour and attitudes],
    [Personal development],
    [#"Early years provision (where applicable)"]
  })
  ```
* Change the new column’s **Data Type** to **Decimal Number**

*(Explain: this creates a composite score averaging key performance indicators.)*

---

### **Step 12: Final Review and Close**

* Verify no missing data or type errors appear.
* Go to **Home ▸ Close & Apply** to load the data into Power BI.

---

## 🧩 Outcome

Students will have a **cleaned, joined, and typed Fact table (`OfstedFact`)** that relates to several Dimensions:

* `DimTypeofEducation`
* `DimSixthForm`
* `DimOfstedPhase`
* `DimLA`
* `Dim Parliament`

They can then model relationships and begin writing **DAX measures** such as:

```DAX
Avg Number of Students = AVERAGE(OfstedFact[Total number of pupils])
Number Inspections = COUNT(OfstedFact[Overall effectiveness])
```


