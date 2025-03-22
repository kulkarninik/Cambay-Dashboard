# Power BI Team Performance Dashboard

## 📌 Project Overview
This Power BI dashboard provides insights into **team performance**, tracking individual contributions, monthly lead generation, and overall progress. It includes **drill-through functionality** to analyze each team member's performance in detail.

## 📊 Features
- **Home Page:**
  - Displays **total leads, yet-to-be-held meetings, held meetings, and monthly leads per year**.
  - Includes a table with all team members' names, allowing **drill-through navigation**.

- **Individual Performance Page:**
  - Shows **team member’s name, image, total leads, yet-to-be-held meetings, held meetings, per-year monthly leads, and months completed**.
  - Uses dynamic filtering to focus on a selected individual.

## 📂 Data Sources
The dashboard is built using two datasets:
1. **Lead Report Account Wise** – Contains all lead-related information.
2. **Team Members (Sheet1(2))** – Contains the names and joining dates of team members.

## 🛠 Power BI Setup Instructions
### 1️⃣ **Prepare Your Data**
- Ensure the **Lead Report Account Wise** table has columns:
  - `SR No`, `Opportunity Name`, `Services`, `Created By - IS Person`, `Manager Assigned To`, `Created Date`, `Meeting Schedule Date`, `Meeting Held (Yes/Yet to be held)`.
- The **Sheet1(2)** table should have:
  - `Name`, `Date of Joining`, `Image URL` (direct image link).

### 2️⃣ **Data Transformation in Power Query**
- Extract **Year** and **Month Name** from `Created Date`.
- Calculate **Months Completed** for each team member:
  ```DAX
  Months Completed = DATEDIFF(
      LOOKUPVALUE('Sheet1(2)'[Date of Joining], 'Sheet1(2)'[Name], SELECTEDVALUE('Table'[Created By - IS Person])),
      TODAY(),
      MONTH
  )
  ```

### 3️⃣ **Create Key Measures in DAX**
- **Leads Per Year Per Month:**
  ```DAX
  Leads Per Year Per Month =
  CALCULATE(
      COUNT('Lead Report Account Wise'[SR No]),
      ALLEXCEPT('Lead Report Account Wise', 'Lead Report Account Wise'[Year], 'Lead Report Account Wise'[Month])
  )
  ```

- **Total Leads, Yet-to-be-Held, and Held Meetings:**
  ```DAX
  Total Leads = COUNT('Lead Report Account Wise'[SR No])
  Yet-to-be-Held Meetings = CALCULATE(COUNT('Lead Report Account Wise'[SR No]), 'Lead Report Account Wise'[Meeting Held] = "Yet to be held")
  Held Meetings = CALCULATE(COUNT('Lead Report Account Wise'[SR No]), 'Lead Report Account Wise'[Meeting Held] = "Yes")
  ```

### 4️⃣ **Build Visualizations**
- **Line Chart:** To display leads per month for each year.
- **Table Visual:** To show team members and their performance.
- **Card Visual:** To show individual statistics on the drill-through page.
- **Image Visual:** Use **"Image by CloudScope"** or **"Smart Image Grid"** to display team member photos.

## 🚀 How to Use the Dashboard
1. **Navigate to the Home Page** to see the team's overall performance.
2. **Click on a team member's name** → **Right-click → Drill-Through** to view their individual stats.
3. **Analyze trends** in lead generation and meeting statuses.

## 📝 Notes
- Ensure images are stored in a publicly accessible location with **direct image URLs**.
- The dashboard dynamically updates as new data is added.

## 🏗 Future Enhancements
- Add **filters for service type**.
- Integrate **monthly and yearly comparisons**.
- Automate data refresh for real-time insights.

---
### 🏆 Built with ❤️ using Power BI
For any queries, feel free to **raise an issue** or contribute! 😊

