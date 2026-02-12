# Instantly.ai Setup - February 12, 2026

**API Key:** `NWU1ZDRjMTgtZmFjYy00OGVhLTgyZWItYTI4MDE5Y2QxMjcwOllabWpabGpGd2NiRw==`  
**Status:** Ready to configure  
**11 Domains Available:** All active at Namecheap, expire Feb 2027

---

## Domain Selection: Starting with 3 (Pilot)

### Recommended First 3 Domains (Priority Order)

**1. tryagendainsider.com** ⭐ TOP PICK
- **Why:** "Try" prefix = freemium/trial association, low-pressure vibe
- **Psychology:** Implies no commitment, testing something new
- **Trust level:** High (common SaaS pattern: "try[product].com")
- **Use case:** Primary cold outreach domain for pilot

**2. getagendainsider.com** ⭐ STRONG SECOND
- **Why:** Action-oriented, implies they're getting something
- **Psychology:** "Get" = value acquisition, positive framing
- **Trust level:** High (common pattern: "get[product].com")
- **Use case:** Re-engagement sequences, follow-ups

**3. useagendainsider.com** ⭐ SOLID THIRD
- **Why:** Usage-focused, practical/functional framing
- **Psychology:** "Use" = tool/utility positioning
- **Trust level:** High (common B2B pattern)
- **Use case:** Executive sequences (higher-authority tone)

---

### Why NOT the Others (For Now):

**Holding for Phase 2 (After pilot success):**
- **agendainsiderapp.com** - Too generic, sounds like the actual product
- **agendainsiderhq.com** - "HQ" feels corporate/official (could dilute if used for cold email)
- **agendainsiderhub.com** - "Hub" is vague, less trust signal
- **agendainsiderlabs.com** - "Labs" = experimental (not ideal for cold outreach)
- **agendainsiderly.com** - Awkward suffix, doesn't read smoothly
- **meetagendainsider.com** - Good for demo requests (use later in funnel)
- **openagendainsider.com** - "Open" unclear meaning
- **theagendainsider.com** - "The" makes it sound like blog/content site

**Strategic Reserve:**
- **meetagendainsider.com** - Save for demo booking sequences (Phase 3)
- **agendainsiderhq.com** - Save for high-value enterprise sequences
- **agendainsiderlabs.com** - Save for beta/innovation messaging

---

## Why Start with 3 (Not All 11)?

### Risk Mitigation:
1. **Test deliverability** - If one domain gets flagged, we don't burn all 11
2. **Learn send patterns** - Understand optimal daily volume before scaling
3. **A/B test domains** - See which domain name performs best with open rates
4. **Warming discipline** - Easier to monitor 3 domains than 11
5. **Preserve arsenal** - Keep 8 domains pristine for future campaigns

### Pilot Goals (3 Domains):
- **200 emails x 3 domains = 600 total pilot contacts**
- Measure: Open rate, reply rate, bounce rate, spam complaints
- **Decision gate:** If all 3 domains show >30% open, <1% bounce, <0.1% spam → scale to 11
- If problems → fix before burning more domains

---

## Instantly.ai Configuration Steps

### Step 1: API Connection
```bash
# Store API key securely (don't commit to GitHub)
export INSTANTLY_API_KEY="NWU1ZDRjMTgtZmFjYy00OGVhLTgyZWItYTI4MDE5Y2QxMjcwOllabWpabGpGd2NiRw=="

# Test connection
curl -X GET "https://api.instantly.ai/api/v1/account" \
  -H "Authorization: Bearer $INSTANTLY_API_KEY"
```

### Step 2: Add 3 Domains to Instantly
**In Instantly dashboard:**
1. Settings → Sending Accounts → Add Account
2. Enter domain: `tryagendainsider.com`
3. Provider: Custom SMTP (Namecheap)
4. Repeat for `getagendainsider.com` and `useagendainsider.com`

