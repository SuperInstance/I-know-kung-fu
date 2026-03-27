# Spreadsheet Analyst Examples

## Example 1: Sales Data Analysis

### User Request
```
Analyze the sales data in /data/sales_2024.xlsx and provide:
1. Summary statistics for revenue and units sold
2. Top 5 performing products
3. Monthly trend analysis
4. Regional performance comparison
```

### Agent Response
```
Analyzing your sales data...

[Loading spreadsheet...]
[Performing statistical analysis...]
[Identifying trends...]
[Generating insights...]

✅ Sales Analysis Complete:

**Dataset Overview:**
- Total Records: 15,234
- Date Range: Jan 1 - Dec 31, 2024
- Products: 48 SKUs
- Regions: 6

📊 Summary Statistics

| Metric | Revenue | Units Sold |
|--------|---------|------------|
| Total | $4,856,230 | 125,430 |
| Mean | $318.75 | 8.23 |
| Median | $245.00 | 6.00 |
| Std Dev | $187.32 | 4.56 |
| Min | $45.00 | 1 |
| Max | $1,250.00 | 25 |

🏆 Top 5 Performing Products

| Rank | Product | Revenue | Units | Margin |
|------|---------|---------|-------|--------|
| 1 | Premium Widget A | $892,340 | 8,234 | 42% |
| 2 | Standard Widget B | $756,120 | 12,456 | 35% |
| 3 | Deluxe Widget C | $623,450 | 4,567 | 48% |
| 4 | Basic Widget D | $534,280 | 15,678 | 28% |
| 5 | Specialty Widget E | $412,890 | 3,210 | 52% |

📈 Monthly Trend Analysis

```
Revenue Trend 2024
$500K ┤
      │        ╭──╮
$400K ┤    ╭───╯  ╰──╮
      │   ╭╯        ╰─╮
$300K ┤  ╭╯           ╰╮
      │ ╭╯             ╰╮
$200K ┼─╯               ╰──
      └────────────────────→
       Jan Mar May Jul Sep Nov
```

Key Insights:
- Q4 showed 23% growth over Q3
- Summer dip in June-August (-15%)
- November peak (Black Friday impact)

🗺️ Regional Performance

| Region | Revenue | % of Total | Growth YoY |
|--------|---------|------------|------------|
| Northeast | $1,234,560 | 25.4% | +12% |
| West | $1,123,450 | 23.1% | +18% |
| Southeast | $987,650 | 20.3% | +8% |
| Midwest | $812,340 | 16.7% | +5% |
| Southwest | $456,780 | 9.4% | +22% |
| Northwest | $241,450 | 5.0% | -3% |

💡 Key Insights:
1. West region shows strongest growth momentum
2. Northwest requires attention (declining)
3. Premium products drive 45% of margin despite 18% of units
4. Q4 seasonal boost 2x higher than previous year

Would you like me to:
1. Create a detailed dashboard visualization
2. Forecast Q1 2025 projections
3. Analyze customer segments within the data
```

---

## Example 2: Formula Generation

### User Request
```
I need a formula that calculates commission based on tiered rates:
- Under $10,000: 5%
- $10,000-$50,000: 8%
- Over $50,000: 12%

The sales amount is in cell B2. Also explain how it works.
```

### Agent Response
```
Generating tiered commission formula...

✅ Formula Created:

**Cell:** C2
**Formula:**
```
=IF(B2<10000, B2*0.05, IF(B2<=50000, B2*0.08, B2*0.12))
```

📝 How It Works:

This is a nested IF statement that checks the sales amount against your tier thresholds:

```
IF B2 < $10,000:
   → Return: B2 × 5% (5% commission)
   
ELSE IF B2 ≤ $50,000:
   → Return: B2 × 8% (8% commission)
   
ELSE:
   → Return: B2 × 12% (12% commission)
```

**Example Calculations:**

| Sales Amount | Commission Rate | Commission |
|--------------|-----------------|------------|
| $5,000 | 5% | $250 |
| $25,000 | 8% | $2,000 |
| $75,000 | 12% | $9,000 |

🔄 Alternative (Using LOOKUP for more tiers):

If you expect to add more tiers later, this formula is more maintainable:

```
=B2*LOOKUP(B2, {0,10000,50001}, {0.05,0.08,0.12})
```

This uses an array to define breakpoints and rates, making it easier to add new tiers.

⚠️ Note: Both formulas calculate commission on the entire amount. If you need marginal/progressive rates (where each tier only applies to the amount in that tier), let me know and I'll provide a different formula.

Would you like me to:
1. Provide the progressive/marginal rate formula
2. Add this to your spreadsheet automatically
3. Create a commission calculator template
```

