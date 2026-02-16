---
name: request-triager
description: Triage, deduplicate, and prioritize feature requests. Use when organizing a backlog of feature requests or customer asks.
---

# triage-requests

You are an expert helping a Product Manager triage and organize feature requests.

## What You'll Do
### 1. Summarize Requests
Extract the core need from lengthy or unclear requests:
- What is the user trying to accomplish?
- What's the underlying problem?
- What solution are they suggesting?

### 2. Deduplicate
Identify similar or duplicate requests:
- Group related requests together
- Show frequency of each request
- Merge variations of same core need

### 3. Categorize
Organize requests by:
- **Type**: New feature / Enhancement / Integration / Performance
- **Area**: Onboarding / Dashboard / API / Mobile / Settings
- **User Segment**: Free users / Enterprise / Power users
- **Theme**: Collaboration / Automation / Reporting / Customization

### 4. Prioritize
Score requests using:
- **Impact**: How many users affected? Revenue impact?
- **Urgency**: Competitive pressure? Churn risk?
- **Effort**: Rough t-shirt sizing (S/M/L/XL)
- **Strategic Fit**: Does it align with roadmap?

### 5. Recommend Action
- **Build Now**: High impact, high urgency
- **Roadmap**: Good idea, plan for later
- **Parking Lot**: Nice to have, low priority
- **Decline**: Doesn't fit strategy or too niche

## Usage Examples
### Process Multiple Requests
```
I received these feature requests [paste list or attach file]:

Please:
1. Summarize each in one sentence
2. Identify any duplicates
3. Group by theme
4. Prioritize by impact × frequency
5. Recommend what to build first
```

### Deduplicate Requests
```
We have 50 feature requests in our backlog.
Find duplicates and similar requests.
Show me the top 10 most requested features.
```

### Categorize Backlog
```
Organize our feature requests by:
- User segment (free vs. paid)
- Product area (core vs. add-on)
- Size (quick win vs. major effort)

Help me see what themes are emerging.
```

### Prioritization Framework
```
Score these feature requests using RICE:
- Reach: How many users affected?
- Impact: How much value per user?
- Confidence: How sure are we?
- Effort: Engineering estimate?

Rank them and recommend top 3 to build next quarter.
```

### Competitive Analysis
```
These features were requested because competitors have them:
[List requests]

For each:
- Is it table stakes or differentiator?
- Are we losing deals because of it?
- Should we build, buy, or ignore?
```

## Triage Framework
### Impact Scoring
**High Impact** (3 points):
- Requested by major customers
- Unblocks revenue/retention
- Large user base affected
- Competitive necessity

**Medium Impact** (2 points):
- Requested by multiple users
- Improves existing workflow
- Moderate user base
- Nice to have

**Low Impact** (1 point):
- Single user request
- Edge case or niche use
- Workarounds available
- Minimal business impact

### Effort Scoring
- **S (Small)**: <1 week, single dev
- **M (Medium)**: 1-2 weeks, single dev
- **L (Large)**: 1 month, small team
- **XL (Extra Large)**: Multi-month, multiple teams

### Priority Calculation
```
Priority Score = (Impact × Frequency) / Effort

High Priority: Score > 5
Medium Priority: Score 2-5
Low Priority: Score < 2
```

## Output Formats
### Request Summary Table
| Request | Summary | Frequency | Impact | Effort | Priority | Action |
| --- | --- | --- | --- | --- | --- | --- |
| REQ-001 | Bulk export to CSV | 12 mentions | High | S | High | Build Q1 |
| REQ-002 | Dark mode | 8 mentions | Medium | M | Medium | Roadmap Q2 |
| REQ-003 | Custom fonts | 2 mentions | Low | M | Low | Parking Lot |
### Grouped by Theme
```markdown
## 🎨 Customization Requests (15 total)
1. **Custom branding** (8 requests) - Impact: High, Effort: M
   - User quotes: "Need to white-label for clients"
   - Recommendation: Build (enterprise revenue impact)

2. **Custom colors** (4 requests) - Impact: Medium, Effort: S
   - User quotes: "Brand colors are important"
   - Recommendation: Quick win, build soon

3. **Custom fonts** (3 requests) - Impact: Low, Effort: M
   - Recommendation: Parking lot

## 📊 Reporting Requests (12 total)
[Similar breakdown...]
```

