# Loophire Talent Intelligence Platform

A SaaS platform providing workforce intelligence, market analysis, and compensation benchmarking for insurance agencies (20-400 employees).

## Overview

Loophire Talent Intelligence transforms raw recruitment data into actionable market intelligence for insurance agency leaders. The platform answers the critical question: **"Are we okay, or are we about to screw something up?"**

### Core Philosophy

- **Judgment over metrics** — Don't just show data, interpret it
- **Implications over information** — Tell leaders what the data means for their business
- **Directive over informative** — Recommend actions, not just observations
- **Confidence scoring** — Be transparent about data quality (Verified/Calibrated/Estimated)

---

## Platform Components

### 1. Market Intelligence Generator (Admin Portal)
`/admin/loophire-crm-bridge.html`

Internal admin tool for Loophire team to generate market intelligence reports.

**Features:**
- CRM data bridge — Pull candidate and job data from Loophire CRM
- Claude Opus 4.5 integration — AI-powered analysis and intelligence generation
- Custom data input — Add external market data via chat interface (LinkedIn Recruiter, Indeed, Sales Nav, competitor intel)
- Multi-market support — Generate intelligence for different geographic markets
- Role-specific analysis — Filter by Commercial Producer, Account Manager, CSR, Underwriter, etc.

**Workflow:**
1. Select Market & Role Type
2. Pull CRM Data (candidates + jobs)
3. Add supplemental market intel via Claude chat
4. Run Opus Analysis
5. Review & Publish to Dashboard

---

### 2. Loophire Intelligence Dashboard (Company-Facing)
`/dashboard/loophire-dashboard.html`

Executive dashboard for insurance agency leaders — designed as a "decision cockpit" not a "tool launcher."

**Key Sections:**

#### Reality Snapshot
- **Dominant Truth Headline** — Single most important insight (e.g., "Your biggest hiring risk this month is underpriced senior roles in Phoenix")
- **Confidence Meter** — Data quality indicator
- **Hire Feasibility** (Primary Risk) — Overall hiring difficulty score
- **Turnover Probability** — Retention risk assessment
- **Comp Competitiveness** — How your pay compares to market

#### Executive Action Card
Specific, prioritized recommendations:
- "Raise Commercial Producer base to $68K or risk losing 2 candidates to competitor offers"
- "Start backfill planning for Account Manager — 67% turnover probability in next 6 months"

#### Roles at Risk Table
| Role | Risk Level | Trigger | Recommended Action |
|------|------------|---------|-------------------|
| Commercial Producer | High | Comp 12% below market | Adjust to $68K base |
| Account Manager | Medium | 2 competitors hiring | Accelerate timeline |

#### Compensation Pressure View
- Interactive slider showing current position vs. market
- Ghost marker showing "+10% impact" threshold
- Split view: Your Comp vs. Market Comp

#### Competitive Hiring Activity
- Competitor job posting tracker with implications
- "ABC Insurance posted 3 producer roles — they're likely expanding or backfilling turnover"

#### Workforce Stability (Retention)
- Risk indicators with operational impact
- Backfill time estimates (e.g., "45-60 day backfill time if lost")

---

### 3. Comp Benchmarking Tool
`/tools/loophire-comp-benchmarking.html`

Standalone compensation analysis tool focused on Commercial Lines Producers.

**Scenarios:**
- **Book Builder** — Producer builds book from scratch (most common due to non-competes)
- **Book Bringer** — Producer brings existing book (rare, requires non-compete expiration)
- **Agency Book Purchase** — Agency acquires book for producer to service

**Key Insight:** Most producers are under 2-year non-competes and cannot bring their book. Agencies should plan for 3-5 year producer ramp times.

**Output:**
- Base salary ranges by experience level
- Commission structures (new business vs. renewal splits)
- Production expectations and timeline to profitability
- Market-specific adjustments

---

## Technical Architecture

### Data Model

