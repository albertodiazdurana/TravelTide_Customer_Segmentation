# TravelTide Customer Segmentation
## Executive Summary

**Project Lead:** Alberto Diaz Durana  
**Date:** October 29, 2025  
**For:** Elena, Head of Marketing

---

## Background

TravelTide seeks to launch a personalized rewards program by assigning 5,765 active customers to one of five perks based on their behavioral preferences. This analysis identifies natural customer segments and matches each user to their optimal reward.

## Objectives

- Segment customers into behavioral groups using clustering analysis
- Assign each customer to their best-fit perk based on data-driven propensity scores
- Provide actionable recommendations for marketing implementation

## Methodology

We analyzed customer behavior across 65 features including booking patterns, engagement metrics, and spending habits. Hierarchical clustering identified 3 distinct customer segments. Individual perk assignments were made using propensity scores calculated from historical behavior, resulting in confidence-rated recommendations for all 5,765 users.

## Key Findings

### Three Clear Customer Segments Emerged

**Premium Paula (79.7% - 4,596 users)**
- High-value hotel travelers driving 98% of customer lifetime value
- Average CLV: $4,985
- Prefers: Hotel Night and related premium perks

**Dining David (5.0% - 287 users)**  
- Mid-value travelers who prioritize dining experiences
- Average CLV: $768
- Prefers: Hotel Meal benefits

**Flexible Fiona (15.3% - 882 users)**
- Budget-conscious travelers valuing flexibility
- Average CLV: $319  
- Prefers: No Cancellation Fee and basic benefits

### Balanced Perk Distribution Across All Five Rewards

```
Free Bag:            24.3% (1,402 users)
Hotel Meal:          23.4% (1,349 users)
Hotel Night:         22.2% (1,277 users)
Exclusive Discount:  16.4% (944 users)
No Cancel Fee:       13.8% (793 users)
```

**Critical Insight:** All 5 perks have meaningful user bases. Initial concerns about 70%+ concentration in one perk did not materialize. Individual preferences within segments are more diverse than cluster averages suggested.

### High Assignment Confidence

- **63.5%** of assignments are HIGH confidence (strong, clear preferences)
- **33.8%** are MEDIUM confidence (reliable preferences)
- **2.8%** are LOW confidence (require A/B testing)

This confidence distribution enables phased rollout with minimal implementation risk.

## Recommendations

### Immediate Actions (Week 1-2)
1. **Implement all 5 perks** - Balanced distribution validates the full rewards suite
2. **Prioritize Premium Paula segment** - Allocate 70-75% of marketing budget to retain high-value customers
3. **Launch with HIGH confidence users first** - Roll out to 3,658 users (63.5%) for immediate impact

### Phase 2 (Month 2)
4. **Expand to MEDIUM confidence users** - Add 1,947 users with reliable assignments
5. **Monitor engagement metrics** - Track perk activation rates, booking frequency, satisfaction scores

### Phase 3 (Month 3+)
6. **A/B test LOW confidence users** - Test assignment vs. choice for 160 users
7. **Quarterly monitoring** - Track cluster stability, re-run analysis every 6-12 months

## Business Impact

**Revenue Protection:** Premium Paula segment represents $22.9M in annual CLV - retention focus critical

**Growth Opportunity:** Converting 20% of Flexible Fiona users from $319 to $500 CLV = $160K incremental annual value

**Marketing Efficiency:** Personalized perks expected to increase booking frequency 15%+ and improve customer satisfaction to 4.5+/5

## Next Steps

**This Week:** Present findings to leadership and secure approval for full rewards program launch

**Weeks 1-2:** Campaign design and platform integration

**Week 3:** Pilot launch with HIGH confidence segment (3,658 users)

**Month 2:** Full rollout to all 5,765 users with ongoing optimization

---

**Bottom Line:** Customer segmentation is complete with high confidence. All 5 perks are viable. Ready for immediate implementation with minimal risk and strong expected ROI.

---

**Files Delivered:**
All files available in the GitHub repository ([text](https://github.com/albertodiazdurana/TravelTide_Customer_Segmentation))

*Clustering Results* (`data/results/clustering/`):
- `user_perk_assignments.csv` - Individual perk assignments with confidence scores (5,765 × 8)
- `cluster_profiles_k3.csv` - Segment characteristics and CLV metrics (3 × 10)
- `cluster_assignments_k3.csv` - User-to-cluster mapping (5,765 × 2)
- `perk_distribution.csv` - Summary of perk allocation across all users (5 × 3)

*Presentation Materials* (`docs/reports/`):
- `executive_summary.md` - One-page project summary for stakeholders
- `detailed_report.md` - Three-page detailed project report for stakeholders
- `presentation_personas.md` - Detailed persona profiles for marketing teams
