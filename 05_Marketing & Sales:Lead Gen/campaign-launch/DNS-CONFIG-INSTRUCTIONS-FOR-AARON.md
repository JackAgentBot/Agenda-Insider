# 🎯 DNS Configuration - Step-by-Step for Aaron

**Time to complete:** 15-20 minutes per domain (3-4 hours total for all 11)  
**Recommendation:** Do Batch 1 (3 domains) today, rest over next few days

---

## Prerequisites

✅ You have: 11 domains at Namecheap  
✅ You need: Namecheap login access  
✅ You need: Smartlead account (to get DKIM keys)

---

## Option 1: Jack Does It (FASTEST)

**If you want Jack to configure everything:**

1. Give Jack your Namecheap API key:
   - Log into Namecheap
   - Go to Profile → Tools → API Access
   - Enable API access
   - Generate API key
   - Give key to Jack via Discord

2. Give Jack your Smartlead API key:
   - Log into Smartlead
   - Go to Settings → API
   - Copy API key
   - Give to Jack

**Jack will then configure all 11 domains in ~1 hour and report back.**

---

## Option 2: You Do It Manually (PAINT-BY-NUMBERS)

### Step 1: Log into Namecheap
1. Go to https://www.namecheap.com/myaccount/login/
2. Log in
3. Click "Domain List" in left sidebar

### Step 2: For EACH Domain (Start with agendainsiderhq.com)

#### A. Access DNS Settings
1. Find the domain in your list
2. Click "Manage" button
3. Click "Advanced DNS" tab

#### B. Add SPF Record
1. Click "Add New Record"
2. Select "TXT Record" from dropdown
3. Fill in:
   - **Type:** TXT Record
   - **Host:** @ (just the @ symbol)
   - **Value:** `v=spf1 include:_spf.smartlead.ai ~all`
   - **TTL:** Automatic (or 3600)
4. Click checkmark to save

#### C. Add DKIM Record (Need Smartlead First)
**STOP HERE - You need DKIM key from Smartlead**

1. Log into Smartlead
2. Go to Settings → Email Accounts → Add Domain
3. Enter domain name (e.g., agendainsiderhq.com)
4. Smartlead will show you a DKIM key (long string starting with "v=DKIM1...")
5. Copy that DKIM key

**Back to Namecheap:**
1. Click "Add New Record"
2. Select "TXT Record"
3. Fill in:
   - **Type:** TXT Record
   - **Host:** `smartlead._domainkey`
   - **Value:** (Paste the DKIM key from Smartlead)
   - **TTL:** Automatic (or 3600)
4. Click checkmark to save

#### D. Add DMARC Record
1. Click "Add New Record"
2. Select "TXT Record"
3. Fill in:
   - **Type:** TXT Record
   - **Host:** `_dmarc`
   - **Value:** `v=DMARC1; p=none; rua=mailto:dmarc-reports@agendainsider.com; pct=100; adkim=r; aspf=r`
   - **TTL:** Automatic (or 3600)
4. Click checkmark to save

#### E. Verify DNS Records
**Wait 10 minutes, then check:**

1. Go to https://mxtoolbox.com/SuperTool.aspx
2. Enter: `txt:agendainsiderhq.com` (replace with your domain)
3. Click "TXT Lookup"
4. You should see your SPF record

5. Enter: `txt:smartlead._domainkey.agendainsiderhq.com`
6. Click "TXT Lookup"
7. You should see your DKIM record

8. Enter: `txt:_dmarc.agendainsiderhq.com`
9. Click "TXT Lookup"
10. You should see your DMARC record

#### F. Verify in Smartlead
1. Back to Smartlead → Settings → Email Accounts
2. Find the domain you just configured
3. Click "Verify DNS"
4. Should show green checkmarks for SPF and DKIM

---

### Step 3: Repeat for All 11 Domains

**Recommended order:**
1. agendainsiderhq.com ✅
2. agendainsiderlabs.com
3. tryagendainsider.com
4. getagendainsider.com
5. useagendainsider.com
6. meetagendainsider.com
7. theagendainsider.com
8. agendainsiderapp.com
9. agendainsiderhub.com
10. openagendainsider.com
11. agendainsiderly.com

**Pro tip:** Do 3 domains, take a break, do 3 more. Prevents mistakes from fatigue.

---

## Option 3: Jack Writes a Script, You Run It (MIDDLE GROUND)

Jack can write a Python script that automates the DNS configuration if you provide:
1. Namecheap API key
2. Smartlead API key

You review the script, approve it, and run it once. Done in 5 minutes.

**Want this option?** Tell Jack and he'll code it up.

---

## What Happens After DNS is Configured?

1. **DNS propagation:** Wait 24-48 hours for records to propagate globally
2. **Verification:** Jack will check all 11 domains are passing SPF/DKIM/DMARC
3. **Smartlead connection:** Jack will connect all domains to Smartlead
4. **Warming starts:** Feb 15 (or earlier if DNS propagates fast)
5. **Pilot launch:** Feb 18-20 (200 contacts)
6. **Full launch:** Feb 25-Mar 5 (2,000 contacts)

---

## Troubleshooting

### "SPF record not showing up"
- Wait 10-15 minutes, try again
- Check you entered `@` in Host field (not blank, not domain name)
- Check no typos in value

### "DKIM record not showing up"
- Wait 10-15 minutes
- Check Host is exactly `smartlead._domainkey` (no extra spaces)
- Check DKIM value has no line breaks (should be one continuous string)

### "Smartlead verification failing"
- Wait full 24 hours
- Click "Verify DNS" again
- Contact Smartlead support if still failing

### "I don't have Smartlead account yet"
- Jack can set one up for you (or you can create at smartlead.ai)
- Free trial available to start
- Once you have account, get DKIM keys and proceed

---

## Time Estimate

**If you do it manually:**
- First domain: 20 minutes (learning curve)
- Remaining 10 domains: 10 minutes each = 100 minutes
- **Total: ~2 hours spread over a few days**

**If Jack does it via API:**
- Jack codes script: 30 minutes
- Jack runs for all domains: 5 minutes
- **Total: 35 minutes, done today**

---

## Your Call

**Reply to Jack:**
- **Option A:** "Jack, configure everything" (give him API keys)
- **Option B:** "I'll do it manually" (follow steps above)
- **Option C:** "Jack, write me a script" (review & run)

**Recommendation:** Option A (fastest, Jack handles it) or Option C (you maintain control, Jack does the work)

---

## Next Steps After DNS Config

1. [ ] Configure sending schedules in Smartlead
2. [ ] Create warmup sequences
3. [ ] Set up seed email lists
4. [ ] Process contact lists (clean, segment, load)
5. [ ] Build landing page for trial signups
6. [ ] Launch pilot (200 contacts)

**Jack will handle all of this once DNS is done.**

---

**Questions?** Ask Jack on Discord. He's standing by to execute.

🦞 Ready when you are.
