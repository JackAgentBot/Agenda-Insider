# ✅ DOMAIN LIST - RECEIVED FEB 12, 2026

## The 11 Domains (All Active, Expires Feb 2027)

1. **agendainsiderapp.com**
2. **agendainsiderhq.com**
3. **agendainsiderhub.com**
4. **agendainsiderlabs.com**
5. **agendainsiderly.com**
6. **getagendainsider.com**
7. **meetagendainsider.com**
8. **openagendainsider.com**
9. **theagendainsider.com**
10. **tryagendainsider.com**
11. **useagendainsider.com**

**Status:** All active at Namecheap, auto-renew enabled, privacy protection ON

---

## DNS Configuration Plan

### Priority Order (Configure in This Sequence)
Start with most "professional" sounding domains first:

**Batch 1 (Priority - Today):**
1. agendainsiderhq.com
2. agendainsiderlabs.com
3. tryagendainsider.com

**Batch 2 (High Priority - Tomorrow):**
4. getagendainsider.com
5. useagendainsider.com
6. meetagendainsider.com

**Batch 3 (Medium Priority - This Weekend):**
7. theagendainsider.com
8. agendainsiderapp.com
9. agendainsiderhub.com

**Batch 4 (Lower Priority - Next Week):**
10. openagendainsider.com
11. agendainsiderly.com

---

## DNS Records Needed for Each Domain

### SPF Record
**Type:** TXT  
**Host:** @  
**Value:** `v=spf1 include:_spf.smartlead.ai ~all`

### DKIM Record
**Type:** TXT  
**Host:** `smartlead._domainkey`  
**Value:** (Get from Smartlead dashboard for each domain)

### DMARC Record (Monitoring Phase - First 30 Days)
**Type:** TXT  
**Host:** `_dmarc`  
**Value:** `v=DMARC1; p=none; rua=mailto:dmarc-reports@agendainsider.com; pct=100; adkim=r; aspf=r`

---

## Campaign Math (Updated for 11 Domains)

**Total contacts:** 2,000  
**Domains:** 11  
**Emails per domain per day (at scale):** ~182 emails/day  
**Total daily send capacity:** 2,000 emails/day (11 × 182)

**Phase distribution:**
- Days 1-7: 11 × 20 = 220 emails/day
- Days 8-14: 11 × 75 = 825 emails/day
- Days 15-21: 11 × 150 = 1,650 emails/day
- Days 22-30: 11 × 182 = 2,002 emails/day (full capacity)

---

## Next Immediate Actions

1. ✅ Copy domains to campaign tracker
2. [ ] Log into Namecheap DNS manager
3. [ ] Configure SPF records (Batch 1 - 3 domains today)
4. [ ] Get DKIM keys from Smartlead
5. [ ] Configure DKIM records
6. [ ] Configure DMARC records
7. [ ] Verify DNS propagation (24-48 hours)
8. [ ] Start warming schedule (Feb 15)

---

## Smartlead Configuration Needed

For each domain, we need:
- DKIM public key
- Domain verification
- Daily send limits configured
- Warmup sequence enabled

**BLOCKER:** Still need Smartlead access (API key or login)

---

**Status:** UNBLOCKED - Ready to configure DNS  
**Next Step:** Aaron provides Namecheap login OR approves Jack to configure via API
