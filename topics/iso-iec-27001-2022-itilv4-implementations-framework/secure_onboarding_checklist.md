# 📋 SOP: Secure Client Onboarding Checklist

**Role:** Implementation Analyst  
**Objective:** Ensure secure transition of services to live operation through controlled configuration, access management and evidence capture.  
**Framework Alignment:** ISO/IEC 27001:2022, ITIL 4

---

## Phase 1: Pre-Implementation (Data Governance)
*Focus: Information Classification & Handling*
- [ ] **Contractual prerequisites:** Confirm contractual and confidentiality requirements are in place prior to onboarding.
- [ ] **Secure data transfer:** User import data received only via approved secure channels (for example secure portal or SFTP). Email attachments containing PII are rejected.
- [ ] **Data minimisation:** Import files reviewed prior to processing. Non-essential fields removed (for example personal mobile numbers) and changes documented.

---

## Phase 2: Configuration (Hardening)
*Focus: Access Control & Security Baselines*
### Authentication Policy
- [ ] **Password policy:** Enforced according to organisational baseline (minimum length, complexity) (A.5.17).
- [ ] **Multi-factor authentication:** Enforced for all users, including administrators (A.5.17).
- [ ] **Session management:** Idle session timeout configured to 15 minutes in line with baseline.

### Access Control (RBAC)
- [ ] **Privileged access:** Named administrative account created for the client owner.
- [ ] **Least privilege:** Standard users assigned roles aligned to business need.
- [ ] **Account validation:** Confirmed no generic or shared administrator accounts exist (A.5.15, A.5.16).

### Network and Platform Controls
- [ ] **Network restrictions:** IP allow-listing configured for client office VPN where applicable.
- [ ] **Baseline verification:** Platform configuration validated against the approved secure baseline (A.8.9).

---

## Phase 3: Transition and Cleanup
*Focus: Logging, Change Management & Clean Close*
- [ ] **Audit logging:** Verified authentication events, failed login attempts, and privilege changes are captured and retained (A.8.15).
- [ ] **Privilege revocation:** Implementation-only elevated access removed immediately after handover (A.5.18).
- [ ] **Onboarding data removal:** Temporary onboarding files removed from endpoints and any sync locations in accordance with information deletion and retention requirements (A.8.10).
- [ ] **Handover and closure:** Handover pack delivered via secure link and onboarding ticket formally closed.

---

*> **Note:** This secure onboarding checklist is designed to align with ISO/IEC 27001:2022 Annex A control themes and ITIL 4 service management practices. The activities in this SOP primarily support controls relating to acceptable use and information handling (A.5.10, A.5.12–A.5.14), access control and authentication (A.5.15–A.5.18), configuration management (A.8.9), logging and monitoring (A.8.15–A.8.16), change management during transition (A.8.32) and information deletion (A.8.10).

From an ITIL 4 perspective, the checklist supports Information Security Management, Service Configuration Management, Change Enablement and Knowledge Management by embedding security and governance requirements directly into onboarding and transition activities rather than treating them as separate assurance tasks.