### Step 3: DNS Configuration (Critical)
**For EACH of the 3 domains, configure at Namecheap:**

#### SPF Record
```
Type: TXT
Host: @
Value: v=spf1 include:_spf.instantly.ai ~all
TTL: Automatic
```

#### DKIM Record
```
Type: TXT
Host: instantly._domainkey
Value: [Get from Instantly dashboard after adding domain]
TTL: Automatic
```

#### DMARC Record
```
Type: TXT
Host: _dmarc
Value: v=DMARC1; p=quarantine; rua=mailto:dmarc@agendainsider.com; pct=100; adkim=r; aspf=r
TTL: Automatic
```

#### MX Records (If not already set)
```
Priority 10: mail.privateemail.com
Priority 10: mail2.privateemail.com
```

**Verification timeline:** DNS propagation takes 1-24 hours (usually <4 hours)

---

## Warming Schedule (3 Domains)

### Phase 1: Days 1-7 (Low Volume)
- **Days 1-3:** 10-20 emails/day per domain
- **Days 4-7:** 20-30 emails/day per domain
- **Total sends week 1:** ~100 emails/domain

### Phase 2: Days 8-14 (Ramp Up)
- **Days 8-10:** 30-50 emails/day per domain
- **Days 11-14:** 50-80 emails/day per domain
- **Total sends week 2:** ~250 emails/domain

### Phase 3: Days 15-21 (Scale)
- **Days 15-17:** 80-120 emails/day per domain
- **Days 18-21:** 120-150 emails/day per domain
- **Total sends week 3:** ~450 emails/domain

### Phase 4: Days 22-30 (Full Capacity)
- **Days 22-30:** 150-200 emails/day per domain
- **Sustained capacity:** 150-200/day ongoing

**3 domains at full capacity = 450-600 emails/day**

---

## Pilot Launch Plan (Feb 18)

### Pilot Targets:
- **200 contacts** (Utah County + Salt Lake County only)
- **67 emails per domain** (tryagendainsider: 67, getagendainsider: 67, useagendainsider: 66)
- **Sequence:** Executive sequence (5 emails over 14 days)
- **Success criteria:**
  - Open rate >30%
  - Reply rate >2%
  - Bounce rate <2%
  - Spam complaints <0.1%

### If Pilot Succeeds (Feb 25 decision):
- Add remaining 8 domains to Instantly
- Begin warming cycle for domains 4-11
- Full launch Mar 10 (all 2,000 contacts)
- 11 domains at capacity = 1,650-2,200 emails/day

---

## Instantly Built-In Deliverability Monitoring

**Good news:** Aaron confirmed we're using Instantly's built-in deliverability tools (no GlockApps for now).

**Instantly provides:**
1. **Inbox placement tracking** - % landing in inbox vs. spam
2. **Engagement metrics** - Opens, clicks, replies per domain
3. **Domain health scores** - Reputation tracking per sending domain
4. **Spam trap detection** - Alerts if hitting known spam traps
5. **Bounce categorization** - Hard vs. soft bounces

**Monitoring protocol:**
- Check daily during warming (Feb 14-Mar 15)
- Red flags: Inbox rate <80%, bounce rate >2%, spam complaints >0.1%
- **If any domain shows problems:** Pause that domain immediately, diagnose before resuming

---

## Cost Breakdown

### Instantly.ai Pricing:
- **Plan needed:** Growth plan ($97/mo) - Supports unlimited domains, 5,000 contacts
- **Our usage:** 2,000 contacts, 11 domains = well within limits
- **Alternative:** If we scale beyond 5,000 contacts, upgrade to Hypergrowth ($197/mo)

**Month 1 cost (Instantly only):** $97  
**With Clay + Calendly (if approved):** $97 + $149 + $10 = $256/mo

---

## Next Steps (Aaron's Approval Required)

