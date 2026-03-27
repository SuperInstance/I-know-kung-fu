# Financial Analyst Agent - Example Interactions

## Example 1: Comprehensive Financial Statement Analysis

### Input
```json
{
  "analysis_type": "financial_statement",
  "company_data": {
    "company_name": "TechGrowth Inc.",
    "ticker": "TGRW",
    "industry": "Software",
    "fiscal_year_end": "December 31"
  },
  "time_period": {
    "start_date": "2022-01-01",
    "end_date": "2023-12-31",
    "period_type": "quarterly"
  },
  "output_preferences": {
    "report_format": "pdf",
    "detail_level": "standard"
  }
}
```

### Processing Output

**Executive Summary:**
```
TechGrowth Inc. demonstrates strong financial performance with accelerating 
revenue growth and expanding margins. However, working capital management 
and leverage warrant attention.

Key Highlights:
• Revenue growth accelerated to 34% YoY (vs. 28% prior year)
• Gross margin expanded 320 bps to 72.4%
• Operating cash flow increased 45% to $89.2M
• Current ratio declined from 2.1x to 1.6x
• Net debt-to-EBITDA increased to 2.4x from 1.8x

Overall Risk Assessment: MODERATE (Score: 42/100)
```

**Ratio Analysis Dashboard:**
```
┌────────────────────────────────────────────────────────────┐
│              FINANCIAL RATIO ANALYSIS                       │
│                  TechGrowth Inc.                            │
├────────────────────────────────────────────────────────────┤
│                                                            │
│ LIQUIDITY RATIOS                          Current  Prior   │
│ ├─ Current Ratio                          1.62     2.14    │
│ ├─ Quick Ratio                            1.45     1.89    │
│ └─ Cash Ratio                             0.82     1.21    │
│                                                            │
│ PROFITABILITY RATIOS                                       │
│ ├─ Gross Margin                           72.4%    69.2%   │
│ ├─ Operating Margin                       18.2%    15.1%   │
│ ├─ Net Margin                             14.8%    12.3%   │
│ ├─ Return on Assets (ROA)                 12.4%    10.8%   │
│ ├─ Return on Equity (ROE)                 22.1%    18.6%   │
│ └─ Return on Invested Capital (ROIC)      19.3%    15.7%   │
│                                                            │
│ LEVERAGE RATIOS                                            │
│ ├─ Debt-to-Equity                         1.24     0.98    │
│ ├─ Debt-to-Assets                         0.38     0.32    │
│ ├─ Interest Coverage                      8.4x     12.1x   │
│ └─ Net Debt-to-EBITDA                     2.4x     1.8x    │
│                                                            │
│ EFFICIENCY RATIOS                                          │
│ ├─ Asset Turnover                         0.84     0.88    │
│ ├─ Inventory Turnover                     N/A      N/A     │
│ ├─ Receivables Turnover                   6.2x     7.1x    │
│ └─ Days Sales Outstanding                 59       51      │
│                                                            │
│ INDUSTRY BENCHMARKS (Software Sector)                      │
│ ├─ Current Ratio Median                   1.85     ✓       │
│ ├─ Gross Margin Median                    68.5%    ✓       │
│ ├─ Net Margin Median                      11.2%    ✓       │
│ └─ Net Debt-to-EBITDA Median              1.5x     ⚠️      │
│                                                            │
└────────────────────────────────────────────────────────────┘
```

**Key Findings:**
```
┌─────────────────────────────────────────────────────────────┐
│                    KEY FINDINGS                             │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│ 📈 POSITIVE                                                 │
│                                                             │
│ 1. Revenue Acceleration                                     │
│    Revenue growth accelerated from 28% to 34% YoY,         │
│    outpacing industry median of 15%. Driven by enterprise  │
│    segment growth (+52%) and international expansion.       │
│                                                             │
│ 2. Margin Expansion                                         │
│    Gross margin improved 320 bps due to:                   │
│    • Scale efficiencies in cloud infrastructure            │
│    • Product mix shift to higher-margin enterprise deals   │
│    • Pricing optimization initiatives                       │
│                                                             │
│ 3. Strong Cash Generation                                   │
│    Operating cash flow grew 45% to $89.2M, with FCF        │
│    conversion of 24% of revenue - well above industry      │
│    median of 18%.                                           │
│                                                             │
│ ⚠️ ATTENTION NEEDED                                         │
│                                                             │
│ 1. Working Capital Deterioration                            │
│    Current ratio declined from 2.1x to 1.6x due to:        │
│    • 40% increase in accounts receivable (DSO up 8 days)   │
│    • Inventory buildup (although immaterial)               │
│    • Reduced cash position from acquisition                 │
│                                                             │
│ 2. Increasing Leverage                                      │
│    Net debt-to-EBITDA increased to 2.4x from 1.8x:         │
│    • $150M acquisition of DataSync in Q2                   │
│    • Debt-funded share repurchase program                  │
│    • Approaching debt covenant of 3.5x                      │
│                                                             │
│ 📊 TRENDS                                                   │
│                                                             │
│ • Revenue CAGR (3-year): 31%                               │
│ • Margin trend: Improving (5 consecutive quarters)         │
│ • Cash conversion: Stable                                   │
│ • Leverage trend: Increasing (3 consecutive quarters)      │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

**Recommendations:**
```
PRIORITY RECOMMENDATIONS

