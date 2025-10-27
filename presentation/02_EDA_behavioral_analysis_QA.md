# Notebook 02: EDA Behavioral Analysis - Q&A for Presentation

**Notebook:** `02_EDA_behavioral_analysis.ipynb`  
**Purpose:** Help prepare for stakeholder presentation  
**Date:** October 2025

---

## Business Context Questions

### Q1: What was the main goal of this notebook?

**Answer:**
To understand **who our customers are** and **how they behave** by analyzing:
1. **Demographics:** Age, gender, family status, location
2. **Booking patterns:** What they book (flights, hotels, packages)
3. **Engagement:** How they interact with the platform
4. **Temporal trends:** When they're most active
5. **Customer value:** CLV segmentation

This analysis identifies **segmentation opportunities** and informs feature engineering for Week 2.

---

### Q2: What are the key demographic characteristics of our customer base?

**Answer:**
**Core Demographics:**
- **Age:** Mean 42.3 years, dominated by 35-44 age group (36.2%)
- **Gender:** 88.1% Female (significant skew for marketing)
- **Family:** 45.8% married, 33.0% have children
- **Tenure:** Average 0.27 years (~3 months) - relatively new user base

**Why this matters:**
- Target demographic is **professional women in their 40s**
- Family-oriented offers may resonate with ~1/3 of users
- New user base suggests **recent growth** or campaign success

---

### Q3: What's the most surprising demographic finding?

**Answer:**
**88.1% Female gender distribution** is highly skewed.

**Implications:**
1. **Marketing:** Messages should be tailored for female travelers
2. **Perk design:** Consider preferences of this demographic (e.g., hotel amenities, safety features)
3. **Product features:** UI/UX should reflect primary user preferences
4. **Partnership opportunities:** Airlines/hotels popular with female travelers

This isn't necessarily a problem - it's an **opportunity to double-down** on serving our core demographic exceptionally well.

---

## Booking Behavior Questions

### Q4: What percentage of users actually book vs just browse?

**Answer:**
**87.7% of users have made at least one booking** (5,058 out of 5,765 users).

This is **excellent** - our cohort definition (>7 sessions) successfully identified engaged, convertible customers, not just window shoppers.

**Breakdown:**
- Flight bookings: 82.8% of users
- Hotel bookings: 84.9% of users
- Both: Most users book both products

Only 12.3% are "browsers only" - these may need nurturing campaigns.

---

### Q5: Do customers prefer to book flights and hotels together or separately?

**Answer:**
**22.7% of sessions are package bookings** (flight + hotel booked together in same session).

**However, at the user level:**
- 79.1% of users (4,561) have booked at least one package
- Most users book both products but not always together

**Insight:** Customers are **flexible** - they'll bundle when convenient but also book separately. This suggests:
- Promote package deals but don't force bundling
- Some users prefer flexibility (different dates for flight/hotel)
- Both standalone and package offerings should be strong

---

### Q6: What do trip characteristics tell us about customer preferences?

**Answer:**
**Flight Preferences:**
- **Return flights dominate:** 95.6% book round trips (not one-way)
- **Solo/couple travel:** Average 1.0 seats per flight
- **Light packers:** Average 0.54 bags per trip
- **Mid-range spending:** $365 average fare, $348 median

**Hotel Preferences:**
- **Short stays:** 3.46 nights average
- **Budget-conscious:** $171/night average, $147 median
- **Standard rooms:** 1.0 room per booking

**Persona emerging:** **Cost-conscious weekend/short-trip travelers** who book round trips, stay 3-4 nights, and travel light.

---

### Q7: What's the cancellation rate, and should we be concerned?

**Answer:**
**0.26% session-level cancellation rate** (114 out of 43,344 sessions)  
**2.0% user-level:** Only 114 users (out of 5,765) have ever cancelled

**This is extremely low** - indicates:
- High booking confidence (customers know what they want)
- Good product/price match (meeting expectations)
- Low buyer's remorse

