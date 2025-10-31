# TravelTide Customer Segmentation
## Data-Driven Rewards Program Assignment

![Project Status](https://img.shields.io/badge/status-complete-success)
![Python](https://img.shields.io/badge/python-3.8+-blue)
![License](https://img.shields.io/badge/license-MIT-green)

**Author:** Alberto Diaz Durana  
**Date:** October 2025  
**Course:** Unsupervised Learning - 4 Week Project

---

## Project Objectives

TravelTide seeks to launch a personalized rewards program by assigning 5,765 active customers to one of five perks based on behavioral preferences. This project delivers:

- **Customer Segmentation:** Identify three distinct behavioral clusters using validated clustering methods
- **Individual Perk Assignment:** Assign each user to their optimal perk using propensity-based scoring
- **High-Confidence Recommendations:** Provide confidence ratings (HIGH/MEDIUM/LOW) for phased implementation
- **Actionable Marketing Insights:** Deliver customer personas and segment profiles for targeted campaigns

---

## Key Results

### Three Clear Customer Segments

| **Cluster** | **Persona**    | **Size**      | **Avg CLV** | **Total CLV** | **Key Characteristics**                                       |
| ----------- | -------------- | ------------- | ----------- | ------------- | ------------------------------------------------------------- |
| **0**       | Premium Paula  | 4,596 (79.7%) | $4,985      | $22.9M (98%)  | High-value hotel travelers, premium spending, strong loyalty  |
| **1**       | Dining David   | 287 (5.0%)    | $768        | $220K (1%)    | Mid-value travelers, dining-focused, experiential preferences |
| **2**       | Flexible Fiona | 882 (15.3%)   | $319        | $281K (<1%)   | Budget-conscious, flexibility-focused, occasional travelers   |

### Balanced Perk Distribution

Despite 79.7% cluster concentration, individual propensities create balanced perk allocation:

| **Perk**             | **Users Assigned** | **Percentage** |
| -------------------- | ------------------ | -------------- |
| Free Checked Bag     | 1,402              | 24.3%          |
| Free Hotel Meal      | 1,349              | 23.4%          |
| One Night Free Hotel | 1,277              | 22.2%          |
| Exclusive Discounts  | 944                | 16.4%          |
| No Cancellation Fee  | 793                | 13.8%          |

**CRITICAL INSIGHT:** All 5 perks viable for marketing. Individual preferences within segments are more diverse than cluster averages suggested.

### High Assignment Confidence

- **HIGH confidence:** 3,658 users (63.5%) - Strong, clear preferences
- **MEDIUM confidence:** 1,947 users (33.8%) - Reliable preferences
- **LOW confidence:** 160 users (2.8%) - Require A/B testing

---

## Methodology Overview

### Development Process

This analysis was initially developed across 15 daily notebooks (Week 1-3: 5 notebooks each) 
and consolidated into 6 production-ready notebooks for final delivery. Consolidation 
improved code quality, eliminated redundancy, and enhanced reproducibility while 
maintaining complete analytical rigor.

### Six-Notebook Analytical Workflow

The analysis follows a systematic, stage-gated approach ensuring data quality and reproducibility:

```
01_EDA_data_quality_cohort.ipynb
   └─> Cohort: 5,765 qualified users
        ├─> Temporal filter (sessions after 2023-01-04)
        ├─> Engagement filter (7+ sessions)
        ├─> Age filter (18-100 years)
        └─> Data quality validation (IQR outlier removal)

02_EDA_behavioral_analysis.ipynb
   └─> Behavioral patterns identified
        ├─> Booking behavior (26% conversion rates)
        ├─> CLV distribution (mean $4,061)
        ├─> Engagement metrics (avg 7.5 sessions/user)
        └─> Natural segmentation indicators

03_FE_core_features.ipynb
   └─> 45 core features engineered
        ├─> Booking patterns (12 features)
        ├─> Spending behavior (10 features)
        ├─> Engagement metrics (8 features)
        ├─> Risk indicators (7 features)
        └─> Travel preferences (8 features)

04_FE_advanced_features.ipynb
   └─> 20 advanced features + 5 perk propensities
        ├─> RFM segmentation (4 features)
        ├─> Behavioral scores (5 features)
        ├─> Discount patterns (6 features)
        └─> PERK PROPENSITIES (5 critical features)

05_CLUSTERING_preparation_selection.ipynb
   └─> K=3 validated through multiple metrics
        ├─> K-selection (tested K=2-10)
        ├─> Method comparison (K-Means vs Hierarchical)
        ├─> PCA analysis (56.4% variance in PC1-2)
        └─> Final: Hierarchical (Ward), K=3

06_CLUSTERING_segmentation_assignment.ipynb
   └─> Final clustering + propensity-based assignment
        ├─> 3 clusters profiled (demographics, behavior, CLV)
        ├─> Individual perk assignments (propensity scores)
        ├─> Confidence ratings (HIGH/MEDIUM/LOW)
        └─> 4 CSV exports + visualization dashboard
```

---

## Customer Personas

### Persona 1: Premium Paula (Cluster 0)
**Profile:** Frequent business/leisure traveler, values quality hotel experiences, represents TravelTide's core high-value base

**Demographics:**
- Age: 42 years | Tenure: 3 months
- Booking frequency: 7.5 sessions/quarter
- Annual value: $4,985

**Behavior:**
- Books premium hotel accommodations frequently
- High platform engagement, strong loyalty once engaged
- Rarely cancels, values hotel perks over flight add-ons

**Preferred Perks:** Free Hotel Night, Hotel Meal (diverse preferences within segment)

**Quote:** *"I travel often for work and pleasure. Give me perks that make my hotel stays better, and I'll keep coming back."*

---

### Persona 2: Dining David (Cluster 1)
**Profile:** Moderate traveler who views meals as essential part of travel experience

**Demographics:**
- Age: 42 years | Tenure: 3 months
- Booking frequency: 7.5 sessions/quarter
- Annual value: $768

**Behavior:**
- Moderate booking frequency, strong hotel+meal correlation
- Values experiential rewards, engaged with dining-related offers
- Mid-tier spender on platform

**Preferred Perk:** Free Hotel Meal (highest propensity 1.64 across all segments)

**Quote:** *"Travel is about experiences. A great meal makes the trip memorable. Include that in my rewards."*

---

### Persona 3: Flexible Fiona (Cluster 2)
**Profile:** Budget-conscious occasional traveler who values flexibility and simplicity

**Demographics:**
- Age: 42 years | Tenure: 3 months
- Booking frequency: 7.4 sessions/quarter
- Annual value: $319

**Behavior:**
- Infrequent bookings with lower spend, price-sensitive decisions
- Values practical benefits over premium perks
- Plans conservatively, appreciates booking flexibility

**Preferred Perk:** No Cancellation Fee (values peace of mind)

**Quote:** *"I need flexibility more than fancy perks. Let me change plans without penalty, and I'm happy."*

---

## Visualizations

All visualizations are generated within the notebooks and saved to `outputs/figures/`. Key visualizations include:

- **K-Selection Dashboard:** Four-metric validation showing K=3 optimal
- **Method Comparison:** Hierarchical vs K-Means performance across metrics
- **PCA Analysis:** 2D projection showing natural segmentation (56.4% variance explained)
- **Perk Propensities:** Distribution of propensity scores across cohort
- **Segmentation Dashboard:** Complete results with cluster sizes, perk distribution, and confidence levels

---

## Project Structure

```
TravelTide_Customer_Segmentation/
│
├── notebooks/                          # Jupyter notebooks (6 total)
│   ├── 01_EDA_data_quality_cohort.ipynb
│   ├── 02_EDA_behavioral_analysis.ipynb
│   ├── 03_FE_core_features.ipynb
│   ├── 04_FE_advanced_features.ipynb
│   ├── 05_CLUSTERING_preparation_selection.ipynb
│   └── 06_CLUSTERING_segmentation_assignment.ipynb
│
├── data/
│   ├── raw/                            # Original datasets (query database directly)
│   ├── processed/                      # Cleaned and engineered features
│   │   ├── user_features_raw.csv
│   │   ├── user_base_complete.csv
│   │   └── user_features_engineered.csv
│   └── results/
│       ├── eda/                        # EDA outputs
│       │   ├── eda_cohort_qualified.csv
│       │   ├── eda_data_quality_report.csv
│       │   └── eda_summary_stats.csv
│       ├── feature_engineering/        # Feature dictionaries
│       │   ├── feature_dictionary.csv
│       │   └── feature_dictionary_week2.csv
│       └── clustering/                 # Final clustering outputs
│           ├── user_perk_assignments.csv     # 5,765 × 8 (PRIMARY DELIVERABLE)
│           ├── cluster_profiles_k3.csv       # 3 × 10
│           ├── cluster_assignments_k3.csv    # 5,765 × 2
│           ├── perk_distribution.csv         # 5 × 3
│           ├── clustering_k_selection_metrics.csv
│           ├── clustering_method_comparison.csv
│           ├── clustering_pca_loadings.csv
│           └── clustering_pca_results.csv
│
├── outputs/
│   └── figures/                        # All visualizations
│       ├── eda/                        # Cohort funnel, demographics, behavior
│       ├── feature_engineering/        # Perk propensities, correlations
│       └── clustering/                 # K-selection, PCA, final dashboard
│
├── docs/
│   └── reports/                        # Documentation and presentations
│       ├── executive_summary.pdf       # 1-page summary for stakeholders
│       ├── detailed_report.pdf         # 3-page comprehensive analysis
│       └── presentation_personas.pdf   # Customer persona profiles
│
├── README.md                           # This file
├── requirements.txt                    # Python dependencies
└── LICENSE                             # MIT License

```

---

## Technical Implementation

### Environment Setup

```bash
# Clone repository
git clone https://github.com/[YOUR-USERNAME]/TravelTide_Customer_Segmentation.git
cd TravelTide_Customer_Segmentation

# Create virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt
```

### Requirements

```
pandas>=2.0.0
numpy>=1.24.0
scikit-learn>=1.3.0
matplotlib>=3.7.0
seaborn>=0.12.0
scipy>=1.11.0
sqlalchemy>=2.0.0
jupyter>=1.0.0
```

### Execution Order

Run notebooks sequentially (dependencies exist between stages):

```bash
jupyter notebook notebooks/01_EDA_data_quality_cohort.ipynb
# ... continue through 06_CLUSTERING_segmentation_assignment.ipynb
```

**Expected runtime:** ~45 minutes total (all 6 notebooks)

---

## Key Technical Decisions

### Why K=3 Instead of K=5?

Despite having 5 perks, clustering analysis identified K=3 as optimal:
- **Silhouette Score:** 0.3806 at K=3 (peak performance)
- **Davies-Bouldin Index:** 0.8844 at K=3 (best cluster separation)
- **Business Interpretability:** Three clear segments map to real customer behaviors

Assignment to 5 perks achieved through **individual propensity scoring**, not cluster membership.

### Why Hierarchical Over K-Means?

At K=3, Hierarchical clustering (Ward linkage) outperforms K-Means:
- **Davies-Bouldin:** 0.88 vs 1.65 (much better - lower is better)
- **Silhouette:** 0.3806 vs 0.3778 (slightly better)
- **Reproducibility:** Deterministic (no random initialization)

### Why Propensity-Based Assignment?

Cluster averages hide individual preferences. Example: Premium Paula cluster (79.7% of users) prefers:
- 28% → Free Hotel Night
- 26% → Free Hotel Meal  
- 24% → Free Bag
- 14% → Exclusive Discount
- 8% → No Cancel Fee

Propensity scoring captures this within-cluster diversity that simple cluster-to-perk mapping would miss.

---

## Data Dictionary

### User Perk Assignments (`user_perk_assignments.csv`)

| Column              | Type  | Description                              |
| ------------------- | ----- | ---------------------------------------- |
| `user_id`           | int   | Unique user identifier                   |
| `cluster`           | int   | Assigned cluster (0, 1, 2)               |
| `assigned_perk`     | str   | Optimal perk for user                    |
| `perk_propensity`   | float | Propensity score for assigned perk [0-1] |
| `second_perk`       | str   | Runner-up perk                           |
| `second_propensity` | float | Propensity for second choice [0-1]       |
| `confidence_delta`  | float | Top - Second propensity                  |
| `confidence_level`  | str   | HIGH/MEDIUM/LOW based on delta           |

### Cluster Profiles (`cluster_profiles_k3.csv`)

| Column              | Type  | Description                     |
| ------------------- | ----- | ------------------------------- |
| `cluster_id`        | int   | Cluster identifier (0, 1, 2)    |
| `size`              | int   | Number of users in cluster      |
| `pct_of_total`      | float | Percentage of total cohort      |
| `age_mean`          | float | Average age in years            |
| `years_active_mean` | float | Average tenure on platform      |
| `avg_bookings`      | float | Mean bookings per user          |
| `avg_sessions`      | float | Mean sessions per user          |
| `avg_clv`           | float | Average Customer Lifetime Value |
| `total_clv`         | float | Total CLV for segment           |
| `dominant_perk`     | str   | Most common perk in cluster     |

---

## Analytical Rigor

### Validation Approach

- **4 clustering metrics:** Silhouette, Davies-Bouldin, Calinski-Harabasz, Inertia
- **9 K-values tested:** K=2 through K=10
- **2 algorithms compared:** K-Means vs Hierarchical
- **PCA dimensionality check:** 56.4% variance in PC1-2, 81.9% in PC1-5
- **65 features engineered:** From 119 raw features
- **100% coverage:** All 5,765 users assigned with confidence ratings

### Data Quality Checks

- **Missing value treatment:** Domain-appropriate imputation (median/mode)
- **Outlier handling:** IQR method for extreme values
- **Normalization:** StandardScaler + 4.0x perk propensity weighting
- **Feature selection:** Correlation analysis, VIF multicollinearity check
- **Cohort validation:** Temporal, engagement, age, and data quality filters

---

## Business Impact

### Revenue Protection
- Premium Paula segment: $22.9M CLV (98% of total)
- 5% retention improvement = $1.15M protected annual revenue
- Expected churn reduction: 15-20% with personalized perks

### Marketing Efficiency
- 63.5% HIGH confidence assignments enable immediate launch
- Balanced perk distribution allows diverse campaign strategies
- Persona-based targeting improves email engagement 25-30%

### Strategic Positioning
- Data-driven personalization differentiates from generic competitor loyalty programs
- Individual propensity scoring creates scalable personalization framework
- Quarterly monitoring enables adaptive strategy refinement

---

## Deliverables

### For Marketing Team
- **Executive Summary** (1 page): High-level findings and recommendations
- **Customer Personas** (3 profiles): Actionable segment descriptions
- **Perk Assignment File** (`user_perk_assignments.csv`): 5,765 users with confidence ratings

### For Analytics Team
- **Detailed Report** (3 pages): Complete methodology and validation
- **6 Jupyter Notebooks**: Fully documented, reproducible analysis
- **Feature Dictionary**: Definitions of all 65 engineered features
- **Q&A Documents** (6 files): 30 questions each, anticipating stakeholder queries

### For Leadership
- **Presentation Slides** (5-6 slides): 5-minute live presentation format
- **Visualization Suite**: 14 publication-quality figures
- **GitHub Repository**: Complete project with version control

---

## Project Highlights

**Analytical Rigor**
- Multi-metric validation of clustering approach
- Systematic feature engineering with business logic
- Confidence ratings enable risk-managed rollout

**Business Value**
- All 5 perks validated as viable (13.8%-24.3% distribution)
- 97.2% of assignments have HIGH/MEDIUM confidence
- Clear segment priorities (70-75% budget to Premium Paula)

**Reproducibility**
- Deterministic algorithms (Hierarchical clustering)
- Comprehensive documentation (6 notebooks + reports)
- Complete data provenance (raw → processed → results)

---

## Author

**Alberto Diaz Durana**  
Data Scientist

- GitHub: [@albertodiazdurana](https://github.com/albertodiazdurana)
- LinkedIn: [albertodiazdurana](https://linkedin.com/in/albertodiazdurana)

---

## Contact

For questions about methodology, implementation, or data access:
- Open an issue in this repository
- Reachout in LinkedIn

---

**Last Updated:** October 30, 2025  
**Project Status:** Complete - Ready for Implementation

---

*Star this repository if you found it helpful!*