1. IMMEDIATE: Working Capital Optimization
   Action: Implement AR collection acceleration program
   Impact: Potential $12-15M cash release
   Risk Mitigation: DSO back to 52 days within 2 quarters

2. NEAR-TERM: Leverage Management
   Action: Pause share repurchases; prioritize debt reduction
   Rationale: Maintain covenant headroom; preserve flexibility
   Target: Net debt-to-EBITDA below 2.0x within 12 months

3. ONGOING: Margin Sustainability
   Action: Monitor cloud infrastructure costs vs. revenue scale
   Watch: Gross margin maintenance as growth continues
   Opportunity: Further expansion to 75% achievable

4. STRATEGIC: Acquisition Integration
   Action: Ensure DataSync integration achieves synergies
   Target: $8M annual cost synergies by Q4
   Measure: Accretive to EPS within 18 months
```

---

## Example 2: Credit Risk Assessment

### Input
```json
{
  "analysis_type": "credit_analysis",
  "company_data": {
    "company_name": "Manufacturing Corp",
    "industry": "Industrial Manufacturing"
  },
  "loan_request": {
    "amount": 50000000,
    "purpose": "Equipment financing",
    "term_years": 5
  }
}
```

### Output

**Credit Risk Summary:**
```
┌─────────────────────────────────────────────────────────────┐
│              CREDIT RISK ASSESSMENT                          │
│              Manufacturing Corp                              │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│ OVERALL CREDIT RISK: MODERATE-HIGH                          │
│ Risk Score: 58/100 (Higher = Higher Risk)                   │
│ Recommended Rating: BB (Non-Investment Grade)               │
│                                                             │
│ RISK FACTORS                                                │
│ ├─ Business Risk: 55/100 (Moderate)                        │
│ ├─ Financial Risk: 62/100 (Elevated)                       │
│ ├─ Industry Risk: 50/100 (Moderate)                        │
│ └─ Management Risk: 45/100 (Moderate-Low)                  │
│                                                             │
│ KEY STRENGTHS                                               │
│ ✓ 15+ years operating history                               │
│ ✓ Diversified customer base (no customer >12% revenue)     │
│ ✓ Experienced management team                               │
│ ✓ Consistent profitability                                  │
│                                                             │
│ KEY CONCERNS                                                │
│ ⚠ Leverage at 3.8x Net Debt/EBITDA                         │
│ ⚠ Declining margins (-180 bps YoY)                         │
│ ⚠ Customer concentration risk (top 5 = 42%)                │
│ ⚠ Capital expenditure requirements                          │
│                                                             │
│ DEBT SERVICE ABILITY                                        │
│ ├─ EBITDA: $28.4M                                          │
│ ├─ Interest Coverage: 3.2x                                 │
│ ├─ Debt Service Coverage: 1.8x                             │
│ └─ Fixed Charge Coverage: 1.5x                             │
│                                                             │
│ RECOMMENDATION                                               │
│ ✓ Approve with conditions                                   │
│ • Require 2x interest coverage covenant                     │
│ • Limit additional indebtedness                             │
│ • Quarterly financial reporting                             │
│ • Personal guarantee from owner (60% ownership)             │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

---

## Example 3: Peer Comparison Analysis

### Input
```json
{
  "analysis_type": "peer_comparison",
  "company_data": {
    "company_name": "CloudSoft Inc.",
    "ticker": "CLDS"
  },
  "comparison_peers": ["SNOW", "DDOG", "NET", "NOW"],
  "metrics": ["revenue_growth", "gross_margin", "rule_of_40", "ev_revenue"]
}
```

### Output