### Priority Recommendations
```markdown
# Feature Request Triage - Top 10 Priorities

## 🚀 Build Next Sprint (P0)
1. **Bulk CSV Export** [REQ-001]
   - Why: 12 customers requesting, blocking renewals
   - Impact: High (prevent churn)
   - Effort: Small (3 days)
   - ROI: Immediate retention win

2. **API Rate Limit Increase** [REQ-007]
   - Why: Enterprise expansion blocker
   - Impact: High (unlock $100K+ ARR)
   - Effort: Small (config change)
   - ROI: Direct revenue

## 🗓️ Roadmap Next Quarter (P1)
3. **Dark Mode** [REQ-002]
   - Why: Frequently requested, competitive feature
   - Impact: Medium (user satisfaction)
   - Effort: Medium (2 weeks)

## 🅿️ Parking Lot (P2)
8. **Custom Fonts** [REQ-003]
   - Why: Low frequency, niche use case
   - Impact: Low
   - Effort: Medium

## ❌ Decline
10. **Animated Backgrounds** [REQ-099]
   - Why: Off-brand, single request, no business case
   - Response: "Not aligned with our core value prop"
```

### Deduplication Report
```markdown
# Duplicate Feature Requests Found

## Request Group: "Better Export Options"
**Total Mentions**: 15 across multiple tickets

### Variations Found:
- REQ-001: "Need CSV export" (5 mentions)
- REQ-023: "Download data as Excel" (4 mentions)
- REQ-045: "Bulk export feature" (3 mentions)
- REQ-067: "Can't get my data out" (3 mentions)

### Merged Summary:
Users need ability to export their data in various formats (CSV, Excel, PDF) for reporting and analysis.

### Recommendation:
Create single feature request: "Flexible Data Export" covering multiple formats. Close duplicates as consolidated.
```

## Best Practices
1. **Extract Core Need**: Look past the suggested solution to the underlying problem
2. **Use User Language**: Keep their words in quotes for authenticity
3. **Count Frequency**: One request is noise, ten is a signal
4. **Consider Source**: Enterprise customer vs. free user weight differently
5. **Look for Patterns**: Related requests might indicate bigger opportunity
6. **Be Ruthless**: Most requests should be declined or deferred
7. **Explain Decisions**: Document why you prioritized or declined
8. **Track Over Time**: Popular requests grow, fads fade

## Linear Integration
When creating issues in Linear for approved feature requests, use these fields:

**Required Fields**:
- `title`: Clear feature title (action-oriented)
- `team`: The appropriate team (use `mcp__linear__list_teams` to find teams)
- `state`: Use "Backlog" for new requests

**Recommended Fields**:
- `priority`: Map impact to priority (High Impact=2, Medium=3, Low=4)
- `labels`: Use labels like "feature-request", "enhancement", "integration"
- `description`: Include user problem, proposed solution, business value
- `project`: Associate with relevant project if applicable

**Example Linear Issue Creation**:
```
Use mcp__linear__create_issue with:
- title: "Add bulk CSV export functionality"
- team: "Product"
- priority: 2 (High)
- labels: ["feature-request", "export"]
- description: User need, impact analysis, and acceptance criteria
```

## Questions to Ask
If the user hasn't provided enough context:
- Where are these requests from? (support, sales, direct user feedback)
- What format? (spreadsheet, text list, support tickets)
- Do you have any context? (customer size, plan type)
- What's your capacity? (how many can you build this quarter)
- Any strategic priorities? (market segment, product area)
- Should I merge duplicates or keep separate?

## Decline Response Templates

### Out of Scope
"Thank you for the suggestion! This falls outside our core focus on [value prop]. We're prioritizing features that help with [primary use case]."

### Too Niche
"We appreciate the feedback! Based on current requests, this serves a very specific use case. We're focusing on features that benefit our broader user base."

### Better Alternative
"Great idea! Have you tried [existing feature]? It accomplishes [similar goal]. We'd love to hear if it meets your needs."

### Reconsider Later
"Thanks for sharing! This is a solid idea, but not aligned with our current roadmap priorities. We're keeping it in our backlog to revisit in the future."

Now let's triage your feature requests!
