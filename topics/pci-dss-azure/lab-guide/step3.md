# Step 3 — Apply DLP Policies with Escalating Enforcement

**Goal (You):** Build and test Data Loss Prevention (DLP) policies that control how PCI-labeled content is handled across Microsoft 365 services.  
**Goal (Reader):** Learn how to design escalating DLP actions (audit → block external → block & override) and evaluate false positives.

---

## ✅ Prerequisites

- Step 1 (labels created) and Step 2 (auto-labeling policy enforced) completed.  
- Microsoft 365 tenant with Purview DLP capabilities.  
- At least one auto-labeled file and one auto-labeled email from Step 2.  

**Estimated time:** 60–90 minutes  

---

## 🔎 What you will build

- A **DLP policy** scoped to SharePoint, OneDrive, Exchange, and Teams.  
- Three **rule levels** with escalating enforcement:  
  1. **Audit only** (log activity, no user impact)  
  2. **Block external sharing** (prevent sending/sharing outside domain)  
  3. **Block with override** (block, but allow business-justified overrides)  
- A test plan to measure effectiveness and false positives.  
- An evidence pack with metrics and screenshots.  

---

## 1) Create a baseline DLP policy

1. Go to **Purview portal → Data Loss Prevention → Policies → Create policy**.  
2. Template: choose **Custom policy**.  
3. Name: `PCI DSS DLP – Pilot`.  
4. Choose locations: **Exchange, SharePoint, OneDrive, Teams**.  
5. Define condition:  
   - Content contains the sensitivity label **PCI Data (Cardholder Data)**.  
6. Define action: **Audit only** (log the event, notify admin).  
7. Save and publish.  

📸 Capture a screenshot of the policy summary.  

---

## 2) Test the baseline rule

- Upload the labeled test document to OneDrive.  
- Share the file externally → should succeed, but activity logged.  
- Send the test email externally → should deliver, but logged.  

📸 Capture a screenshot of the audit logs showing detected activity.  

---

## 3) Add a stricter rule — block external sharing

1. Edit the policy → add a new rule.  
2. Condition: content contains **PCI Data (Cardholder Data)**.  
3. Action: **Block sharing with people outside your organization**.  
4. User notification: enable **policy tip** (e.g., “Sharing blocked: PCI DSS content”).  
5. Save.  

📸 Capture a screenshot of the rule configuration.  

---

## 4) Test the block rule

- Attempt to share the test file with an external Gmail/Outlook account.  
- Attempt to send the test email externally.  
- Both actions should be **blocked**.  

📸 Capture screenshots of the block message in Outlook/SharePoint.  

---

## 5) Add the override option

1. Edit the policy again → add a third rule.  
2. Condition: content contains **PCI Data (Cardholder Data)**.  
3. Action: **Block sharing**.  
4. Add override: allow users to **override with business justification**.  
5. Enable logging of justification text.  
6. Save.  

📸 Capture a screenshot of the override configuration.  

---

## 6) Test the override rule

- Attempt to send or share labeled content externally.  
- Choose the **override** option and enter justification.  
- Confirm the action succeeds with justification recorded.  

📸 Capture a screenshot of the justification prompt.  

---

## 7) Record metrics

Update your metrics log (`metrics.csv`) with Step 3 results:

| step       | items_tested | manually_labeled | auto_labeled | false_positives | notes                                        | timestamp   |
|------------|--------------|------------------|--------------|-----------------|----------------------------------------------|-------------|
| 3-dlp      | 6            | 0                | 6            | 1               | DLP enforced: 2 blocked, 1 override, 1 false positive | YYYY-MM-DD |

---

## 8) Collect and Organize Your Evidence

- **Screenshots**:  
  - Policy summary  
  - Audit log entry (baseline)  
  - Block messages (email and file sharing)  
  - Override justification prompt  
- **Metrics**: updated `metrics.csv` file  
- **Test data**: synthetic PCI documents/emails  

📂 Suggested storage in your lab project:  
- `/figures/step3_*` → screenshots  
- `/manuscript/metrics.csv` → updated table  
- `/data/` → synthetic test data  

---

## 9) Evidence checklist for Step 3

- [ ] Screenshot of baseline policy (audit mode)  
- [ ] Screenshot of block rule configuration  
- [ ] Screenshot of override rule configuration  
- [ ] Screenshot of audit log entry  
- [ ] Screenshot of block message in Outlook/SharePoint  
- [ ] Screenshot of override justification prompt  
- [ ] Updated metrics log with Step 3 row  

---

## Troubleshooting

- **No audit entries:** Ensure the policy is applied to the right services.  
- **Block not working:** Confirm the condition is tied to the sensitivity label, not just keywords.  
- **Override option missing:** Re-check the rule config; override must be explicitly enabled.  

---

## End of PCI DSS 4.0 Lab (Steps 1–3)

At this stage you have:  
- A working **sensitivity label** for PCI data.  
- **Auto-labeling** that applies it based on custom patterns.  
- **DLP policies** that escalate from logging → blocking → override.  

This forms a reproducible case study of how Microsoft 365 Purview can meet PCI DSS 4.0 requirements for protecting cardholder data.  