```
┌─────────────────────────────────────────────────────────────┐
│                    DATA SOURCES                              │
├─────────────────┬─────────────────┬─────────────────────────┤
│  Loophire CRM   │  External Data  │  Subscriber Data        │
│  - Candidates   │  - LinkedIn     │  - Confirmed salaries   │
│  - Jobs         │  - Indeed       │  - Role structures      │
│  - Placements   │  - Competitor   │  - Growth plans         │
│                 │    intel        │                         │
└────────┬────────┴────────┬────────┴────────┬────────────────┘
         │                 │                 │
         ▼                 ▼                 ▼
┌─────────────────────────────────────────────────────────────┐
│              CLAUDE OPUS 4.5 ANALYSIS                        │
│  - Compensation benchmarking                                 │
│  - Market narrative generation                               │
│  - Risk assessment                                           │
│  - Actionable recommendations                                │
└─────────────────────────┬───────────────────────────────────┘
                          │
                          ▼
┌─────────────────────────────────────────────────────────────┐
│              PUBLISHED INTELLIGENCE                          │
│  - Market-specific dashboards                                │
│  - Role-specific benchmarks                                  │
│  - Confidence-scored insights                                │
└─────────────────────────────────────────────────────────────┘
```

### Confidence Scoring

| Level | Description | Source |
|-------|-------------|--------|
| **Verified** | Direct from placements/confirmed data | Loophire CRM |
| **Calibrated** | Cross-referenced from multiple sources | CRM + External |
| **Estimated** | Projected from limited data | External only |

---

## Data Scaling Strategy

### The Cold Start Problem
When expanding to new markets without placement data, the platform uses a "offer intelligence to collect data" model:

1. **Lead with recruiting** — Intelligence follows successful placements
2. **Subscriber-contributed data** — Agencies confirm salary/comp data during onboarding
3. **External source aggregation** — LinkedIn, Indeed, industry reports
4. **Confidence transparency** — Always show data quality level

### Onboarding Flow
New subscribers complete a questionnaire:
- Confirm salary/total comp for roles (Producer, Account Manager, Underwriter)
- Current headcount and structure
- Growth goals and hiring timeline
- Competitive landscape observations

---

## File Structure

```
loophire-talent-intelligence/
├── README.md
├── admin/
│   └── loophire-crm-bridge.html      # Admin portal - Market Intelligence Generator
├── dashboard/
│   └── loophire-dashboard.html        # Company-facing executive dashboard
└── tools/
    └── loophire-comp-benchmarking.html # Standalone comp benchmarking tool
```

---

## Design System

### Colors
- **Navy** `#1c223c` — Primary background
- **Coral** `#de635e` — Accent, warnings, emphasis
- **Teal** `#2a615e` — Success, positive indicators
- **Beige** `#eee1ce` — Secondary backgrounds
- **Purple** `#7c3aed` — Claude/AI indicators

### Typography
- **DM Sans** — Primary UI font
- **Libre Baskerville** — Headlines, large numbers
- **JetBrains Mono** — Data, code, technical info

### Key UI Principles
- Dark theme for executive dashboard (reduces eye strain, feels premium)
- Card-based layout with clear visual hierarchy
- Judgment-based language ("At Risk" not "Score: 72")
- Always show implications, not just data

---

## Roadmap

### Phase 1 (Current)
- [x] Executive dashboard design
- [x] CRM bridge admin portal
- [x] Comp benchmarking tool
- [x] Claude chat interface for custom data input

### Phase 2 (Planned)
- [ ] Settings page (CRM config, user management)
- [ ] Onboarding questionnaire flow
- [ ] API integration with Loophire CRM
- [ ] Automated intelligence refresh
- [ ] Multi-tenant subscriber access

### Phase 3 (Future)
- [ ] Mobile-responsive dashboard
- [ ] Email alerts and notifications
- [ ] Historical trend analysis
- [ ] Predictive turnover modeling

---

## License

Proprietary — Loophire, Inc.

---

## Contact

- **Website:** [loophire.com](https://loophire.com)
- **GitHub:** [LoophireTechHub](https://github.com/LoophireTechHub)
