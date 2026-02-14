# Sentinel Mode — Anti-Churn Feature Brief

**Date**: February 14, 2026  
**Purpose**: Product feature to reduce churn during contractor busy cycles  
**Target Dev Time**: ~2 hours (per Gemini market research)  
**Priority**: High (addresses primary churn risk identified in market research)  
**Status**: **READY FOR JEFF'S REVIEW — AWAITING AARON'S DECISION ON TIMING**

---

## The Problem

Dirt contractors and excavators have a 9-month busy cycle. When they land a project, they're heads-down for 9-12 months and don't care about finding new leads. If Agenda Insider is positioned as "find your next job," it becomes a snack, not a subscription — they cancel after Month 1.

**Aaron's direct feedback**: A dirt contractor told him he'd sign up for a single month about twice every 18 months.

**Impact**: High churn rate during peak construction season (spring/summer) destroys MRR.

---

## The Solution: Sentinel Mode

Reframe Agenda Insider from "hunting tool" to "market radar." Even when contractors are busy, they care about:
- Competitor rezonings near their active site
- City council decisions that could affect their current project
- Drainage changes, utility work, or road closures near their job
- New developments that could change site access or logistics

**Sentinel Mode** keeps the product valuable during busy periods by monitoring the user's active project site and alerting them to anything within a defined radius (default: 5 miles) that could impact their work.

---

## User Stories

### Story 1: Busy Excavator
**As** an excavation contractor locked in on a 12-month project,  
**I want** to know if a competitor gets a rezoning approved on the lot next to my current site,  
**So that** I can protect my territory and spot change order opportunities.

### Story 2: GC Monitoring Multiple Sites
**As** a general contractor managing 3 active projects,  
**I want** to monitor all 3 sites simultaneously for city council surprises,  
**So that** I'm not blindsided by drainage changes, road closures, or zoning amendments that affect my work.

### Story 3: Developer Tracking Competition
**As** a developer with land holdings in Utah County,  
**I want** to see every rezoning and annexation within 2 miles of my parcels,  
**So that** I know what competitors are building nearby before it's public knowledge.

---

## Feature Spec

### Core Functionality

1. **Project Watch Input**
   - User inputs one or more active project addresses (or selects from Map view)
   - User sets radius (default: 5 miles, options: 2/5/10 miles)
   - User sets alert frequency (real-time, daily digest, weekly digest)

2. **Background Monitoring**
   - System monitors all planning commission agendas, city council meetings, and design review committee notes
   - Filters for any activity within the user's defined radius around their active site(s)
   - Triggers alert when match is found

3. **Alert Content**
   - Subject: "Sentinel Mode Alert: Activity Near [Your Project Address]"
   - Body: Project name, address, type, planning stage, distance from user's site, link to agenda document
   - Map preview showing user's site + new project pin

4. **Dashboard UI**
   - "Sentinel Mode" tab in user dashboard
   - Shows active watch sites, radius, last alert date
   - Toggle on/off per site
   - Quick actions: "Add Site," "Edit Radius," "Pause Alerts"

---

## UX Flow

### Setup Flow
1. User clicks "Enable Sentinel Mode" from dashboard
2. Modal: "Enter your current project address"
3. User inputs address (autocomplete from Map view data)
4. Modal: "How far should we monitor?" → Select radius (2/5/10 miles)
5. Modal: "How often do you want alerts?" → Select frequency (real-time/daily/weekly)
6. Confirmation: "Sentinel Mode active. We're watching a 5-mile radius around [Address]."

### Alert Flow
1. New project appears in planning commission agenda within user's radius
2. System generates alert email
3. Email subject: "Sentinel Mode Alert: New Project 2.3 Miles from Your Site"
4. Email body:
   - "We detected new activity near your project at [User's Address]"
   - Project details: Name, address, type, stage, distance
   - Map preview image
   - CTA: "View on Map" (link to agendainsider.com/map with both pins visible)

---

## Technical Requirements

### Backend

1. **Database Schema**
   - New table: `sentinel_watches`
     - `user_id` (foreign key to users)
     - `watch_address` (geocoded lat/long)
     - `radius_miles` (integer: 2, 5, or 10)
     - `alert_frequency` (enum: real-time, daily, weekly)
     - `active` (boolean)
     - `created_at`, `updated_at`

2. **Alert Logic**
   - When new project is scraped, calculate distance from all active `sentinel_watches`
   - If distance < radius_miles, generate alert
   - Batch alerts by frequency (real-time = immediate, daily = 8 AM MT, weekly = Monday 8 AM MT)

3. **Email Template**
   - Extend existing alert email template with "Sentinel Mode" variant
   - Include: user's watch address, new project details, distance, map preview

### Frontend

1. **Dashboard Tab**
   - New "Sentinel Mode" navigation item
   - List view of active watches (address, radius, status)
   - "Add Watch" button → modal flow

2. **Map View Integration**
   - Right-click on any project pin → "Watch This Area"
   - Populates address into Sentinel Mode setup flow

3. **Onboarding**
   - During initial signup, after user completes first search:
     - "You're likely working on a project right now. Want us to monitor the area around it while you're busy? Enable Sentinel Mode."
   - Day 20 of trial (automated email):
     - "You're probably hitting the dirt now. We've switched your account to Sentinel Mode. We'll monitor your site while you're in the cab."