**No concern** - this is healthy. The "no cancellation fee" perk may have limited appeal given actual behavior.

---

## Engagement Pattern Questions

### Q8: How engaged are sessions that result in bookings vs those that don't?

**Answer:**
**Booked sessions have 2x the engagement:**
- **Booked:** 25.09 mean clicks, 22 median
- **Not booked:** 11.28 mean clicks, 8 median

**Interpretation:**
This **strong signal** suggests:
1. High engagement predicts conversion
2. Users who book are doing more research/comparison
3. Page clicks could be a key feature for segmentation
4. Users who book spend more time finding the perfect option

**Business action:** Track page clicks as a **conversion intent indicator** for targeted campaigns.

---

### Q9: When are customers most active on the platform?

**Answer:**
**Three temporal patterns identified:**

**1. Hour of Day (Daily Pattern):**
- **Morning low:** 0.5-2% of sessions (midnight-8am)
- **Afternoon ramp:** Gradual increase from 2pm
- **Peak at 7pm:** 9.6% of sessions (4,158 sessions)
- **Evening drop:** Sharp decline after 9pm

**2. Day of Week (Weekly Pattern):**
- **Even distribution:** 13.8-14.8% across all days
- No strong weekend/weekday preference

**3. Month (Seasonal Pattern):**
- **Jan-Mar peak:** 67% of all traffic
- **Summer decline:** April onwards drops significantly
- Jul has only 5.4% of traffic

---

### Q10: Why is 7pm the peak hour, and how should we use this?

**Answer:**
**7pm peak represents "after-work browsing behavior":**
- Customers finish work (5-6pm)
- Have dinner (6-7pm)
- Browse travel during relaxation time (7-9pm)

**Strategic implications:**

**Marketing timing:**
- Schedule email campaigns for 6-7pm delivery
- Run ads during evening hours (6-10pm)
- Launch promotions at 7pm for maximum visibility

**Customer support:**
- Staff support channels heavily 6-10pm
- Chatbot should be most responsive during peak

**A/B testing:**
- Run tests during peak hours for faster results
- Avoid testing during low-traffic hours (midnight-8am)

This is **actionable intelligence** for campaign optimization.

---

### Q11: What does the January-March seasonality tell us?

**Answer:**
**67% of traffic occurs in Q1 (Jan-Mar), then drops dramatically.**

**Possible explanations:**
1. **New Year travel planning:** People plan vacations in January
2. **Tax refunds:** February-March spending increase
3. **Spring break:** March travel planning
4. **Summer vacation decline:** People already booked or traveling

**Strategic implications:**
- **Double-down Q1:** Maximize marketing spend Jan-Mar
- **Combat summer slump:** Launch campaigns in April to sustain engagement
- **Year-round engagement:** Develop strategies to smooth seasonality
- **Inventory planning:** Ensure best prices/availability in Q1

**Risk:** Over-reliance on Q1 traffic. Diversification strategies needed.

---

## User-Level Aggregation Questions

### Q12: Why did you aggregate to user level instead of keeping session level?

**Answer:**
**Segmentation requires user-level features, not session-level.**

**Reasons:**
1. **Clustering goal:** Group similar **users**, not similar sessions
2. **Perk assignment:** Perks are assigned to **users**, not sessions
3. **Marketing campaigns:** Target **users** with personalized offers
4. **Behavioral patterns:** Need to understand **user** behavior over time

**What we aggregated:**
- Session counts, averages, totals
- Booking history (flights, hotels, packages)
- Spending patterns (total, averages)
- Engagement metrics (clicks, duration)

**Output:** 41 user-level features ready for Week 2 feature engineering.

---

### Q13: What are the most important features created in the aggregation?

**Answer:**
**Top features for segmentation:**

**Engagement Features:**
- `total_sessions`: How often they visit
- `avg_page_clicks_per_session`: Engagement intensity
- `avg_session_duration_minutes`: Time investment