---

## Example 3: Pivot Table Creation

### User Request
```
Create a pivot table from /data/employee_survey.xlsx that shows:
- Average satisfaction score by department
- Count of responses by department
- Average satisfaction by tenure group (0-1 years, 1-3 years, 3+ years)
```

### Agent Response
```
Creating pivot table analysis...

[Loading survey data...]
[Creating tenure groupings...]
[Building pivot tables...]

✅ Pivot Tables Created:

**Dataset Summary:**
- Total Responses: 1,247
- Departments: 8
- Tenure Range: 0.1 to 15.2 years

📊 Pivot Table 1: Satisfaction by Department

| Department | Avg Score | Responses | Response Rate |
|------------|-----------|-----------|---------------|
| Engineering | 4.2 | 312 | 78% |
| Sales | 3.8 | 245 | 82% |
| Marketing | 4.1 | 156 | 75% |
| Operations | 3.5 | 198 | 71% |
| HR | 4.4 | 67 | 89% |
| Finance | 3.9 | 134 | 76% |
| Customer Service | 3.6 | 89 | 68% |
| Legal | 4.0 | 46 | 92% |

**Overall Average: 3.94**

📊 Pivot Table 2: Satisfaction by Tenure Group

| Tenure Group | Avg Score | Responses | % of Total |
|--------------|-----------|-----------|------------|
| 0-1 years | 3.6 | 287 | 23% |
| 1-3 years | 4.0 | 423 | 34% |
| 3+ years | 4.1 | 537 | 43% |

📊 Pivot Table 3: Cross-Tabulation (Department × Tenure)

| Dept \ Tenure | 0-1 yr | 1-3 yr | 3+ yr |
|---------------|--------|--------|-------|
| Engineering | 3.9 | 4.3 | 4.4 |
| Sales | 3.4 | 3.9 | 4.1 |
| Marketing | 3.8 | 4.2 | 4.3 |
| Operations | 3.2 | 3.5 | 3.8 |
| HR | 4.1 | 4.4 | 4.6 |
| Finance | 3.5 | 4.0 | 4.2 |
| Customer Service | 3.2 | 3.6 | 3.9 |
| Legal | 3.8 | 4.1 | 4.2 |

💡 Key Insights:

1. **Tenure Impact**: Satisfaction increases with tenure across all departments
   - New hires (0-1 yr) score 3.6 average
   - Long-tenured (3+ yr) score 4.1 average
   - Gap suggests onboarding improvement opportunity

2. **Department Leaders**:
   - HR has highest satisfaction (4.4)
   - Operations has lowest (3.5)
   - 0.9 point gap between highest and lowest

3. **Areas for Attention**:
   - Customer Service: Low response rate + low scores
   - Operations: Consistent underperformance across tenure groups

**Output File:** employee_survey_pivot_analysis.xlsx
- Sheet 1: By Department
- Sheet 2: By Tenure Group
- Sheet 3: Cross-Tabulation
- Sheet 4: Source Data

Would you like me to:
1. Create visualizations for these pivot tables
2. Perform statistical significance testing
3. Generate an executive summary report
```

---

## Example 4: Data Cleaning

### User Request
```
Clean the customer data in /data/customers_raw.csv:
- Standardize phone numbers to (XXX) XXX-XXXX format
- Fix inconsistent state abbreviations
- Remove duplicate records
- Split full names into first and last name columns
```

### Agent Response
```
Analyzing and cleaning customer data...

[Loading data...]
[Detecting issues...]
[Applying transformations...]

📋 Initial Data Assessment:
- Records: 5,234
- Columns: 8
- Issues Detected: 4 types

🔧 Cleaning Operations Applied:

**1. Phone Number Standardization**
- Formats Found: 7 different formats
- Standardized to: (XXX) XXX-XXXX

| Before | After |
|--------|-------|
| 5551234567 | (555) 123-4567 |
| 555.123.4567 | (555) 123-4567 |
| (555)123-4567 | (555) 123-4567 |
| +1 555 123 4567 | (555) 123-4567 |

Records Fixed: 3,892

**2. State Abbreviation Standardization**
- Inconsistent formats: 23 variations

| Before | After |
|--------|-------|
| California | CA |
| calif | CA |
| Ca. | CA |
| New York | NY |
| NY | NY |

Records Fixed: 847

**3. Duplicate Removal**
- Exact duplicates found: 67
- Near-duplicates found: 23

Action: Removed 90 duplicate records
Remaining records: 5,144

**4. Name Splitting**

| Full Name | First Name | Last Name |
|-----------|------------|-----------|
| John Smith | John | Smith |
| Mary Jane Wilson | Mary Jane | Wilson |
| Dr. Robert Brown | Robert | Brown |
| García-López, Maria | Maria | García-López |

Records Processed: 5,144

✅ Cleaning Complete:

**Summary Statistics:**
| Metric | Before | After |
|--------|--------|-------|
| Total Records | 5,234 | 5,144 |
| Phone Format Issues | 3,892 | 0 |
| State Format Issues | 847 | 0 |
| Duplicates | 90 | 0 |
| Columns | 8 | 10 |

**Output File:** customers_cleaned.xlsx
- Sheet 1: Cleaned Data
- Sheet 2: Cleaning Log
- Sheet 3: Rejected Records (for review)

**Data Quality Score:** 98.7% (up from 72.3%)

Would you like me to:
1. Validate cleaned data against source
2. Export to your CRM format
3. Set up automated cleaning pipeline
```

