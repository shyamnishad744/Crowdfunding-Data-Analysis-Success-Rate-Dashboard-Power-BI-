

# 🚀 Kickstarter Crowdfunding Analysis – Power BI


> **End-to-end analysis of 378,000+ Kickstarter projects (2010-2018) revealing what drives crowdfunding success through advanced data modeling and interactive dashboards.**

---


---

## 📊 Project Overview

This project analyzes Kickstarter crowdfunding campaigns to uncover success patterns and provide data-driven guidance for creators and backers. Using Power BI for visualization and advanced DAX for calculations, I transformed raw epoch timestamps into actionable business intelligence.

**Dataset:** 378,661 projects | **Time Period:** 2010-2018 | **Categories:** 169 types | **Locations:** 23,252 places

---

## 🎯 The STAR Method

### 📌 SITUATION
Kickstarter raised over $34 billion globally, but most creators lack data-driven insights. With a **62% failure rate**, understanding what drives success is critical. Projects often fail due to unrealistic goals, poor timing, or market saturation—problems that data analysis can solve.

**The Problem:** How can creators maximize their probability of success? What patterns separate funded projects from failures?

---

### 🎯 TASK
Build a comprehensive analytics solution to:
- Calculate overall and segmented success rates
- Identify optimal funding goals and campaign durations
- Analyze geographic and category performance
- Discover temporal trends (yearly, monthly patterns)
- Provide actionable recommendations for creators

**Success Metrics:**
- Interactive dashboard with <3 second load time
- Calendar intelligence with fiscal year support
- Top/bottom performer identification
- Real-time filtering across all dimensions

---

### ⚙️ ACTION

#### **Step 1: Data Transformation**
- **Epoch Time Conversion:** Converted Unix timestamps to natural dates
  ```
  Natural Date = (Epoch Time / 86400) + DATE(1970, 1, 1)
  ```
- **Currency Standardization:** Normalized all goals to USD using static exchange rates
- **Data Validation:** Cleaned duplicates, handled missing values, verified data integrity

#### **Step 2: Calendar Table Creation**
Built comprehensive date dimension with:
- Year, Quarter, Month, Week dimensions
- Financial Year columns (April-March): FM1-FM12, FQ1-FQ4
- Day of week analysis for launch timing optimization

**DAX Formula:**
```DAX
Calendar = CALENDAR(MIN(Projects[created_date]), MAX(Projects[created_date]))
Financial Month = IF(MONTH([Date]) >= 4, MONTH([Date]) - 3, MONTH([Date]) + 9)
```

#### **Step 3: Data Modeling**
- **Star Schema Design:** Projects (fact) connected to Category, Location, Creator, Calendar (dimensions)
- **Relationships:** Established one-to-many relationships for efficient filtering
- **Data Model:** 5 tables with proper cardinality and cross-filter direction

#### **Step 4: KPI Development**
Created business metrics using DAX:
```DAX
Success Rate = DIVIDE(
    COUNTROWS(FILTER(Projects, Projects[state] = "successful")),
    COUNTROWS(Projects), 0
)

Avg Successful Days = CALCULATE(
    AVERAGE(Projects[duration_days]),
    Projects[state] = "successful"
)

Total Backers = SUM(Projects[backers_count])
```

#### **Step 5: Dashboard Design**
- **Page 1:** Executive KPIs, trends, top performers, geographic analysis
- **Page 2:** Success rate trends, goal range analysis, category breakdown
- **Interactivity:** Slicers for state, category, year with cross-filtering

---

### 📈 RESULT

#### **Key Findings:**

| Metric | Value | Insight |
|--------|-------|---------|
| **Overall Success Rate** | 38% | Only 1 in 3 projects succeed—highly competitive |
| **Total Amount Raised** | $18.94M | Successful projects only |
| **Average Campaign Duration** | 80.43 days | Sweet spot for successful projects |
| **Total Backers** | 40M | Massive global participation |
| **Total Projects** | 140K successful | Out of 378K total |