**Peer Comparison Dashboard:**
```
┌───────────────────────────────────────────────────────────────────┐
│                    PEER COMPARISON ANALYSIS                        │
│                    Cloud Software Sector                           │
├───────────────────────────────────────────────────────────────────┤
│                                                                   │
│ COMPANY PERFORMANCE RANKINGS                                      │
│                                                                   │
│ Revenue Growth (YoY)                                              │
│ ├─ 1. SNOW: 48% ████████████████████████████████████████████████ │
│ ├─ 2. CLDS: 42% ███████████████████████████████████████████      │
│ ├─ 3. DDOG: 38% ███████████████████████████████████████          │
│ ├─ 4. NET:  35% █████████████████████████████████████            │
│ └─ 5. NOW:  25% ██████████████████████████                       │
│                                                                   │
│ Gross Margin                                                      │
│ ├─ 1. CLDS: 78% ████████████████████████████████████████████████ │
│ ├─ 2. SNOW: 75% ███████████████████████████████████████████████  │
│ ├─ 3. DDOG: 72% █████████████████████████████████████████████    │
│ ├─ 4. NOW:  70% ███████████████████████████████████████████      │
│ └─ 5. NET:  68% █████████████████████████████████████████        │
│                                                                   │
│ Rule of 40 (Growth + Margin)                                      │
│ ├─ 1. CLDS: 58 ████████████████████████████████████████████████  │
│ ├─ 2. SNOW: 57 █████████████████████████████████████████████████ │
│ ├─ 3. DDOG: 52 █████████████████████████████████████████████     │
│ ├─ 4. NET:  48 ███████████████████████████████████████████       │
│ └─ 5. NOW:  42 ███████████████████████████████████████           │
│                                                                   │
│ EV/Revenue Multiple                                               │
│ ├─ 1. SNOW: 18x ████████████████████████████████████████████████ │
│ ├─ 2. DDOG: 14x ███████████████████████████████████████████      │
│ ├─ 3. CLDS: 12x █████████████████████████████████████████        │
│ ├─ 4. NET:  10x █████████████████████████████████████            │
│ └─ 5. NOW:  8x  ██████████████████████████████                   │
│                                                                   │
│ COMPETITIVE POSITION ASSESSMENT                                   │
│                                                                   │
│ CloudSoft (CLDS) is well-positioned relative to peers:           │
│                                                                   │
│ Strengths:                                                        │
│ • Highest gross margin (78%) - best-in-class efficiency          │
│ • Strong Rule of 40 score (58) - balanced growth/profitability   │
│ • Revenue growth above median (42% vs. 38%)                      │
│                                                                   │
│ Areas for Improvement:                                            │
│ • EV/Revenue multiple below top peers                             │
│   Potential undervaluation or lower growth expectations          │
│                                                                   │
│ Implied Valuation Opportunity:                                    │
│ If CLDS traded at median peer multiple (13x):                     │
│   Current: $2.4B → Potential: $2.6B (+8% upside)                 │
│                                                                   │
└───────────────────────────────────────────────────────────────────┘
```

---

## Example 4: Financial Forecasting

### Input
```json
{
  "analysis_type": "forecasting",
  "company_data": {
    "company_name": "RetailCo"
  },
  "forecast_periods": 8,
  "assumptions": {
    "revenue_growth_rate": 0.08,
    "seasonality": true
  }
}
```

### Output