---

## Example 5: Dashboard Creation

### User Request
```
Create an executive dashboard from /data/kpi_data.xlsx showing:
- Revenue trend (line chart)
- Top 5 products by revenue (bar chart)
- Regional breakdown (pie chart)
- Key metrics cards at the top
```

### Agent Response
```
Building executive dashboard...

[Loading KPI data...]
[Calculating metrics...]
[Creating visualizations...]
[Designing layout...]

✅ Executive Dashboard Created:

📊 Dashboard Layout:

```
┌─────────────────────────────────────────────────────────────┐
│  EXECUTIVE KPI DASHBOARD - 2024                    [Refresh]│
├─────────────┬─────────────┬─────────────┬───────────────────┤
│  REVENUE    │  ORDERS     │  CUSTOMERS  │  AVG ORDER VALUE  │
│  $2.45M     │  15,234     │  8,567      │  $160.87          │
│  ↑ 23%      │  ↑ 12%      │  ↑ 18%      │  ↑ 8%             │
│  vs LY      │  vs LY      │  vs LY      │  vs LY            │
├─────────────┴─────────────┴─────────────┴───────────────────┤
│                                                             │
│  REVENUE TREND                                    [Details] │
│  ┌──────────────────────────────────────────────────────┐  │
│  │ $300K ┤                        ╭───╮                  │  │
│  │       │               ╭───────╯   ╰──╮               │  │
│  │ $200K ┤         ╭─────╯              ╰──╮            │  │
│  │       │    ╭────╯                       ╰──╮         │  │
│  │ $100K ┼────╯                                ╰────    │  │
│  │       └────────────────────────────────────────────→ │  │
│  │        Jan  Mar  May  Jul  Sep  Nov                  │  │
│  └──────────────────────────────────────────────────────┘  │
├────────────────────────────┬────────────────────────────────┤
│  TOP 5 PRODUCTS            │  REGIONAL BREAKDOWN            │
│  ┌────────────────────┐    │  ┌──────────────────────────┐  │
│  │ Product A ████████ │    │  │     ╭────╮               │  │
│  │ Product B ███████  │    │  │   ╭─╯NE  │               │  │
│  │ Product C ██████   │    │  │ ╭─╯      ╰──╮            │  │
│  │ Product D █████    │    │  │╭╯   West   ╰─╮           │  │
│  │ Product E ████     │    │  │╯    25%     ╰──╮         │  │
│  │                    │    │  │    South     ╰─╮         │  │
│  │ $0   $200K $400K   │    │  │     22%       ╰──╮       │  │
│  └────────────────────┘    │  │                MW│       │  │
│                            │  └──────────────────┴───────┘  │
└────────────────────────────┴────────────────────────────────┘
```

📈 Component Details:

**Metric Cards:**
| Metric | Value | Change | Status |
|--------|-------|--------|--------|
| Revenue | $2.45M | +23% | 🟢 On Track |
| Orders | 15,234 | +12% | 🟢 On Track |
| Customers | 8,567 | +18% | 🟢 Exceeding |
| Avg Order Value | $160.87 | +8% | 🟢 On Track |

**Charts Included:**
1. Line Chart: Monthly revenue trend with YoY comparison
2. Bar Chart: Top 5 products by revenue (horizontal)
3. Pie Chart: Regional revenue distribution
4. Sparklines: Weekly trends in each card

**Interactive Features:**
- Click-through to detailed data
- Date range filter
- Region selector
- Export to PDF/Image

**Output File:** executive_dashboard.xlsx
- Sheet 1: Dashboard (main view)
- Sheet 2: Source Data
- Sheet 3: Regional Details
- Sheet 4: Product Details
- Sheet 5: Trend Analysis

Would you like me to:
1. Add additional KPI cards
2. Include competitive benchmarking
3. Set up automated refresh schedule
```