#### **Critical Insights:**

**1. Goal Range Paradox:**
- ✅ **Below $5K:** 39% of successful projects (highest probability)
- ⚠️ **$5K - $10K:** 5% of successful projects
- ⚠️ **$10K - $50K:** 4% of successful projects  
- ❌ **Above $50K:** 2% of successful projects (20x lower than <$5K)

**2. Temporal Trends:**
- 📈 **2014 Peak:** 49K projects launched BUT success rate dropped to 33%
- 📉 **2018 Collapse:** 96% decline in volume (49K → 2K projects)
- 🔄 **Market Saturation Effect:** High volume = lower individual success rates

**3. Geographic Concentration:**
- 🥇 **California:** 52K projects (tech/creative hub)
- 🥈 **New York:** 30K projects (arts/media center)
- 🥉 **England:** 29K projects (international presence)
- **Insight:** Major creative hubs dominate project creation

**4. Top Performers:**
- **Exploding Kittens:** 220K backers
- **Fidget Cube:** 150K backers
- **Bring Reading Rainbow Back:** 110K backers
- **Pattern:** Viral appeal + existing fan base = massive success

#### **Strategic Recommendations:**

✅ **For Creators:**
1. **Set conservative goals** (<$5K) to maximize success probability
2. **Plan 80-day campaigns** for optimal momentum building
3. **Avoid peak periods** (2014 shows saturation reduces success)
4. **Leverage location advantage** if in CA/NY/London creative hubs
5. **Build pre-launch audience** (38% success rate requires preparation)

✅ **For Platform:**
1. **Investigate 2014-2018 decline** (96% volume drop needs analysis)
2. **Provide goal-setting tools** showing category-specific success rates
3. **Offer campaign duration guidance** based on historical data

---

## 🔍 Key Insights Summary

| Finding | Impact | Action |
|---------|--------|--------|
| 38% success rate | HIGH | Emphasize realistic goal-setting |
| Sub-$5K goals succeed 20x more than $50K+ | CRITICAL | Promote incremental funding approach |
| 2014: 49K projects, 33% success | HIGH | Avoid market saturation periods |
| 80-day avg duration | MEDIUM | Standard campaign length guidance |
| CA, NY, England dominate | MEDIUM | Geographic targeting strategies |
| 96% platform decline (2014→2018) | CRITICAL | Investigate platform health |

---

## 📊 Dashboard Features

### **Page 1: Success Rate Dashboard**
- 📌 **KPI Cards:** Success Rate (38%), Amount Raised ($18.94M), Avg Days (80.43), Total Backers (40M)
- 📊 **Top 5 Backers:** Bar chart showing viral projects
- 📈 **Total Projects Over Years:** Line chart (2010-2018 trend)
- 🗺️ **Top 5 States:** Geographic concentration analysis
- 📋 **Top 7 Successful Projects:** Detailed table with amounts
- 🎯 **Success Rate by Name:** Donut chart comparison
- 🔍 **State Filter:** Interactive slicer

### **Page 2: Deep Dive Analysis**
- 📉 **Success % Over Years:** Trend line showing 2014 dip
- 📊 **Success % by Goal Range:** Bar chart (<$5K vs $50K+)
- 💡 **Category Analysis:** Performance by project type
- 📅 **Monthly Patterns:** Seasonal trends

### **Interactive Elements:**
- Cross-filtering across all visuals
- Drill-through from summary to detail
- Dynamic tooltips with additional context
- Mobile-responsive design

---

## 🧰 Tools & Technologies

| Tool | Purpose | Key Features Used |
|------|---------|-------------------|
| **Power BI Desktop** | Data modeling & visualization | Star schema, DAX, Interactive reports |
| **DAX** | Calculated measures | Time intelligence, Statistical functions |
| **Power Query (M)** | Data transformation | Epoch conversion, Data cleansing |
| **Excel** | Source data | Initial CSV files (Category, Location, Creator) |

