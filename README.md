# User Journey Funnel Analysis (Power BI)

An interactive Power BI dashboard that tracks how users move through an e-commerce purchase journey (Visit → Product View → Add to Cart → Checkout → Purchase), shows where they drop off, and compares performance by device and marketing channel.

> **AI assistance disclosure:** The written insights and recommendations in this README were drafted with AI assistance (Claude) and checked against the dashboard figures. The dashboard was built by me in Power BI Desktop.

## Project Goal
Find out where users leave the purchase funnel and which devices and channels convert best, so the business knows where to focus its improvement effort.

## Data
- **Events** table: 21,180 event records from 10,000 unique users (columns: event_id, user_id, session_id, event_name, event_time, device, channel).
- **Stages** table: the five funnel stages with a StageOrder column (1–5).
- Period covered: September 2026.

## Tools and Method
- Power BI Desktop and Power Query (loaded both tables, set data types, trimmed stage names)
- Data model: one-to-many relationship from `Stages[StageName]` to `Events[event_name]`; stages sorted by `StageOrder` so the funnel displays in the correct order
- DAX measures: `Users at Stage` (DISTINCTCOUNT of user_id), `Step Conversion %`, `Overall Conversion %`, `Drop-off Users`, `Drop-off %`, `Funnel Conversion Rate`, `Cart Abandonment %`, `Avg Hours to Purchase`
- Visuals: KPI cards, funnel chart, funnel table, drop-off bar chart, device and channel matrices, slicers for channel, device and date

## Key Metrics
| Metric | Value |
|---|---|
| Total visitors | 10,000 |
| Total purchasers | 780 |
| Overall funnel conversion rate | 7.8% |
| Cart abandonment (Add to Cart → Checkout) | 50% |
| Average time from first visit to purchase | 2.95 hours |

| Stage | Users | Step conversion | Overall conversion |
|---|---|---|---|
| Visit | 10,000 | 100% | 100% |
| Product View | 6,500 | 65% | 65% |
| Add to Cart | 2,600 | 40% | 26% |
| Checkout | 1,300 | 50% | 13% |
| Purchase | 780 | 60% | 7.8% |

## Key Insights
1. **The biggest drop-off is between Product View and Add to Cart.** 3,900 users (60% of those who viewed a product) leave at this step, the largest single loss in the funnel. Only 40% go on to add an item to the cart.
2. **Half of users who add to cart do not reach checkout.** Cart abandonment is 50% (1,300 of 2,600 users), and a further 520 users (40%) leave at checkout before paying.
3. **Mobile is the weakest device despite being the largest.** Mobile brings 59.6% of all visitors (5,961) but converts at only 4.8%, compared with 13.4% on desktop and 7.7% on tablet.
4. **Channel quality varies sharply.** Email converts best at 21.5%, followed by Organic Search at 9.3%, Paid Ads at 6.4% and Social Media at 2.1%. Email supplies only 9.9% of visitors but 27.3% of purchases.
5. **Paid Ads and Social Media bring over half the traffic but few buyers.** Together they account for 55% of visitors (5,536) but only 31% of purchases (244 of 780).
6. **Buyers decide quickly.** The average time from first visit to purchase is about 3 hours, so users who intend to buy do so within the same session or day.

## Recommendations
1. **Improve the Product View → Add to Cart step.** Test clearer prices, product images and reviews on product pages, and a more visible Add to Cart button. Measure the step conversion rate (currently 40%) before and after.
2. **Reduce cart abandonment.** Show total cost, including shipping, earlier, add guest checkout, and send a reminder email to users who leave with items in the cart.
3. **Fix the mobile experience.** Review page speed, button size and the checkout form on mobile, and run an A/B test on a simplified mobile checkout. Mobile's 4.8% conversion is the biggest opportunity because it carries most of the traffic.
4. **Shift effort toward high-converting channels.** Grow email (sign-up incentives, newsletters) and review the Social Media targeting and landing pages, since its 2.1% conversion makes it the least efficient channel for sales.
5. **Use follow-up within a few hours.** Because buyers purchase within about 3 hours on average, send cart reminders in the first few hours rather than days later.

*Note: the dashboard shows what is happening, not why. The reasons behind each drop-off above are hypotheses that need testing (for example, through A/B tests or user research).*


## Files
- `Funnel_Analysis.pbix` – Power BI report
- `funnel_analysis.png` – dashboard screenshot
- Raw data (Excel) – source file
