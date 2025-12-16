# 📋 SOP: Secure Client Onboarding Checklist

**Role:** Implementation Analyst  
**Objective:** Ensure secure transition of services to live operation.  

## Phase 1: Pre-Implementation (Data Governance)
- [ ] **NDA Verification:** Confirmed active Non-Disclosure Agreement with client (A.6.6).
- [ ] **Secure Data Transfer:** Received user import data via Secure Portal. **Rejected** email attachments containing PII.
- [ ] **Data Minimization:** Verified import file contains only required fields. Deleted extraneous columns (e.g., personal mobile numbers).

## Phase 2: Configuration (Hardening)
- [ ] **Authentication Policy:**
    - [ ] Password Complexity: Min 12 chars, alphanumeric (A.5.17).
    - [ ] MFA: Enforced for *all* users (A.8.5).
    - [ ] Session Timeout: Set to 15 minutes idle.
- [ ] **Access Control (RBAC):**
    - [ ] Created 1x Super Admin (Client Owner).
    - [ ] Created Standard Users with Least Privilege roles.
    - [ ] *Validation:* Confirmed no "Generic Shared Accounts" exist.
- [ ] **Network Security:**
    - [ ] IP Whitelisting configured for client office VPN (if applicable).

## Phase 3: Transition & Cleanup
- [ ] **Audit Log Check:** Verified system audit logs are capturing login events and failed attempts (A.8.15).
- [ ] **Privilege Revocation:** Removed internal 'Implementation Admin' access rights (A.5.18).
- [ ] **Data Purge:** Securely deleted client source files from analyst workstation (Shift+Delete).
- [ ] **Handover:** Sent "Welcome Pack" via secure link. Ticket closed.