# TravelTide Customer Segmentation
## Slide Content for 5-Minute Presentation

**Presenter:** Alberto Diaz Durana  
**Audience:** Elena, Head of Marketing  
**Duration:** 5 minutes  
**Format:** 6 slides, minimal content, visual focus

---

## SLIDE 1: Introduction
**Duration:** 0.5 minutes  
**Visual:** TravelTide logo + project title

### Title
**TravelTide Rewards Program**  
Customer Segmentation & Perk Assignment

### Content (3 bullets max)
- **Goal:** Assign 5,765 active customers to personalized perks
- **Approach:** Data-driven segmentation using behavioral patterns
- **Outcome:** Three customer segments with balanced perk distribution

### Speaker Notes
"Good morning Elena. Today I'm presenting our customer segmentation analysis for the TravelTide rewards program. We analyzed 5,765 active customers to assign each one to their optimal perk based on booking behavior. The analysis identified three distinct customer segments and provides high-confidence recommendations for all five proposed perks."

---

## SLIDE 2: Data & Methodology
**Duration:** 1 minute  
**Visual:** Cohort funnel chart (from Notebook 01)

### Title
**From 5.4M Sessions to 5,765 Qualified Customers**

### Content (4 bullets)
- **Starting Point:** 5.4 million sessions, 47,300 unique users
- **Filtering Applied:** Active users (7+ sessions), valid age range (18-100), quality checks
- **Final Cohort:** 5,765 qualified customers ready for rewards program
- **Features Analyzed:** 65 behavioral metrics including booking patterns, spending, engagement

### Visual Element
INSERT: Cohort funnel visualization (eda_cohort_funnel.png)

### Speaker Notes
"We started with 5.4 million sessions and applied rigorous filters to identify customers most likely to engage with a rewards program. After filtering for activity level, data quality, and valid demographics, we established a qualified cohort of 5,765 users. We then engineered 65 behavioral features capturing their booking patterns, spending habits, and platform engagement. This forms the foundation for segmentation."

---

## SLIDE 3: Premium Paula - Our Core High-Value Segment
**Duration:** 1.5 minutes  
**Visual:** Segment profile chart + persona illustration

### Title
**Cluster 0: Premium Paula (79.7% of customers, 98% of revenue)**

### Content (5 bullets)
- **Size:** 4,596 customers representing our largest segment
- **Value:** $4,985 average CLV - drives $22.9M total (98% of revenue)
- **Behavior:** Frequent hotel bookings, premium spending, strong loyalty
- **Perks Assigned:** Diverse preferences - Hotel Night (28%), Hotel Meal (26%), Free Bag (24%)
- **Strategy:** Priority retention focus - cannot afford to lose these customers

### Visual Element
INSERT: Cluster comparison chart (from clustering_segmentation_dashboard.png - top left panel)

### Speaker Notes
"Premium Paula represents 79.7% of our customer base and is absolutely critical to our business - this segment drives 98% of our total customer lifetime value, representing $22.9 million. These are frequent travelers who book premium hotels and demonstrate strong loyalty once engaged. Despite being one cluster, their perk preferences are actually quite diverse - 28% prefer Free Hotel Night, 26% prefer Hotel Meal, and 24% prefer Free Bag. This shows individual propensities matter more than cluster membership alone. Our recommendation is to allocate 70-75% of marketing budget to retaining this segment."

---

## SLIDE 4: Dining David & Flexible Fiona - Growth Opportunities
**Duration:** 1.5 minutes  
**Visual:** Two-panel comparison chart

### Title
**Clusters 1 & 2: Mid-Value & Budget Segments**

### Left Panel: Dining David (Cluster 1)
- **Size:** 287 customers (5.0%)
- **Value:** $768 average CLV
- **Focus:** Experiential travelers, values dining
- **Top Perk:** Free Hotel Meal (highest propensity)

### Right Panel: Flexible Fiona (Cluster 2)
- **Size:** 882 customers (15.3%)
- **Value:** $319 average CLV
- **Focus:** Budget-conscious, values flexibility
- **Top Perk:** No Cancellation Fee

### Visual Element
INSERT: Side-by-side cluster profiles (normalized comparison from clustering_segmentation_dashboard.png - bottom left panel)

### Speaker Notes
"Our two smaller segments represent growth opportunities. Dining David is our mid-value experiential traveler - 287 customers averaging $768 in lifetime value. They prioritize dining experiences and show the strongest propensity for Free Hotel Meal across all segments. Flexible Fiona is our budget-conscious segment - 882 customers averaging $319 CLV. They value flexibility over premium perks and show strong preference for No Cancellation Fee. Together these segments represent 20% of our customer base and warrant 25-30% of marketing investment focused on conversion and value growth."

---

## SLIDE 5: Key Finding - Balanced Perk Distribution
**Duration:** 0.5 minutes  
**Visual:** Horizontal bar chart showing perk distribution

### Title
**All Five Perks Are Viable - No Single Perk Dominates**

### Content (3 bullets + chart)
- **Balanced Distribution:** Despite 79.7% cluster concentration, perks range from 13.8% to 24.3%
- **Why?** Individual propensities within clusters are more diverse than cluster averages
- **Result:** All five perks have meaningful user bases worthy of marketing investment

### Perk Distribution Chart
```
Free Checked Bag        ████████████████████████ 24.3% (1,402 users)
Free Hotel Meal         ███████████████████████  23.4% (1,349 users)
One Night Free Hotel    ██████████████████████   22.2% (1,277 users)
Exclusive Discounts     ████████████████         16.4% (944 users)
No Cancellation Fee     █████████████            13.8% (793 users)
```

