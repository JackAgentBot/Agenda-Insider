# DNS Configuration Guide - 12 Burner Domains

## Purpose
Set up SPF, DKIM, and DMARC records for all 12 domains to ensure email deliverability and domain reputation.

---

## Step-by-Step Setup (For Each Domain)

### Prerequisites
- Access to Namecheap DNS management
- ESP credentials (Smartlead API keys)
- DKIM keys from Smartlead

---

## Configuration for Each Domain

### 1. SPF Record (Sender Policy Framework)
Authorizes which mail servers can send email on behalf of your domain.

**DNS Record Type:** TXT  
**Host:** @ (or domain root)  
**Value:**
```
v=spf1 include:_spf.smartlead.ai ~all
```

**Explanation:**
- `v=spf1` - SPF version
- `include:_spf.smartlead.ai` - Authorize Smartlead's servers
- `~all` - Soft fail (recommended for warming phase)

**After 30 days of good reputation, change to:**
```
v=spf1 include:_spf.smartlead.ai -all
```
(Hard fail = stricter)

---

### 2. DKIM Record (DomainKeys Identified Mail)
Cryptographic signature that verifies email authenticity.

**DNS Record Type:** TXT  
**Host:** `smartlead._domainkey` (check Smartlead dashboard for exact value)  
**Value:** (Provided by Smartlead - looks like this)
```
v=DKIM1; k=rsa; p=MIGfMA0GCSqGSIb3DQEBA... (long key string)
```

**Where to get this:**
1. Log into Smartlead
2. Go to Settings → Domain Authentication
3. Copy DKIM key for each domain
4. Paste into Namecheap DNS

**TTL:** 3600 (1 hour)

---

### 3. DMARC Record (Domain-based Message Authentication)
Policy for handling emails that fail SPF/DKIM checks.

**DNS Record Type:** TXT  
**Host:** `_dmarc`  
**Value (WARMING PHASE - First 30 Days):**
```
v=DMARC1; p=none; rua=mailto:dmarc-reports@agendainsider.com; pct=100; adkim=r; aspf=r
```

**Explanation:**
- `p=none` - Monitor only (don't reject failed emails yet)
- `rua=mailto:...` - Send aggregate reports here
- `pct=100` - Apply policy to 100% of messages
- `adkim=r` - Relaxed DKIM alignment
- `aspf=r` - Relaxed SPF alignment

**After 30 days, change to strict policy:**
```
v=DMARC1; p=quarantine; rua=mailto:dmarc-reports@agendainsider.com; pct=100; adkim=s; aspf=s
```

**After 60 days (if reputation strong):**
```
v=DMARC1; p=reject; rua=mailto:dmarc-reports@agendainsider.com; pct=100; adkim=s; aspf=s
```

---

### 4. Custom Tracking Domain (Optional but Recommended)
Create a subdomain for link tracking to preserve main domain reputation.

**Example:** `track.domain1.com`

**DNS Record Type:** CNAME  
**Host:** `track`  
**Value:** (Provided by Smartlead)

---

## DNS Propagation & Verification

### Check DNS propagation (after adding records):
```bash
# Check SPF
dig TXT domain1.com

# Check DKIM
dig TXT smartlead._domainkey.domain1.com

# Check DMARC
dig TXT _dmarc.domain1.com
```

**Online tools:**
- https://mxtoolbox.com/SuperTool.aspx
- https://dmarcian.com/dmarc-inspector/
- https://www.mail-tester.com/

**Expected propagation time:** 1-48 hours (usually faster)

---

## Domain Warming Schedule

### Phase 1: Days 1-7 (Seed Phase)
- **Volume:** 10-20 emails/day per domain
- **Recipients:** High-quality seed lists (personal emails, internal team)
- **Purpose:** Establish sending pattern

### Phase 2: Days 8-14 (Ramp Phase)
- **Volume:** 30-50 emails/day per domain
- **Recipients:** Mix of seed + small batch of real prospects
- **Purpose:** Build reputation score

### Phase 3: Days 15-21 (Scale Phase)
- **Volume:** 75-150 emails/day per domain
- **Recipients:** Gradually increase real prospect ratio
- **Purpose:** Stabilize reputation

### Phase 4: Days 22-30 (Full Production)
- **Volume:** 150-200 emails/day per domain (max sustainable)
- **Recipients:** Full prospect lists
- **Purpose:** Maintain healthy reputation

---

## Reputation Monitoring

### Key Metrics to Track Daily:
- **Bounce rate:** Keep below 2%
- **Complaint rate:** Keep below 0.1%
- **Open rate:** Target >20%
- **Domain reputation score:** Check via SenderScore.org

### Red Flags (STOP SENDING if you see these):
- Bounce rate >5%
- Complaint rate >0.3%
- Sudden drop in open rate (>50% decrease)
- Domain blacklisted (check MXToolbox)

---

## Troubleshooting

### Issue: SPF record not validating
**Solution:** Ensure you're not exceeding 10 DNS lookups. Use `include:` sparingly.

### Issue: DKIM failing
**Solution:** 
- Verify DKIM selector matches Smartlead settings
- Check for typos in public key
- Ensure no line breaks in key value

### Issue: Emails going to spam
**Solution:**
- Slow down sending
- Check email content for spam triggers
- Verify all DNS records are passing
- Review complaint rate

### Issue: Domain blacklisted
**Solution:**
- Identify which blacklist (MXToolbox)
- Request delisting (each blacklist has own process)
- Pause sending until delisted
- Review what triggered the listing

---

## Quick Setup Checklist

For each of the 12 domains:

- [ ] Add SPF record
- [ ] Get DKIM key from Smartlead
- [ ] Add DKIM record
- [ ] Add DMARC record (monitoring mode)
- [ ] Set up tracking subdomain (optional)
- [ ] Verify all records propagate
- [ ] Connect domain to Smartlead
- [ ] Start warmup with seed emails (10/day)
- [ ] Monitor deliverability dashboard

---

## Batch Setup Script (When You Have Domain Names)

```bash
# Template for batch DNS updates via Namecheap API (if available)
# Replace DOMAIN_LIST with actual 12 domains

DOMAINS=("domain1.com" "domain2.com" ... "domain12.com")

for domain in "${DOMAINS[@]}"; do
    echo "Setting up $domain..."
    # Add SPF, DKIM, DMARC via API or manual
    # Log completion
    echo "$domain DNS configured"
done
```

---

## Contact for Issues
- **Namecheap Support:** https://www.namecheap.com/support/
- **Smartlead Support:** support@smartlead.ai
- **Deliverability Questions:** Jack (me) via Discord

---

## Next Steps
1. [ ] Get list of 12 domain names from Aaron
2. [ ] Log into Namecheap DNS manager
3. [ ] Configure all DNS records
4. [ ] Verify propagation
5. [ ] Begin warming schedule