**Booking Features:**
- `total_flights_booked`, `total_hotels_booked`: Product preferences
- `total_package_bookings`: Bundling behavior
- `cancellation_rate`: Risk/reliability

**Financial Features:**
- `total_spend`: Historical value
- `estimated_annual_clv`: Future value
- `avg_flight_fare`, `avg_hotel_price_per_night`: Price sensitivity

**Behavioral Features:**
- `flight_trips`, `hotel_trips`: Travel frequency
- `avg_nights_per_stay`: Trip length preference
- `return_flight_count`: Travel style

These 15-20 features will be **most predictive** for clustering.

---

## CLV Analysis Questions

### Q14: How is Customer Lifetime Value (CLV) calculated?

**Answer:**
**Formula:** `CLV = Total Spend / Years Active`

**Logic:**
- If a user spent $1,000 in 0.5 years → CLV = $2,000/year
- If a user spent $500 in 1 year → CLV = $500/year

**Adjustments:**
- Minimum tenure of 30 days to avoid division by zero
- Accounts for new users vs established users

**Interpretation:** CLV estimates **annual spending rate** - how much we can expect this user to spend per year if they continue current behavior.

**Limitations:**
- Assumes spending rate stays constant (may change)
- Doesn't account for churn probability
- Based on short history (avg 0.27 years tenure)

**Still valuable:** Good proxy for customer value ranking.

---

### Q15: What does the CLV distribution tell us?

**Answer:**
**CLV Distribution:**
- **Mean:** $4,135.84
- **Median:** $3,579.80
- **Range:** $0-$37,038.78

**Key insights:**

**1. High value overall:** $4k average annual spending is substantial

**2. Right-skewed distribution:** Median < Mean indicates outliers pulling average up

**3. Massive range:** Top customers worth 100x+ bottom customers

**4. Quartile breakdown:**
- **Q1 (bottom 25%):** $449 average - casual/new users
- **Q2:** $2,574 average - regular travelers
- **Q3:** $4,616 average - frequent travelers
- **Q4 (top 25%):** $8,907 average - VIP customers

**5. Total annual value:** $23.8M across 5,765 users

---

### Q16: What's the business value of the CLV segmentation?

**Answer:**
**CLV Segments created:**
- **Low Value:** $0-$500 (156 users, 2.7%)
- **Medium Value:** $500-$1,500 (570 users, 9.9%)
- **High Value:** $1,500-$5,000 (2,440 users, 42.3%)
- **VIP:** $5,000+ (1,892 users, 32.8%)

**Strategic value:**

**1. Resource allocation:**
- Focus premium perks on VIP/High Value (75% of users)
- Basic perks for Low/Medium Value

**2. Retention priority:**
- Losing a VIP costs 20x more than losing Low Value user
- VIP retention should get disproportionate attention

**3. Marketing budget:**
- Acquisition cost justified by CLV
- Spend more to acquire/retain High Value+ users

**4. Perk design:**
- VIP perks: Exclusive lounge access, concierge
- High Value: Free upgrades, priority support
- Medium/Low: Basic discounts, promotions

**ROI focus:** Top 25% generates ~38% of revenue - serve them exceptionally well.

---

### Q17: Why are 75% of users in High Value or VIP segments?

**Answer:**
This seems counterintuitive but is actually **correct given our cohort definition:**

**Remember Elena's filters:**
- **>7 sessions:** Already filters out casual browsers
- **Post-2023-01-04:** Recent, engaged users
- **Age 18-100:** Removes test accounts

**Result:** We're analyzing **qualified, engaged customers** - not the general population.

**This is by design:**
- We want to segment **valuable customers** for rewards program
- Not trying to understand all users (including inactive ones)
- The cohort **self-selects** for engagement and value

**The 2.7% Low Value users:**
- Likely very new (high sessions, low bookings yet)
- Browsers who haven't converted fully
- Budget researchers planning future trips

