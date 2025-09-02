# Step 2 — Configure Auto-Labeling in Microsoft Purview

---

## ✅ Prerequisites

- Step 1 completed (sensitivity labels created and published).  
- Microsoft 365 tenant with Purview auto-labeling capability.  
- At least one synthetic test file/email with PCI-like strings (from Step 1).  

**Estimated time:** 45–60 minutes  

---

## 🔎 What you will build

- A **custom sensitive information type (SIT)** to detect PAN-like patterns.  
- An **auto-labeling policy** that applies the “PCI Data” label automatically.  
- A repeatable test process with baseline metrics.  
- Updated evidence artifacts (screenshots, metrics log, sample data).  

---

## 1) Create a custom sensitive information type

1. Go to **Purview portal → Data classification → Sensitive info types → Create**.  
2. Name: `PAN with Context`.  
3. Description: “Matches PAN patterns only when accompanied by cardholder context (name/expiry).”  
4. Primary pattern: Use the built-in **Credit Card Number** regex template.  
5. Supporting elements: Add keywords like `Expiry`, `Exp`, `CVV`, `Name`, `Customer`.  
6. Confidence level: High → requires both the PAN regex and at least one supporting element nearby.  
7. Save the SIT.  

📸 Capture a screenshot of the SIT configuration for evidence.  

---

## 2) Create an auto-labeling policy

1. Go to **Information Protection → Auto-labeling policies → Create**.  
2. Name: `PCI Data Auto-Labeling`.  
3. Choose info to detect: select your SIT `PAN with Context`.  
4. Choose label to apply: `PCI Data (Cardholder Data)`.  
5. Scope: Start with **Exchange email** and **SharePoint/OneDrive documents**.  
6. Mode: Choose **Simulation** first (recommended).  
   - Simulation runs detection without applying labels.  
7. Save the policy.  

📸 Capture a screenshot of the policy summary page.  

---

## 3) Run the simulation

1. Wait for policy deployment (can take up to 1 hour).  
2. Upload your test document (`pci_test_doc.txt`) to OneDrive or SharePoint.  
3. Send the test email with synthetic PAN strings to your test user.  
4. In **Purview → Auto-labeling policy → View simulation results**:  
   - Note how many items matched.  
   - Review the confidence level.  

📸 Capture a screenshot of the simulation results.  

---

## 4) Switch to enforcement mode

Once simulation looks correct:

1. Edit the policy.  
2. Change from **Simulation** to **Enforce**.  
3. Save.  
4. Wait for enforcement (up to 1 hour).  

Re-test by uploading the same file and sending the same email.  
Confirm that the label is now applied **automatically**.  

📸 Capture a screenshot of the label being applied without manual action.  

---

## 5) Record updated metrics

Update your metrics log (`/topics/pci-dss-azure/manuscript/metrics.csv`) with a new row:

| step       | items_tested | manually_labeled | auto_labeled | false_positives | notes                                       | timestamp   |
|------------|--------------|------------------|--------------|-----------------|---------------------------------------------|-------------|
| 2-auto     | 4            | 0                | 4            | 0               | Auto-labeling applied correctly with context | YYYY-MM-DD |

---

## 6) Collect and Organize Your Evidence

As part of good security governance (and for audit or research purposes), keep clear records of what you’ve done:

- **Screenshots** → save images of the SIT configuration, the auto-labeling policy, and the results.  
- **Test data** → keep a copy of your synthetic test document and email sample.  
- **Metrics log** → update your `metrics.csv` file with the new Step 2 row.  

📂 Suggested structure for storing these in your lab project:  
- `/figures/step2_*` → screenshots  
- `/data/` → synthetic test documents  
- `/manuscript/metrics.csv` → updated metrics table  

---

## 7) Evidence checklist for Step 2

- [ ] Screenshot of custom SIT config  
- [ ] Screenshot of auto-labeling policy (simulation mode)  
- [ ] Screenshot of simulation results  
- [ ] Screenshot of auto-labeled item in Word/Outlook/Explorer  
- [ ] Updated metrics log with Step 2 row  

---

## Troubleshooting

- **Policy not triggering:** Wait up to 60 minutes after enabling.  
- **False positives:** Add more supporting keywords or increase confidence.  
- **Nothing detected:** Ensure your test data includes both PAN + context.  

---

## Next Step