### **Technical Skills Demonstrated:**
✅ **Data Transformation:** Epoch time conversion, currency normalization  
✅ **Data Modeling:** Star schema with 5 tables, relationship management  
✅ **Calendar Intelligence:** Custom fiscal year dimensions  
✅ **DAX Proficiency:** Success rate calculations, time-based measures  
✅ **Visualization:** Interactive dashboards with drill-down capabilities  
✅ **Business Analysis:** Pattern recognition, strategic recommendations  

---

## 💡 Key Learnings

**Technical:**
- Converting epoch timestamps requires mathematical precision
- Calendar tables enable powerful time intelligence analysis
- Star schema improves performance and user experience
- DAX context (row vs filter) is critical for accurate calculations
- Data validation catches anomalies (2018's 3% success rate = incomplete data)

**Business:**
- Crowdfunding success is highly competitive (62% failure rate)
- Conservative goal-setting dramatically increases success probability
- Market saturation inversely affects individual project visibility
- Geographic location provides networking/media advantages
- Platform health trends reveal ecosystem challenges

**Analytical:**
- Always question anomalies (2018 data prompted deeper investigation)
- Multiple dimensions reveal hidden patterns (volume vs success inverse relationship)
- Visualization choices impact insight discovery (goal range chart revealed 20x difference)

---

## 📂 Project Structure

```
Kickstarter-Analysis/
│
├── data/
│   ├── crowdfunding_Category.xlsx
│   ├── Crowdfunding_Location.xlsx
│   ├── Crowdfunding_Creator.xlsx
│   └── Crowdfunding_Project.xlsx (31MB+ main file)
│
├── powerbi/
│   └── PROJECT-Kickstarter Crowdfunding.pbix
│
├── screenshots/
│   ├── dashboard_page1.png
│   └── dashboard_page2.png
│
├── documentation/
│   └── Kickstarter_Overview.pdf
│
└── README.md
```

---

## 🚀 How to Use

### **Prerequisites:**
- Power BI Desktop (latest version)
- Excel 2016 or later

### **Setup:**

1. **Clone Repository:**
   ```bash
   git clone https://github.com/yourusername/kickstarter-analysis.git
   ```

2. **Open Power BI File:**
   - Launch Power BI Desktop
   - Open `PROJECT-VIKRANT.pbix`
   - Data sources should auto-connect to Excel files

3. **Explore Dashboard:**
   - Use slicers to filter by state, category, year
   - Click on charts for cross-filtering
   - Navigate between pages using tabs

4. **Refresh Data:**
   - If using updated data, click "Refresh" in Home tab
   - Verify relationships in Model view

---

## 📸 Dashboard Preview

### Success Rate Overview
![Dashboard Page 1](screenshots/dashboard_page1.png)

### Trend Analysis
![Dashboard Page 2](screenshots/dashboard_page2.png)

---

## 🔄 Future Enhancements

- [ ] Predictive model for success probability
- [ ] Text analysis of project descriptions
- [ ] Backer behavior and retention analysis
- [ ] Category deep-dive (subcategory performance)
- [ ] Real-time data integration (current projects)
- [ ] Competitive platform comparison (Indiegogo, GoFundMe)

---

## 👤 Author

**Shyam Nishad**

- 📧 Email: nishadshyamsunder83@gmail.com
- 💼 LinkedIn: [linkedin.com/in/shyamnishad](https://linkedin.com/in/shyamnishad)
- 🐙 GitHub: [@shyamnishad](https://github.com/shyamnishad)

---

## 🙏 Acknowledgments

- Dataset: Kickstarter historical campaign data
- Inspiration: Understanding the $34B+ crowdfunding ecosystem
- Reference: Kickstarter platform documentation

---


[![GitHub stars](https://img.shields.io/github/stars/shyamnishad/kickstarter-analysis?style=social)](https://github.com/shyamnishad/kickstarter-analysis/stargazers)

</div>