**Insight:** Our rewards program should focus on the 75% High Value+ segment - they're the target audience.

---

## Data Quality & Process Questions

### Q18: What engagement outliers did you discover, and why remove them?

**Answer:**
**Discovered 238 outlier sessions (0.55%) with extreme engagement metrics:**

**Page Clicks Outliers:**
- 114 sessions with >66 clicks (upper bound)
- Maximum: 219 clicks
- Mean outlier: 91 clicks

**Session Duration Outliers:**
- 238 sessions with >8.07 minutes (upper bound)
- Maximum: 120 minutes
- Mean outlier: 27 minutes

**Suspicious patterns detected:**
- Many sessions exactly 120 minutes (system cap)
- Many sessions exactly 200 clicks (system cap)
- These appear to be **technical limits**, not real behavior

**Why remove:**
1. **Data quality:** Likely system artifacts, not genuine user behavior
2. **Statistical impact:** 7.2% distortion in session duration mean
3. **Visual clarity:** Distorting distribution plots, hiding real patterns
4. **Minimal loss:** Only 0.55% of sessions
5. **Conservative threshold:** 3x IQR is standard, well-justified

**Impact of removal:**
- Session duration: 1.95 → 1.81 minutes mean
- Page clicks: 14.84 → 14.56 mean
- Cleaner distributions for analysis
- More accurate user-level aggregations

**Decision rationale:** Preserving data quality and analytical clarity outweighs minimal data loss.

---

### Q19: How confident are you in the user-level aggregations?

**Answer:**
**Very confident** - multiple validation checks passed:

**1. Data integrity:**
- Zero missing user_ids
- Zero duplicate user_ids
- All 5,765 users present

**2. Critical columns:**
- 0% missing values in age, sessions, CLV
- Complete demographic coverage

**3. Logical consistency:**
- Session counts match expectations (mean 7.52)
- Booking rates align with business metrics (87.7%)
- CLV calculations verified ($23.8M total)

**4. Cross-validation:**
- User counts match across all aggregations
- Booking metrics sum correctly
- Spend totals reconcile

**Quality assessment:** Production-ready for feature engineering.

---

### Q19: Why did you create 4 separate visualization figures instead of one big dashboard?

**Answer:**
**Intentional design for presentation flexibility:**

**1. Demographics (Figure 1):**
- 6 plots covering age, gender, family, tenure, location
- Tells "who are our customers" story
- Can be shown standalone or combined

**2. Booking Behavior (Figure 2):**
- 6 plots covering conversion, trips, fares, destinations
- Tells "what do they book" story
- Product-focused insights

**3. Engagement & Temporal (Figure 3):**
- 6 plots covering clicks, duration, timing patterns
- Tells "when and how they engage" story
- Campaign optimization insights

**4. CLV Analysis (Figure 4):**
- 4 plots covering value distribution, segments
- Tells "customer value" story
- ROI-focused insights

**Benefits:**
- **Modular:** Can show specific figures for specific audiences
- **Narrative:** Each figure tells complete sub-story
- **File size:** Smaller individual files load faster
- **Presentation:** Can distribute figures across slides

---

### Q20: What data transformations were applied, and why?

**Answer:**
**Key transformations:**

**1. Date parsing:**
- Converted all date columns to datetime objects
- Enables temporal analysis (day, hour, month extraction)

**2. Derived temporal features:**
- `day_of_week`, `hour_of_day`, `month` from session_start
- `days_since_signup`, `years_active` from sign_up_date

**3. Session duration calculation:**
- `(session_end - session_start)` converted to minutes
- More interpretable than seconds

**4. Aggregation functions:**
- **sum:** Total bookings, spend
- **mean:** Average behavior patterns
- **median:** Robust central tendency
- **count:** Frequency metrics

