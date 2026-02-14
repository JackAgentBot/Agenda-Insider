# Scout: Nightly Innovation Monitoring System
Date: 2026-02-14  
Status: DESIGNED (Implementation Pending)

## Mission
Scout monitors the internet every night for the latest strategies, tactics, and innovations in:
1. Cold email strategy
2. B2B SaaS subscriber acquisition
3. Construction tech marketing
4. AI-powered sales
5. Landing page optimization

Scout finds the top 3 most relevant pieces of content (YouTube videos, Reddit threads, forum posts), reads/fetches transcripts, and writes one-paragraph summaries with actionable insights.

---

## Implementation Design

### Option A: Cron Job (Isolated Agent)
Since sub-agent spawning is not allowed, Scout runs as a **nightly cron job** in an isolated session.

**Cron Schedule**: 2:00 AM MT daily (before morning briefing at 7 AM MT)  
**Session Target**: `isolated`  
**Model**: `github-copilot/gpt-4o` (free)  
**Wake Mode**: `now`

### Scout Task Prompt
```
Scout's nightly research mission:

1. Use web_search to find the top 3 most relevant pieces of content published in the last 7 days about:
   - Cold email strategy
   - B2B SaaS subscriber acquisition
   - Construction tech marketing
   - AI-powered sales
   - Landing page optimization

2. For each piece of content:
   - If it's a YouTube video, use web_fetch to grab the transcript or description
   - If it's a Reddit thread or forum post, use web_fetch to read the full content
   - If it's a blog post or article, use web_fetch to extract the key points

3. Write a one-paragraph summary for each:
   - What was said
   - What applies to Agenda Insider / BidList
   - What we should consider doing

4. Save the report to jack-learnings/scout-report-YYYY-MM-DD.md

5. Push to GitHub repo (JackAgentBot/Agenda-Insider)

6. Post a summary on Discord:
   "Scout Report - [Date]: Found [#] insights. Top finding: [one sentence]. Full report in GitHub."

Prioritize recent content (last 7 days). Prioritize actionable insights over theory.
```

### Cron Job Definition
```json
{
  "name": "Scout - Nightly Innovation Monitoring",
  "enabled": true,
  "schedule": {
    "kind": "cron",
    "expr": "0 2 * * *",
    "tz": "America/Denver"
  },
  "sessionTarget": "isolated",
  "wakeMode": "now",
  "payload": {
    "kind": "agentTurn",
    "message": "Scout's nightly research mission: [full prompt above]",
    "model": "github-copilot/gpt-4o"
  },
  "delivery": {
    "mode": "announce",
    "channel": "discord"
  }
}
```

---

## Scout Report Format

### Template: `jack-learnings/scout-report-YYYY-MM-DD.md`

```markdown
# Scout Report - [Date]

## 1. [Content Type]: [Title]
**Source**: [URL]  
**Published**: [Date]  
**Relevance**: [Category - e.g., Cold Email Strategy]

**Summary**: [One paragraph: what was said, what applies to us, what we should consider doing]

---

## 2. [Content Type]: [Title]
**Source**: [URL]  
**Published**: [Date]  
**Relevance**: [Category]

**Summary**: [One paragraph]

---

## 3. [Content Type]: [Title]
**Source**: [URL]  
**Published**: [Date]  
**Relevance**: [Category]

**Summary**: [One paragraph]

---

## Top Actionable Insight
[One sentence: the single most valuable thing we should do this week based on these findings]
```

---

## Workflow Integration

1. **Scout runs nightly** at 2:00 AM MT (before morning briefing)
2. **Saves report** to `jack-learnings/scout-report-YYYY-MM-DD.md`
3. **Pushes to GitHub** automatically
4. **Announces on Discord** with one-sentence summary
5. **Jack reviews** Scout's findings and decides what's worth bringing to Aaron in the morning briefing

---

## Why This Matters

### Without Scout:
- We rely on Aaron to send us videos manually
- We miss 99% of what's happening in cold email, B2B SaaS, construction tech
- We react to trends weeks or months after competitors

### With Scout:
- We scan hundreds of sources every night
- We identify actionable tactics within 24 hours of publication
- We stay ahead of competitors by implementing innovations faster
- Jack focuses on execution; Scout handles research

---

## Scout Performance Metrics

Track Scout's effectiveness:

| Metric | Goal | How to Measure |
|--------|------|----------------|
| **Insights Found** | 3 per night | Count findings in daily report |
| **Actionable Insights** | 1 per night | Insights Jack brings to Aaron |
| **Implemented Changes** | 1 per week | Changes made based on Scout findings |
| **Revenue Impact** | Positive ROI | Track conversion rate changes after implementing Scout insights |

---

## First Scout Report (Manual Tonight)

Since Scout cron job isn't set up yet, Jack will manually run the first Scout report tonight to deliver on Aaron's deadline. Future reports will be automated.

**Status**: 🚧 NEXT TASK

---

## Implementation Checklist

- [ ] Create Scout cron job in OpenClaw gateway
- [ ] Test Scout prompt in isolated session
- [ ] Verify Scout can push to GitHub
- [ ] Verify Scout can announce on Discord
- [ ] Run first manual Scout report tonight (2026-02-14)
- [ ] Review Scout report quality with Aaron
- [ ] Automate nightly at 2:00 AM MT

**Target Completion**: 2026-02-14 (tonight)
