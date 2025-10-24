

## 🧩 Major Step: Creating the *DimOfstedRatings* Dimension Table

### **Objective**

Students will create a dimension table from a small Excel file that defines the Ofsted grades used across inspections.
They will import the data, promote headers, and apply the correct data types.

---

### **Step-by-Step Instructions**

#### 🪜 Step 1: Load the Excel File

1. In Power BI Desktop, go to **Home ▸ Get Data ▸ Excel workbook**.
2. Browse to the file:

   ```
   C:\Users\GethynEllis\Desktop\Offsted_Grade.xlsx
   ```
3. In the **Navigator** window, select the sheet named **Ofsted Ratings**.
4. Click **Transform Data** to open it in Power Query.

---

#### 🪜 Step 2: Promote Headers

* On the **Home** tab, select **Use First Row as Headers**.
  *(This converts the first row into proper column names.)*

---

#### 🪜 Step 3: Verify and Set Data Types

1. In the **Transform** tab, set:

   * **Ofsted Grade Index** → **Whole Number**
   * **Ofsted Grade Rating** → **Text**
2. You can change data types using:

   * Column header drop-down ▸ **Data Type ▸ Whole Number/Text**,
     or
   * **Transform ▸ Data Type ▸ …**

---

#### 🪜 Step 4: Rename the Query

* In the **Query Settings** pane on the right, rename the query to:

  ```
  DimOfstedRatings
  ```

---

### ✅ **Result**

Your final table should look like this:

| Ofsted Grade Index | Ofsted Grade Rating       |
| ------------------ | ------------------------- |
| 1                  | Outstanding               |
| 2                  | Good                      |
| 3                  | Requires Improvement      |
| 4                  | Inadequate                |
| 5                  | Unknown – Awaiting rating |
| 6                  | Not Judged                |

---

### 🧠 Teaching Notes

* This table is a **lookup (dimension)** used for decoding numeric grade values in the fact table.
* The relationship between `OfstedFact[Overall effectiveness]` and `DimOfstedRatings[Ofsted Grade Index]` provides readable labels in visuals and slicers.
* Reinforce to learners that *lookup dimensions* like this improve model clarity and maintain data consistency.

---

Would you like me to prepare the same Power Query step-by-step guide for **DimSixthForm** next?


## 🧩 Major Step: Creating the *Dim Parliament* Dimension Table

### **Objective**

Students will create a **Parliamentary Constituency dimension** to support regional analysis within the Ofsted dataset.
They’ll extract unique constituency names, remove duplicates, and assign a numeric surrogate key.

---

### **Step-by-Step Instructions**

#### 🪜 Step 1: Load the CSV File

1. In Power BI Desktop, go to **Home ▸ Get Data ▸ Text/CSV**.
2. Browse to:

   ```
   C:\Users\GethynEllis\Downloads\Management_information_-_state-funded_schools_-_latest_inspections_as_at_30_June_2025.csv
   ```
3. Select **Transform Data** to open it in **Power Query**.

---

#### 🪜 Step 2: Promote Headers

* On the **Home** tab, select **Use First Row as Headers** to ensure the first row becomes your column headers.

---

#### 🪜 Step 3: Set Data Type

* Verify that the column **Parliamentary constituency** is set to **Text**.
  *(If not, select the column ▸ go to **Transform ▸ Data Type ▸ Text**.)*

---

#### 🪜 Step 4: Keep Only the Relevant Column

* Select the **Parliamentary constituency** column.
* Choose **Home ▸ Remove Columns ▸ Remove Other Columns**.
  *(This keeps only the column you need for the dimension.)*

---

#### 🪜 Step 5: Remove Duplicate Values

* Go to **Home ▸ Remove Rows ▸ Remove Duplicates**.
  *(This ensures each constituency name only appears once.)*

---

#### 🪜 Step 6: Add a Surrogate Key

* Navigate to **Add Column ▸ Index Column ▸ From 1**.
  *(This adds a numeric identifier for each constituency — your surrogate key.)*

---

#### 🪜 Step 7: Rename the Index Column

* Double-click on the **Index** column header and rename it to:

  ```
  Key Parliament
  ```

---

#### 🪜 Step 8: Rename the Query

* In the **Query Settings** pane on the right, rename the query to:

  ```
  Dim Parliament
  ```

---

### ✅ **Result**

You’ll have a dimension table like this:

