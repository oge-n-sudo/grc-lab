# Step 1 — Create a PCI DSS Sensitivity Label in Microsoft Purview

**Goal (You):** Create a reusable sensitivity label for PCI card data, scoped and documented for audit.  
**Goal (Reader):** Follow the same steps in their tenant and verify the results with synthetic data.

---

## ✅ Prerequisites

- **Microsoft 365** tenant with Purview Information Protection (E5 trial is fine).
- Admin rights to create labels (Compliance Administrator/Security Administrator or equivalent).
- A test user mailbox (e.g., `lab.user@yourtenant.onmicrosoft.com`).
- Synthetic test files (we’ll create them below — no real card data).

**Time:** ~30–45 minutes

---

## 🔎 What you will build

- A sensitivity label: **“PCI Data (Cardholder Data)”**
- A sublabel (optional): **“PCI Data — High Risk (PAN present)”**
- A label policy that publishes the label to selected users
- A small, safe **test kit** with synthetic PAN-like strings

---

## 1) Design your label structure (2 minutes)

Decide the names you’ll use:

- **Parent label:** `PCI Data (Cardholder Data)`
- **Sublabel (optional):** `PCI Data — High Risk (PAN present)`

> Rationale: Parent label for general PCI scope; sublabel for confirmed Primary Account Number (PAN) presence.

---

## 2) Create the parent label (10–15 minutes)

1. Go to **Microsoft Purview portal** → **Information Protection** → **Labels** → **Create a label**.
2. **Name:** `PCI Data (Cardholder Data)`
3. **Description for users:**  
   “Use this label for any document or email that may contain PCI cardholder data (PAN, cardholder name, expiration).”
4. **Admin description:**  
   “Intended for PCI DSS 4.0 scope classification. Used with auto-labeling and DLP policies.”
5. **Encryption (optional at this step):** Leave **off** for now to avoid blocking your tests. You can enable later.
6. **Content marking:**  
   - Header text: `PCI Data` (optional)  
   - Footer text: `Contains PCI Cardholder Data` (optional)  
   - Watermark: skip for now (you can add in later steps).
7. **Auto-labeling (do not enable here):** We’ll configure **centralized auto-labeling** in Step 2 of the lab.
8. **Create** the label.

> 📸 **Evidence tip:** Screenshot the label summary page after creation.

---

## 3) (Optional) Create a sublabel for confirmed PAN

1. On the `PCI Data (Cardholder Data)` label, choose **Add sublabel**.
2. **Name:** `PCI Data — High Risk (PAN present)`
3. **User description:** “For content containing confirmed PAN patterns.”
4. **Admin description:** “Triggers stricter DLP actions in later steps.”
5. Keep encryption/content marking **off** for now.
6. **Create** the sublabel.

---

## 4) Publish the label (5–10 minutes)

You need a **label policy** so users/apps can see the label.

1. **Information Protection** → **Label policies** → **Publish labels**.
2. Select the label(s):  
   - `PCI Data (Cardholder Data)`  
   - `PCI Data — High Risk (PAN present)` (if created)
3. **Choose users/groups:** Start with your test user(s) only.
4. **Policy settings:**  
   - Do **not** set as default (for now).  
   - Optional: Require justification to remove the label.
5. **Name policy:** `PCI Labels — Pilot`
6. **Publish**.

> ⏱️ Propagation can take up to 24 hours; usually much faster. If labels don’t show yet, wait a bit or restart Office apps.

---

## 5) Prepare synthetic test data (safe) (5 minutes)

Create a test file and email that **look** like they have card numbers but are **synthetic**.

> ⚠️ Never use real card data. These examples are generated and will not pass live checks.

**Create a test document (`/topics/pci-dss-azure/data/pci_test_doc.txt`):**

Customer: Jane Doe
Order: 123-456-789
PAN-like examples for testing ONLY (synthetic):
Visa: 4111 1111 1111 1111
Mastercard: 5555-5555-5555-4444
Amex: 3782 822463 10005
Expiry: 12/29  CVV: 123 (synthetic)

**Create a test email** from your admin to the test user:  
Subject: `Test: PCI Labeling`  
Body (include the same synthetic lines above).

> 💡 These strings are common **test patterns**. In Step 2 you’ll tune auto-labeling and DLP to detect a “PAN” pattern with context (name/expiry) to reduce false positives.

---

## 6) Manually apply the label (user test) (5–10 minutes)

On a machine signed in as the **test user**:

- Open the test document in **Word** (or upload to **SharePoint/OneDrive** and open in Word for the web).
- Go to **Sensitivity** → choose **PCI Data (Cardholder Data)**.
- Save the file, close, reopen — confirm the label persists.
- Forward the **test email** in Outlook and apply the label from the **Sensitivity** menu.

**Capture evidence:**
- Screenshot the **Sensitivity** menu showing the label.
- Screenshot the **File → Info** pane showing the applied label.

---

## 7) Validate in Purview Activity/Content Explorer (5 minutes)

- In **Purview** → **Data Loss Prevention** or **Content Explorer** (if available to your role), verify that labeled items appear as expected for your test user.  
- Note the **count** of labeled items (documents/emails).

> 📸 Screenshot the activity or explorer results for your evidence pack.

---

## 8) Record metrics (2 minutes)

Create `/topics/pci-dss-azure/manuscript/metrics.csv` and add a line:

step,items_tested,manually_labeled,auto_labeled,false_positives,notes,timestamp
1-baseline,2,2,0,0,“Manual label works; auto not enabled yet”,

You’ll update this table again in Step 2 (auto-labeling) and Step 3 (DLP).

---

## 9) Save artifacts to your repo (2 minutes)

- Place screenshots in: `/topics/pci-dss-azure/figures/step1_*`
- Place the synthetic test file in: `/topics/pci-dss-azure/data/pci_test_doc.txt`
- Commit with a clear message:
  - `git add .`
  - `git commit -m "PCI Step 1: Created PCI labels, published policy, manual labeling validated"`

---

## 10) What’s next

- **Step 2:** Configure **auto-labeling** in Purview using a **custom sensitive info type** for PAN with context rules (name/expiry proximity). Measure **precision/recall**.  
- **Step 3:** Create **DLP policies** (SharePoint/OneDrive/Exchange/Teams) with escalating actions (audit → block external → block & override with justification). Track **false positives** and **exceptions**.

---

## Troubleshooting

- **Labels not visible:** Wait up to 24h, restart Office apps, confirm the user is in the **publish policy** scope.  
- **Sensitivity button missing:** Ensure the Office apps are logged in with the **scoped test user** and have **Information Protection** enabled in that tenant.  
- **Content Explorer empty:** You may need additional **Purview RBAC** permissions or to wait for indexing.

---

## Visa-friendly evidence checklist for Step 1

- [ ] Screenshot of label configuration summary  
- [ ] Screenshot of label policy (publish) scope  
- [ ] Screenshot of manual label applied in Word/Outlook  
- [ ] Purview explorer/activity screenshot  
- [ ] `metrics.csv` update committed  
- [ ] Commit history showing timestamps and author