### Visual Element
INSERT: Perk distribution bar chart (from clustering_segmentation_dashboard.png - top right panel)

### Speaker Notes
"Here's our most important finding: despite having 79.7% of customers in one cluster, perk assignments are remarkably balanced. All five perks range from 13.8% to 24.3% of users. This happened because individual preferences within clusters are more nuanced than cluster averages suggested. A Premium Paula customer might prefer Free Bag, Hotel Meal, or Hotel Night depending on their specific booking patterns. The bottom line: all five proposed perks are viable and should be deployed. No perk should be eliminated from the rewards suite."

---

## SLIDE 6: Recommendations & Next Steps
**Duration:** 0.5 minutes  
**Visual:** Implementation roadmap or key metrics dashboard

### Title
**Ready for Launch - High Confidence, Low Risk**

### Content (5 bullets)
- **Implementation Confidence:** 97.2% of assignments rated HIGH or MEDIUM confidence
- **Phased Rollout:** Start with 3,658 HIGH confidence users (63.5%), expand systematically
- **Priority Investment:** 70-75% budget to Premium Paula retention
- **Expected Impact:** 15-20% churn reduction, 15% booking frequency increase
- **Monitoring:** Quarterly segmentation review to track behavior changes

### Visual Element
INSERT: Confidence distribution chart (from clustering_segmentation_dashboard.png - bottom right panel)

### Speaker Notes
"We're ready to implement with high confidence and low risk. 97.2% of our assignments have HIGH or MEDIUM confidence ratings, meaning we have strong data support for these perk matches. I recommend a phased rollout starting with our 3,658 HIGH confidence users, followed by systematic expansion. Prioritize 70-75% of marketing budget to Premium Paula retention - they're our competitive moat. Expected business impact includes 15-20% churn reduction among high-value customers and 15% increase in booking frequency. We'll monitor with quarterly segmentation reviews to ensure the model stays current as customer behavior evolves. Thank you - happy to answer questions."

---

## TIMING BREAKDOWN

| Slide | Duration | Cumulative | Focus |
|-------|----------|------------|-------|
| 1. Introduction | 0:30 | 0:30 | Set context |
| 2. Methodology | 1:00 | 1:30 | Establish credibility |
| 3. Premium Paula | 1:30 | 3:00 | Highlight priority segment |
| 4. David & Fiona | 1:30 | 4:30 | Complete the picture |
| 5. Key Finding | 0:30 | 5:00 | Deliver insight |
| 6. Next Steps | 0:30 | 5:30 | Call to action |

**Buffer:** 30 seconds for Q&A transition

---

## VISUAL ASSETS NEEDED

### Required Images (from your project)
1. **Slide 2:** `eda_cohort_funnel.png` (Notebook 01)
2. **Slide 3:** `clustering_segmentation_dashboard.png` - Cluster size panel
3. **Slide 4:** `clustering_segmentation_dashboard.png` - Profile comparison panel
4. **Slide 5:** `clustering_segmentation_dashboard.png` - Perk distribution panel
5. **Slide 6:** `clustering_segmentation_dashboard.png` - Confidence distribution panel

### Optional Enhancements
- TravelTide logo (Slide 1)
- Persona illustrations for Paula, David, Fiona (Slides 3-4)
- Icons for each perk type (Slide 5)

---

## DESIGN GUIDELINES

### Typography
- **Headers:** Large, bold, sentence case
- **Body:** 18-24pt, maximum 6 bullets per slide
- **Emphasis:** Bold for numbers, italics for insights

### Color Palette
- **Primary:** Professional blue (trust, reliability)
- **Accent:** Warm orange/coral (engagement, energy)
- **Data:** Multi-color for segments (distinct but harmonious)
- **Background:** Clean white or light gray

### Layout Principles
- **One idea per slide:** Single clear message
- **Visual hierarchy:** Title → Chart → 3-5 bullets
- **White space:** Don't overcrowd - let content breathe
- **Consistency:** Same layout structure across slides

---

## DELIVERY TIPS

### Pacing
- **Speak slowly:** You have 5 minutes, don't rush
- **Pause after key insights:** Let numbers sink in
- **Transition smoothly:** "Moving to our next segment..."

### Emphasis Points
1. **Slide 3:** "98% of revenue" - pause for impact
2. **Slide 5:** "All five perks are viable" - key finding
3. **Slide 6:** "97.2% high confidence" - low risk message

### Body Language (for recording)
- **Camera on:** Professional but friendly
- **Eye contact:** Look at camera, not screen
- **Hand gestures:** Natural, not excessive
- **Screen share:** Ensure slides fill frame clearly

---

## PRESENTATION CHECKLIST

### Before Recording
- [ ] Test screen share + camera setup
- [ ] Practice full run-through (time yourself)
- [ ] Check all visualizations display correctly
- [ ] Prepare backup slides (PDF export)
- [ ] Close unnecessary applications
- [ ] Turn off notifications

### During Recording
- [ ] Start with name and project title
- [ ] Maintain steady pace (not too fast)
- [ ] Point to specific chart elements when referencing
- [ ] End with clear call to action
- [ ] Leave 5-10 seconds silence at end (editing buffer)

### After Recording
- [ ] Review for timing (under 5:30?)
- [ ] Check audio quality (clear, no background noise?)
- [ ] Verify all slides visible and readable
- [ ] Export as MP4 (H.264 codec for compatibility)

---

END OF SLIDE CONTENT