| Parliamentary constituency       | Key Parliament |
| -------------------------------- | -------------- |
| Cities of London and Westminster | 1              |
| Holborn and St Pancras           | 2              |
| Hampstead and Highgate           | 3              |
| Greenwich and Woolwich           | 4              |
| …                                | …              |

---

### 🧠 Teaching Notes

* This table can be related to the **OfstedFact** table using the *Parliamentary constituency* field.
* Explain that **Parliamentary Constituency** represents a *political geography dimension* used in analysis.
* The **Index column** serves as a **surrogate key**, which improves model performance and ensures relationships stay stable if constituency names change.




## 🧩 Lab: Creating the *DimLA* (Local Authority) Dimension Table

### **Objective**

Students will create a dimension table listing all **unique Local Authorities** from the Ofsted dataset.
They will use Power Query to clean and prepare the data, remove duplicates, and generate a surrogate key for relationships.

---

### **Step-by-Step Instructions**

#### 🪜 Step 1: Load the CSV file

1. In Power BI Desktop, go to **Home ▸ Get Data ▸ Text/CSV**.
2. Browse to:

   ```
   C:\Users\GethynEllis\Downloads\Management_information_-_state-funded_schools_-_latest_inspections_as_at_30_June_2025.csv
   ```
3. Click **Transform Data** to open Power Query.

---

#### 🪜 Step 2: Promote Headers

* On the **Home** tab, click **Use First Row as Headers**.
  *(This promotes the first row to column names.)*

---

#### 🪜 Step 3: Set Data Type

* Verify the **Local authority** column is set to **Text**.
  *(If not, select the column ▸ **Transform ▸ Data Type ▸ Text**.)*

---

#### 🪜 Step 4: Keep Only the Required Column

* Select the **Local authority** column.
* Then go to **Home ▸ Remove Columns ▸ Remove Other Columns**.
  *(This keeps just the Local Authority column for your dimension.)*

---

#### 🪜 Step 5: Remove Duplicate Values

* On the **Home** tab, choose **Remove Rows ▸ Remove Duplicates**.
  *(This ensures each Local Authority appears only once.)*

---

#### 🪜 Step 6: Add a Surrogate Key

* Go to **Add Column ▸ Index Column ▸ From 1**.
  *(This adds a new numeric key starting at 1.)*

---

#### 🪜 Step 7: Rename the Index Column

* Double-click the column header **Index** and rename it to:

  ```
  Key LA
  ```

---

#### 🪜 Step 8: Rename the Query

* In the **Query Settings** pane (right-hand side), rename the query to:

  ```
  DimLA
  ```

---

### ✅ **Result**

Your final dimension table should look similar to this:

| Local authority | Key LA |
| --------------- | ------ |
| City of London  | 1      |
| Camden          | 2      |
| Greenwich       | 3      |
| Hackney         | 4      |
| …               | …      |

---

### 🧠 Teaching Notes

* Explain that **Local Authority** is a *geographical dimension* useful for analysis by council area or region.
* The **Index Column** acts as a *surrogate key*, allowing efficient relationships between the **OfstedFact** table and this **DimLA** table.
* Encourage students to check for blanks or missing entries in the column profile panel (bottom of Power Query).




## 🧩 Major Step: Creating the *DimOfstedPhase* Dimension Table

### **Objective**

Students will create a dimension table listing all unique Ofsted phases (e.g., Primary, Secondary, Special).
This exercise helps them understand how to create dimension tables with surrogate keys from a flat file source.

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

* In the **Home** tab, click **Use First Row as Headers** to make the first row your column names.

---

#### 🪜 Step 3: Set Column Data Types

* Ensure that the column **Ofsted phase** is set to **Text** type.
  (If not, click the column header ▸ choose **Transform ▸ Data Type ▸ Text**.)

---

#### 🪜 Step 4: Keep Only the Required Column

* Select the **Ofsted phase** column.
* Go to **Home ▸ Remove Columns ▸ Remove Other Columns**.
  *(This keeps only the relevant field for your dimension.)*

---

#### 🪜 Step 5: Remove Duplicate Values

* With the **Ofsted phase** column selected, go to **Home ▸ Remove Rows ▸ Remove Duplicates**.
  *(This ensures each phase only appears once.)*

---

#### 🪜 Step 6: Add a Surrogate Key