---

## Success Metrics

### Primary Metric: Churn Reduction
- **Current churn assumption**: 2% monthly = 24% annually (industry standard)
- **Target churn with Sentinel Mode**: 1% monthly = 12% annually (50% churn reduction)
- **Measure**: Churn rate of users with Sentinel Mode enabled vs. users without

### Secondary Metrics
- **Adoption rate**: % of paid subscribers who enable Sentinel Mode within 30 days
- **Engagement**: # of Sentinel Mode alerts sent per user per month
- **Retention**: Users with Sentinel Mode enabled have longer LTV (lifetime value)

### Qualitative Feedback
- Survey question after 60 days: "How valuable is Sentinel Mode in keeping you subscribed even when you're busy?" (1-10 scale)

---

## Messaging Integration

### For Pilot Campaign (Track B: Defense/Sentinel)

Email subject: "Quick question"

Email body:
> [First Name],
> 
> Quick question: do you know which competitor just got a rezoning approved on the lot next to your current project?
> 
> You're locked in for the next year. Agenda Insider monitors the 5-mile radius around your active site for competitor activity, drainage changes, and city council surprises that could affect your job.
> 
> Free trial: [link]
> 
> $100/month. Radar on the dash.
> 
> Jack  
> Agenda Insider

### For Landing Page

Feature card:
> **🛡️ Sentinel Mode**  
> Monitor your active site's 5-mile radius for competitor rezonings, city council surprises, and drainage changes. Your radar on the dash while you're in the cab.

---

## Implementation Phases

### Phase 1 (MVP — 2 hours dev time)
- Single watch site per user
- Fixed 5-mile radius
- Daily digest alerts only
- Email-only (no dashboard UI)
- Manual address input (no Map view integration)

**Deploy this first.** Validate the concept before building full UI.

### Phase 2 (Full Feature — +4 hours dev time)
- Multiple watch sites per user
- User-selectable radius (2/5/10 miles)
- Real-time, daily, and weekly alert options
- Dashboard UI (list view, add/edit/delete watches)
- Map view integration (right-click to add watch)

### Phase 3 (Advanced — +6 hours dev time)
- Mobile push notifications (requires mobile app or PWA)
- SMS alerts (requires Twilio integration)
- Auto-detection of user's active site from CRM integrations (if they use Procore, CoConstruct, etc.)
- "Competitive Intel" dashboard showing all competitor activity in watched areas

---

## Cost/Benefit Analysis

### Development Cost
- Phase 1 (MVP): 2 hours × $150/hour (Jeff's time) = $300
- Phase 2 (Full): +4 hours = $600 additional
- Phase 3 (Advanced): +6 hours = $900 additional
- **Total**: $1,800 for complete feature

### Revenue Impact
- **Churn reduction**: 50% churn reduction = 12% more retained subscribers annually
- At 100 subscribers, 12% churn reduction = 12 additional retained subscribers × $100/month = **$1,200/month retained MRR** = **$14,400/year**
- At 500 subscribers, 50% churn reduction = 60 additional retained subscribers × $100/month = **$6,000/month retained MRR** = **$72,000/year**

**ROI at 100 subscribers**: $14,400 retained revenue / $1,800 dev cost = **8x ROI in Year 1**

**ROI at 500 subscribers**: $72,000 retained revenue / $1,800 dev cost = **40x ROI in Year 1**

---

## Risks and Mitigation

### Risk 1: Alert Fatigue
**Risk**: Users get too many alerts and unsubscribe.  
**Mitigation**: Default to daily digest (not real-time). Allow users to set radius and frequency.

### Risk 2: Low Adoption
**Risk**: Users don't understand or enable Sentinel Mode.  
**Mitigation**: Onboarding flow auto-suggests it. Day 20 email positions it as "we've switched you to Sentinel Mode while you're busy."

### Risk 3: Technical Complexity
**Risk**: Geocoding + distance calculation at scale is slow.  
**Mitigation**: Pre-compute distances when projects are scraped (not when alerts are sent). Cache results.

---

## Next Steps

1. **Aaron decides timing**: When to brief Jeff on this feature? (Immediate priority or wait until after pilot launch?)
2. **Jeff reviews brief**: Technical feasibility check, dev time estimate validation
3. **Phase 1 MVP deployment**: 2-hour build, deploy to beta users first, validate concept
4. **Measure impact**: Track churn rate of Sentinel Mode users vs. non-users over 60 days
5. **Phase 2 rollout**: If Phase 1 reduces churn, build full dashboard UI

---

## Jack's Recommendation

**Deploy Phase 1 MVP immediately after pilot launch (late February).** The 9-month busy cycle is the biggest churn risk we face. Sentinel Mode directly addresses it. Two hours of dev time to potentially cut churn in half is the highest ROI feature we could build right now.

**Test messaging in pilot**: Track B (Defense/Sentinel) emails will validate whether this positioning resonates with excavators and GCs. If Track B outperforms Track A in conversions, it's a green light for Sentinel Mode.

---

**Status**: Brief complete. Saved to repo. Awaiting Aaron's decision on when to present to Jeff.
