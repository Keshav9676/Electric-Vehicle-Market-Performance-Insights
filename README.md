# Electric-Vehicle-Market-Performance-Insights[TABLEAU_DEPLOYMENT_GUIDE.md](https://github.com/user-attachments/files/34133107/TABLEAU_DEPLOYMENT_GUIDE.md)
# Tableau Deployment Guide: EV Performance Insights Dashboard

This guide provides end-to-end instructions for deploying the **Electric Vehicle Performance Insights Dashboard** using **Tableau Public** (Free) or **Tableau Desktop / Tableau Cloud / Tableau Server**.

---

## 📁 Packaged Tableau Files in this Repository

| File Path | Description |
| :--- | :--- |
| [`tableau/ev_performance_insights.twb`](file:///c:/Users/kesha/python3/Electric%20Vehicle%20Market%20Performance%20&%20Insights/tableau/ev_performance_insights.twb) | Native Tableau Workbook XML with predefined data connections, worksheets, and dashboards. |
| [`tableau/ev_market_data.xlsx`](file:///c:/Users/kesha/python3/Electric%20Vehicle%20Market%20Performance%20&%20Insights/tableau/ev_market_data.xlsx) | Multi-tab Excel workbook containing master data, KPI references, calculated fields, and audit log. |
| [`tableau/ev_market_data.csv`](file:///c:/Users/kesha/python3/Electric%20Vehicle%20Market%20Performance%20&%20Insights/tableau/ev_market_data.csv) | Primary cleaned master CSV used by the Tableau workbook. |
| [`tableau/TABLEAU_CALCULATED_FIELDS.md`](file:///c:/Users/kesha/python3/Electric%20Vehicle%20Market%20Performance%20&%20Insights/tableau/TABLEAU_CALCULATED_FIELDS.md) | Copy-pasteable Tableau LOD calculations and formulas. |

---

## 🚀 Option 1: Deploy Using Tableau Public (100% Free Web Hosting)

Tableau Public allows you to host interactive dashboards online for free without needing a paid license.

### Step 1: Download & Install Tableau Public
1. Download **Tableau Public Desktop** from [public.tableau.com](https://public.tableau.com/en-us/s/download).
2. Install and launch the application.

### Step 2: Open or Connect the Data
1. Launch Tableau Public.
2. Under **Connect to a File**, select **Text File** and choose:
   `c:\Users\kesha\python3\Electric Vehicle Market Performance & Insights\tableau\ev_market_data.csv`
   *(Alternatively, open `tableau/ev_performance_insights.twb` directly via `File -> Open`).*
3. Verify the columns:
   - Ensure `Manufacturing Country` has the Geographic Role: **Country / Region**.
   - Ensure `Model Year` is set to **Dimension (Discrete)**.

### Step 3: Publish to Web
1. From the top menu, click **Server** → **Tableau Public** → **Save to Tableau Public As...**
2. Sign in with your free Tableau Public account.
3. Name your workbook: `EV Performance Insights Dashboard`.
4. Click **Save**.
5. Once published, Tableau Public provides a **live interactive web URL** and an **`<iframe>` embed code** that you can embed into any website, Notion, or intranet.

---

## 🏢 Option 2: Deploy to Tableau Cloud / Tableau Server (Enterprise)

For corporate deployments requiring role-based access control and scheduled refreshes:

1. Open `tableau/ev_performance_insights.twb` in **Tableau Desktop**.
2. Go to **Server** → **Sign In...** and connect to your **Tableau Cloud** or on-premises **Tableau Server**.
3. Go to **Server** → **Publish Workbook...**
4. Configure options:
   - **Project**: Select target project folder (e.g., `Market Intelligence`).
   - **Name**: `EV Performance Insights Dashboard`.
   - **Sheets**: Select `All Dashboards` or `Story`.
   - **Permissions**: Grant access to Executive Strategy, BI Managers, and Research Analysts.
5. Click **Publish**.

---

## ⚙️ How to Configure PRD Interactive Features in Tableau

### 1. Cross-Filtering Across All Visuals (PRD FR-21)
To allow clicking a category (e.g. `SUV`) or country on the map to filter all other charts:
1. Open the dashboard in Tableau.
2. In the top menu, select **Dashboard** → **Actions...**
3. Click **Add Action** → **Filter...**
4. Set:
   - **Source Sheets**: Select all sheets in the dashboard.
   - **Run action on**: `Select`.
   - **Target Sheets**: Select all sheets in the dashboard.
   - **Clearing the selection will**: `Show all values`.
5. Click **OK**.

### 2. Multi-Attribute Global Filters (PRD FR-20)
1. In the first worksheet, drag each of the following fields to the **Filters** shelf:
   - `[Model Year]`
   - `[Vehicle Category]`
   - `[Manufacturer]`
   - `[Battery Type]`
   - `[Manufacturing Country]`
2. Right-click each filter on the shelf and select **Apply to Worksheets** → **All Using This Data Source**.
3. In the dashboard view, display these filters as **Multiple Values (Dropdown)**.

### 3. Persona Storyboards (PRD FR-25)
To create persona-oriented navigation:
1. Click **New Story** (bottom tab).
2. Set Story size to `Automatic` or `1440 x 900`.
3. Add **Point 1**: Drag `1. Executive Summary` and title it:
   `👑 Emily Johnson: EV Market Strategy Director View`
   *Description: Portfolio allocation, YoY growth segments, and volume leaders.*
4. Add **Point 2**: Drag `2. Competitive Positioning` and title it:
   `💼 David Chen: Automotive BI Manager View`
   *Description: OEM scorecards, market share shifts, and Price vs. Range positioning.*
5. Add **Point 3**: Drag `3. Technology & Geography` and title it:
   `🔬 Dr. Sarah Williams: Mobility Researcher View`
   *Description: Battery chemistry transition (LFP, Solid-State) and global production footprint.*

---

## 📤 Export Capabilities (PRD FR-24)

Once deployed on Tableau Public, Cloud, or Server:
- **Download as PDF**: Users can click the native **Download** button at the top/bottom and select **PDF** with orientation *Landscape*.
- **Download Filtered CSV**: Click any chart visual → click **Download** → select **Data** or **Crosstab** to download an Excel/CSV file with the current filter state.
- **Download Image (PNG)**: Click **Download** → **Image**.