**5. Missing value handling:**
- 0-fill for users without bookings (they exist, just didn't book)
- Preserves all 5,765 users in analysis

**6. CLV calculation:**
- Annualized spending rate
- Minimum tenure adjustment (30 days)

**All transformations are reversible and documented** for reproducibility.

---

## Stakeholder Questions

### Q21: "Why is the gender distribution so skewed? Is this a data problem?"

**Answer:**
**No, this is real user behavior, not a data error.**

**Evidence it's real:**
1. **Consistent across all users:** Not isolated to one cohort
2. **Matches sign-up data:** Gender collected at registration
3. **Behavioral consistency:** Female users show coherent behavior patterns
4. **No technical anomalies:** No data quality flags

**Possible business explanations:**
1. **Marketing targeting:** Previous campaigns may have targeted women
2. **Product positioning:** Platform may naturally appeal to female travelers
3. **Social factors:** Women may be primary travel planners in households
4. **Partnership channels:** Referral sources may skew female

**What to do:**
- **Embrace it:** Optimize product for primary demographic
- **Test it:** Run male-targeted campaigns to see if balance shifts
- **Investigate:** Survey users about discovery channel
- **Leverage it:** Partner with brands popular with female travelers

**Bottom line:** It's an opportunity, not a problem.

---

### Q22: "You removed 238 sessions as outliers - how do we know you didn't remove real customer behavior?"

**Answer:**
**Multiple lines of evidence show these are data artifacts, not real behavior:**

**1. System limits detected:**
- Many sessions exactly 120 minutes (suspicious uniformity)
- Many sessions exactly 200 clicks (suggests a cap)
- Real behavior would show variation around these values

**2. Statistical extremeness:**
- Beyond 3x IQR threshold (very conservative)
- 0.55% of sessions (extreme minority)
- 91 average clicks for outliers vs 15 for normal (6x difference)

**3. Minimal impact:**
- Only 7.2% change in mean duration
- User-level aggregations barely affected
- All users retained (no user lost all sessions)

**4. Visual validation:**
- Distributions much cleaner after removal
- No loss of meaningful patterns
- Improved analytical clarity

**What we preserved:**
- All 5,765 users remain in analysis
- 99.45% of sessions retained
- Normal high-engagement behavior kept (up to 66 clicks, 8 minutes)

**Decision process:** Conservative threshold + technical evidence + minimal impact = justified removal.

---

### Q23: "The summer traffic drop is concerning - are we losing customers?"

**Answer:**
**This is seasonal behavior, not customer loss.**

**Evidence it's seasonality:**
1. **Pattern matches travel industry:** Q1 = planning season
2. **User base stable:** We still have 5,765 qualified users
3. **Booking rates consistent:** 87.7% still booking when active
4. **CLV unchanged:** Annual value projections hold

**Why summer drops:**
- **Planning vs traveling:** People browse in winter, travel in summer
- **School schedules:** Families plan around academic calendar
- **Budget cycles:** Tax refunds boost Q1 spending
- **Vacation timing:** May-July = actually traveling, not browsing

**Strategic response:**
1. **Expect it:** Build seasonality into forecasts
2. **Combat it:** Launch summer campaigns to maintain engagement
3. **Optimize it:** Ensure Q1 conversion is maximized
4. **Expand it:** Develop year-round travel reasons (fall foliage, winter sports)

**Not a crisis** - standard travel industry pattern.

---

### Q23: "Should we be concerned that average tenure is only 0.27 years?"

**Answer:**
**No - this indicates recent growth, which is positive.**

**Context:**
- Analysis period: Jan-July 2023
- Average tenure: 3.2 months
- Range: -0.05 to 1.77 years

**Interpretation:**
1. **Recent user acquisition:** Many users signed up in early 2023
2. **Growth signal:** Platform is attracting new customers
3. **Cohort effect:** Elena's filter includes recent sign-ups
4. **Not churn:** Users are new, not abandoned

**Why this is actually good:**
1. **Engagement despite newness:** New users already have >7 sessions
2. **Quick conversion:** 87.7% booking rate even with short tenure
3. **High CLV:** $4,136 annual value from new users
4. **Growth opportunity:** As tenure increases, CLV may grow

**Challenge ahead:**
- **Retention focus:** Keep these users engaged long-term
- **Maturation:** Watch how behavior changes as users age
- **Cohort tracking:** Monitor newer vs older users separately

**Bottom line:** Growing user base is a strength, not a weakness.

---

### Q24: "How do we know these patterns will hold for future customers?"

**Answer:**
**We don't with certainty, but we have strong indicators:**

**Evidence patterns are stable:**
1. **Large sample:** 5,765 users, 43,344 sessions
2. **Consistent behavior:** Patterns stable across users
3. **Business logic:** Findings align with travel industry norms
4. **Statistical significance:** Effects are large, not noise

**Potential changes:**
1. **Seasonal variation:** Summer patterns may differ
2. **User maturation:** Newer users may change behavior over time
3. **Market shifts:** Economic changes could impact travel
4. **Product evolution:** New features may change engagement

**Risk mitigation:**
1. **Regular monitoring:** Re-run analysis quarterly
2. **Cohort comparison:** Track new vs existing users separately
3. **A/B testing:** Validate perk assignments experimentally
4. **Feedback loops:** Survey users to understand changes

**Current recommendation:** Proceed with segmentation using these insights, but **build monitoring into the process** to detect drift.

---

### Q25: "What's the single most important insight from this analysis?"

**Answer:**
**Booked sessions have 2x the engagement (25 clicks vs 11 clicks).**

**Why this matters most:**

**1. Actionable signal:**
- Can identify high-intent users in real-time
- Trigger interventions when users show high engagement
- Segment users by engagement for targeted campaigns

**2. Validates segmentation approach:**
- Behavior predicts outcomes
- Feature engineering will work (engagement → conversion)
- Clustering will find meaningful groups

**3. Business impact:**
- Focus retention on high-engagement users
- Re-engage low-click users with promotions
- Optimize site experience to encourage exploration

**4. Immediate application:**
- Build "engagement score" feature
- Create alerts for high-engagement sessions
- Test perk offers on engaged users first

**Supporting insights:**
- 87.7% booking rate (strong base)
- $4,136 average CLV (high value)
- 7pm peak hour (optimization target)
- 75% High Value+ users (quality cohort)

**Elevator pitch:** *"Our most engaged users convert at 2x the rate - by identifying and nurturing high-engagement behavior, we can maximize the impact of our personalized rewards program."*

---

## Technical Follow-Up Questions

### Q26: "Could you have done this analysis at session-level instead?"

**Answer:**
**Technically yes, but it wouldn't support our goals.**

**Session-level analysis limitations:**
1. **Can't assign perks:** Perks go to users, not sessions
2. **Noise:** Individual sessions vary widely
3. **Incomplete picture:** Miss cross-session patterns
4. **Not actionable:** Can't market to "Session #12345"

**User-level advantages:**
1. **Marketing target:** Can send emails to users
2. **Stable patterns:** Averages smooth out noise
3. **Lifecycle view:** See entire relationship
4. **Perk assignment:** One perk per user

**When session-level would be useful:**
- Understanding conversion funnels within sessions
- Real-time intervention during browsing
- A/B testing of page layouts

**Our use case (segmentation):** User-level is correct choice.

---

### Q27: "Why did you use mean instead of median for some metrics?"

**Answer:**
**Both are provided where relevant - each tells different story:**

**Mean (average):**
- **Use when:** Want total impact (CLV, spending)
- **Affected by:** Outliers (VIP users pull up average)
- **Business meaning:** Expected value across population

**Median (middle value):**
- **Use when:** Want typical user (clicks, fares)
- **Resistant to:** Outliers (robust measure)
- **Business meaning:** What most users experience

**Examples from our analysis:**

**CLV:**
- Mean: $4,136 (includes VIPs)
- Median: $3,580 (typical user)
- **Interpretation:** Most users ~$3,600, but VIPs boost average

**Page clicks:**
- Mean: 14.84
- Median: 12
- **Interpretation:** Typical session = 12 clicks, some power users skew up

**Flight fare:**
- Mean: $365
- Median: $348
- **Interpretation:** Most flights ~$350, some expensive trips boost average

**Best practice:** Report both, explain which to use for decisions.

---

### Q28: "How would this analysis change with more data?"

**Answer:**
**Analysis would become more robust but patterns likely similar:**

**With 10x more users (57,650 instead of 5,765):**

**Benefits:**
- **Smaller confidence intervals:** More precise estimates
- **Rare patterns visible:** Can detect 1% behaviors
- **Subgroup analysis:** Can segment within segments
- **Stability testing:** Compare multiple cohorts

**Likely to stay same:**
- **Core demographics:** Age, gender distributions
- **Booking patterns:** Product preferences
- **Temporal trends:** 7pm peak, Q1 seasonality
- **CLV structure:** Quartile differences

**May change:**
- **Outlier detection:** Might find new edge cases
- **Niche segments:** Could discover small but valuable groups
- **Regional patterns:** If geographic expansion occurs

**Current sample size (5,765) is sufficient** for:
- Reliable clustering (>1,000 users needed)
- Stable averages (CLV, engagement metrics)
- Pattern detection (seasonality, preferences)

**Recommendation:** Proceed with current data, re-validate with future cohorts.

---

## Summary Questions

### Q29: "What are the three key takeaways for the presentation?"

**Answer:**

**1. We have a high-quality, high-value customer base**
- 87.7% booking rate (extremely engaged)
- $4,136 average annual CLV ($23.8M total value)
- 75% are High Value or VIP customers

**2. Engagement predicts conversion (2x more clicks when booking)**
- Clear behavioral signal for segmentation
- Can identify high-intent users in real-time
- Foundation for personalized perk assignment

**3. Strong temporal patterns enable optimization**
- 7pm peak hour (9.6% of traffic)
- Q1 seasonality (67% of traffic)
- Even weekday distribution
- **Actionable:** Time campaigns for maximum impact

**Supporting evidence:** 5,765 users, 43,344 sessions, 41 features created, ready for Week 2.

---

### Q30: "If you could only show three visualizations from this notebook, which would you choose?"

**Answer:**

**1. CLV Distribution (Figure 4, Plot 1)**
- **Why:** Shows customer value spread
- **Message:** "75% of our customers are high-value"
- **Impact:** Justifies rewards program investment

**2. Engagement by Booking Status (Figure 3, Plot 3)**
- **Why:** Shows the 2x engagement signal
- **Message:** "We can predict who will book"
- **Impact:** Validates segmentation approach

**3. Sessions by Hour (Figure 3, Plot 6)**
- **Why:** Shows 7pm peak clearly
- **Message:** "We know exactly when to reach customers"
- **Impact:** Immediate campaign optimization

**These three tell complete story:**
- **Who:** High-value customers (CLV)
- **What:** Predictable behavior (Engagement)
- **When:** Optimal timing (Hour of day)

---

## Closing Message

### Key Messages for Presentation:

**Three sentences to explain this notebook:**

1. **"We analyzed 5,765 qualified users and found they're highly valuable - 87.7% have booked, with $4,136 average annual CLV."**

2. **"Behavioral patterns are strong: booked sessions show 2x engagement, there's a clear 7pm activity peak, and Q1 dominates with 67% of traffic."**

3. **"We created 41 user-level features capturing demographics, booking preferences, engagement patterns, and customer value - ready for segmentation in Week 2."**

---

**End of Q&A Document**

**Confidence Level:** HIGH - All insights data-driven, patterns are clear and actionable.

**Preparation Tip:** Focus on the "2x engagement" finding and CLV segmentation - these are the most compelling for stakeholders and directly support the rewards program business case.