**Revenue Forecast:**
```
┌─────────────────────────────────────────────────────────────────┐
│                 REVENUE FORECAST MODEL                           │
│                 8-Quarter Projection                             │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│ REVENUE FORECAST ($M)                                           │
│                                                                 │
│ Quarter    Base    Seasonal   Forecast    Low    High          │
│           Growth   Adjust                  (80% CI)            │
│ ────────────────────────────────────────────────────────────── │
│ Q1 2024   $52.1    -8%        $47.9      $44.2   $51.6         │
│ Q2 2024   $56.3    +5%        $59.1      $54.8   $63.4         │
│ Q3 2024   $60.8    +3%        $62.6      $57.9   $67.3         │
│ Q4 2024   $65.7    +12%       $73.6      $68.1   $79.1         │
│ Q1 2025   $70.9    -8%        $65.2      $59.3   $71.1         │
│ Q2 2025   $76.6    +5%        $80.4      $73.1   $87.7         │
│ Q3 2025   $82.7    +3%        $85.2      $77.5   $92.9         │
│ Q4 2025   $89.3    +12%       $100.0     $91.0   $109.0        │
│                                                                 │
│ KEY ASSUMPTIONS                                                  │
│ • Base annual growth rate: 8%                                   │
│ • Seasonal patterns based on 5-year historical average          │
│ • No major economic disruption assumed                          │
│                                                                 │
│ MODEL PERFORMANCE                                                │
│ • Historical accuracy (MAPE): 4.2%                              │
│ • R-squared: 0.94                                               │
│ • Confidence level: 80%                                         │
│                                                                 │
│ DRIVERS                                                          │
│ • New store openings: +2 per quarter planned                    │
│ • E-commerce growth: +15% assumed                               │
│ • Same-store sales: +3% assumed                                 │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

---

## Example 5: Variance Analysis

### Input
```json
{
  "analysis_type": "variance_analysis",
  "company_data": {
    "company_name": "SaaS Startup"
  },
  "comparison": {
    "actual_period": "Q4 2023",
    "budget_period": "Q4 2023 Budget"
  }
}
```

### Output

**Budget vs. Actual Analysis:**
```
┌───────────────────────────────────────────────────────────────────┐
│                    BUDGET VARIANCE ANALYSIS                        │
│                    Q4 2023 Performance Review                      │
├───────────────────────────────────────────────────────────────────┤
│                                                                   │
│ LINE ITEM              Budget    Actual   Variance   %Var  Flag  │
│ ═════════════════════════════════════════════════════════════════ │
│                                                                   │
│ REVENUE                                                            │
│ Subscription Revenue   $4,200    $4,580    +$380    +9.0%   ✓    │
│ Professional Services    $300      $245     -$55   -18.3%   ⚠️   │
│ Total Revenue          $4,500    $4,825    +$325    +7.2%   ✓    │
│                                                                   │
│ COST OF REVENUE                                                    │
│ Cloud Infrastructure   $1,260    $1,352     +$92    +7.3%   ⚠️   │
│ Support Staff            $420      $398     -$22    -5.2%        │
│ Total COGS             $1,680    $1,750     +$70    +4.2%        │
│                                                                   │
│ GROSS PROFIT          $2,820    $3,075    +$255    +9.0%   ✓    │
│ Gross Margin           62.7%     63.7%    +1.0pp          ✓    │
│                                                                   │
│ OPERATING EXPENSES                                                 │
│ Sales & Marketing     $1,200    $1,340    +$140   +11.7%   ⚠️   │
│ Product Development     $800      $765     -$35    -4.4%   ✓    │
│ G&A                     $600      $635     +$35    +5.8%        │
│ Total OpEx            $2,600    $2,740    +$140    +5.4%        │
│                                                                   │
│ OPERATING INCOME        $220      $335    +$115   +52.3%   ✓    │
│ Operating Margin        4.9%      6.9%    +2.0pp          ✓    │
│                                                                   │
│ ═════════════════════════════════════════════════════════════════ │
│                                                                   │
│ VARIANCE DRIVERS                                                   │
│                                                                   │
│ ✓ Positive Drivers:                                               │
│   • Subscription revenue beat driven by enterprise wins           │
│   • Product development under budget - delayed hiring             │
│   • Cloud efficiency improvements offset higher volume            │
│                                                                   │
│ ⚠️ Negative Drivers:                                              │
│   • S&M overspend on customer acquisition campaigns               │
│   • Cloud costs above budget due to traffic spike                 │
│   • Professional services shortfall - project delays              │
│                                                                   │
│ RECOMMENDATIONS                                                    │
│ 1. Investigate enterprise sales success for replication           │
│ 2. Review S&M spend efficiency (CAC increased 15%)                │
│ 3. Plan for cloud capacity to handle growth                       │
│ 4. Address professional services pipeline                         │
│                                                                   │
└───────────────────────────────────────────────────────────────────┘
```

---

## Example 6: Early Warning Alert

### System Alert
```
┌─────────────────────────────────────────────────────────────┐
│                  ⚠️ EARLY WARNING ALERT                      │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│ Company: RetailCo Inc.                                      │
│ Alert Type: Financial Distress Indicator                    │
│ Severity: HIGH                                              │
│ Generated: January 15, 2024 09:32 AM                        │
│                                                             │
│ ALERT DETAILS                                                │
│                                                             │
│ Multiple warning indicators triggered:                      │
│                                                             │
│ 1. CURRENT RATIO DECLINE                                    │
│    Current: 0.95 (Below 1.0 threshold)                      │
│    Previous: 1.32 (3 months ago)                            │
│    Trend: Declining for 4 consecutive months                │
│                                                             │
│ 2. INTEREST COVERAGE DETERIORATION                          │
│    Current: 1.8x (Below 2.0x threshold)                     │
│    Previous: 2.9x (6 months ago)                            │
│    Risk: Covenant breach imminent at 1.5x                   │
│                                                             │
│ 3. WORKING CAPITAL DECLINE                                  │
│    Current: -$2.3M (Negative)                               │
│    Change: -$8.1M from prior quarter                        │
│    Cause: AR collection slowdown + inventory buildup        │
│                                                             │
│ 4. CASH CONVERSION CYCLE                                    │
│    Current: 87 days (vs. industry median 45 days)           │
│    DSO: 62 days (vs. historical 48 days)                    │
│                                                             │
│ RECOMMENDED IMMEDIATE ACTIONS                                │
│                                                             │
│ 1. Review AR aging - implement collection acceleration      │
│ 2. Negotiate temporary covenant waiver with lenders         │
│ 3. Evaluate short-term financing options                    │
│ 4. Review inventory management and slow-moving stock        │
│ 5. Schedule call with CFO within 24 hours                   │
│                                                             │
│ This alert has been sent to:                                │
│ • CFO, Treasurer, Controller                                │
│ • Relationship Manager                                      │
│ • Risk Management Team                                      │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```