### Immediate (Today):
1. ✅ Domain selection - **tryagendainsider.com, getagendainsider.com, useagendainsider.com**
2. ⏳ **Aaron signs up for Instantly.ai** ($97/mo)
3. ⏳ **Aaron adds 3 domains to Instantly** (tryagenda, getagenda, useagenda)

### Tomorrow (Feb 13):
1. ⏳ **Aaron configures DNS records** at Namecheap (SPF, DKIM, DMARC for 3 domains)
2. ⏳ Verify DNS propagation (Jack can check via dig/nslookup)
3. ⏳ **Begin warming cycle** Feb 14 (Instantly automates this)

### Feb 18 (Pilot Launch):
1. ⏳ Load 200 pilot contacts into Instantly
2. ⏳ Assign 67 per domain (even distribution)
3. ⏳ Launch executive sequence
4. ⏳ Monitor daily for 7 days

### Feb 25 (Pilot Review):
1. ⏳ Evaluate metrics (open, reply, bounce, spam)
2. ⏳ **GO/NO-GO decision:** Scale to 11 domains or adjust?
3. ⏳ If GO → add 8 more domains, start warming Feb 26

---

## Product Feature Questions (Aaron's Input Needed)

**Before I can write killer cold emails, I need to answer:**

1. **Explore v2 (https://agendainsider.com/explore/v2)** - What does this feature do?
   - Is it a searchable database of planning agendas?
   - Can users filter by project type, location, date?
   - What's the value prop in one sentence?

2. **Map (https://agendainsider.com/map)** - What does this feature do?
   - Is it a geographic view of projects?
   - Can users see project concentration/heat maps?
   - What's the value prop in one sentence?

**Why I need this:**
- Cold email Hook #1 references the product benefit
- I can't write "Agenda Insider gives you [X]" if I don't know what [X] is
- Need 1-2 sentence description of each feature for email copy

**Aaron:** Can you describe in 30 seconds what Explore v2 and Map do? Or give me demo login credentials so I can see for myself?

---

## Git Status

**Current commits ready to push (4 total):**
1. `0d7fac1` - Campaign infrastructure (overnight Feb 12)
2. `c3efdc0` - Research & audit
3. `9a1b18c` - Final execution report
4. `f3e676e` - Cold email competitive research

**Blocker:** Git authentication (HTTPS requires token, SSH requires key)

**Options:**
1. **Aaron pushes manually** - `cd /tmp/Agenda-Insider && git push`
2. **Aaron gives Jack a GitHub token** - Store in ~/.gitconfig or env var
3. **Aaron sets up SSH key** - Generate key, add to GitHub, configure in container

**Jack's recommendation:** Aaron pushes manually tonight (fastest), set up token tomorrow for automation.

---

## Summary for Aaron

### ✅ COMPLETE:
- Competitive research done (construction email = 3,800% ROI, 4% target is conservative)
- 3 domains selected: **tryagendainsider, getagendainsider, useagendainsider**
- Instantly.ai configuration plan written
- DNS setup guide ready
- Warming schedule mapped
- Pilot plan designed (200 contacts, 3 domains, Feb 18 launch)

### ⏳ BLOCKED (Need Aaron):
1. **Sign up for Instantly.ai** - $97/mo, use API key: `NWU...FjbRw==`
2. **Configure DNS** for 3 domains (SPF, DKIM, DMARC) - Takes 10 minutes
3. **Describe product features** - What do Explore v2 and Map do? (30-second answer)
4. **Push git commits** - 4 commits ready in /tmp/Agenda-Insider

### 🎯 TIMELINE:
- **Feb 13:** Tools signup + DNS config (Aaron)
- **Feb 14:** Begin warming (automated)
- **Feb 18:** Pilot launch (200 contacts)
- **Feb 25:** GO/NO-GO decision (scale to 11 domains?)
- **Mar 10:** Full launch (2,000 contacts, all 11 domains)

---

**Jack is ready to execute the moment Aaron completes signup + DNS. No more blockers on my end.**