* Go to **Add Column ▸ Index Column ▸ From 1**.
  *(This adds a numeric key starting at 1 — used as the surrogate key for the dimension table.)*

---

#### 🪜 Step 7: Rename the Index Column

* Double-click the new column header `Index` and rename it to:

  ```
  KeyOfstedPhase
  ```

---

#### 🪜 Step 8: Rename the Query

* In the **Query Settings** pane (right-hand side), change the query **Name** to:

  ```
  DimOfstedPhase
  ```

---

### ✅ **Result**

You now have a dimension table like this:

| Ofsted phase | KeyOfstedPhase |
| ------------ | -------------- |
| Primary      | 1              |
| Nursery      | 2              |
| PRU          | 3              |
| Secondary    | 4              |
| Special      | 5              |

---

### 🧠 Teaching Notes

* The **Index Column** is used to generate a **surrogate key** for joining to fact tables.
* Dimension tables hold **descriptive, categorical data** used in slicers and filters.
* This table will later relate to the **OfstedFact** table on the `Ofsted phase` column.


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


---

## 🧭 Final Step: Building Relationships Between the Fact and Dimension Tables

### **Objective**

You will now connect your **OfstedFact** table to each of the dimension tables you created.
This step turns your Power BI model into a true **star schema**, enabling easy slicing and filtering across multiple dimensions.

---

### **Step-by-Step Instructions**

#### 🪜 Step 1: Open the Model View

1. In **Power BI Desktop**, click on the **Model** icon (bottom-left side panel).
   *(It looks like three connected boxes — this view shows how tables relate to each other.)*

---

#### 🪜 Step 2: Review the Existing Tables

You should see the following tables listed:

* **OfstedFact**
* **DimOfstedRatings**
* **DimTypeofEducation**
* **DimSixthForm**
* **DimOfstedPhase**
* **DimLA**
* **Dim Parliament**

---

#### 🪜 Step 3: Create Relationships

Drag and connect the fields as follows:

| From Table (Fact) | From Column               | To Table (Dimension) | To Column              |
| ----------------- | ------------------------- | -------------------- | ---------------------- |
| OfstedFact        | **Overall effectiveness** | DimOfstedRatings     | **Ofsted Grade Index** |
| OfstedFact        | **KeyTypeofEducation**    | DimTypeofEducation   | **KeyTypeofEducation** |
| OfstedFact        | **KeySixthForm**          | DimSixthForm         | **KeySixthForm**       |
| OfstedFact        | **KeyOfstedPhase**        | DimOfstedPhase       | **KeyOfstedPhase**     |
| OfstedFact        | **Key LA**                | DimLA                | **Key LA**             |
| OfstedFact        | **Key Parliament**        | Dim Parliament       | **Key Parliament**     |

*(Tip: If you renamed columns differently, match on your equivalent key fields.)*

---

#### 🪜 Step 4: Verify Relationship Settings

For each relationship:

1. Double-click the connecting line to open **Edit Relationship**.
2. Confirm these settings:

   * **Cardinality:** *Many-to-One (* *)*
     *(Many Fact rows map to one Dimension row.)*
   * **Cross filter direction:** *Single*
     *(Filtering should flow from the Dimension to the Fact table.)*
3. Click **OK** to confirm.

---

#### 🪜 Step 5: Check Relationship Arrows

* Arrows should point **from each Dimension table → to OfstedFact**.
* This ensures filters (for example, selecting “Outstanding”) correctly affect your visuals.

---

#### 🪜 Step 6: Save and Test the Model

1. Save your Power BI file.
2. Create a simple **report visual**:

   * Use a **table** visual.
   * Add **Ofsted Grade Rating** (from DimOfstedRatings) and **Avg Number of Students** (measure).
3. Confirm that changing slicers like *Type of Education* or *Ofsted Phase* updates your results — proving relationships work.

---

### ✅ **Result**

You now have a **fully related star-schema model**:

* A single **Fact** table (*OfstedFact*) in the centre
* Surrounded by connected **Dimension** tables that describe context (Phase, Education Type, LA, etc.)

This model structure is efficient, easy to understand, and ready for **DAX measures** and interactive **Power BI reports**.

---

### 🧠 **Teaching Notes**

* Emphasise that **relationships** enable cross-filtering and ensure measures aggregate correctly.
* Reinforce **star schema best practice**: one Fact table, many connected Dimensions.
* Encourage learners to sketch or screenshot their completed data model for future reference.


