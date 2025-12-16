# Third-Party Risk Management (TPRM) Framework with ISO 27001 and ITIL 4

A practical, risk-based framework for assessing third-party vendors before onboarding.  
Designed to support secure SaaS ecosystems by ensuring suppliers meet baseline security expectations before they are introduced into production environments.

**Context:** Supply Chain Security and Vendor Onboarding  
**Alignment:** ISO/IEC 27001:2022 Annex A (A.5.19, A.5.20, A.5.21, A.5.22) and ITIL 4  

---

## 📖 Overview
Modern services rarely operate in isolation. Most platforms rely on external vendors for hosting, analytics, payments, support tooling or AI-driven functionality. Each integration introduces risk, often outside direct organisational control. This project presents a **risk-based Third-Party Risk Management (TPRM) framework** that focuses on the controls that matter most. Rather than relying on long, generic questionnaires, it prioritises evidence-backed security fundamentals such as encryption, access control, incident handling, and operational resilience. The framework is designed to support informed decision-making. It enables security and delivery teams to recommend approval, rejection, or conditional acceptance of vendors based on documented risk not assumptions.

---

## 🎯 Objectives

1. Standardise how new vendors are assessed before onboarding  
2. Focus assessment effort on critical security controls  
3. Translate vendor responses into a clear risk outcome (Low, Medium, High)  
4. Support contractual and onboarding decisions with documented evidence  
5. Enable periodic review and reassessment of supplier risk  

---

## 🔄 Assessment Workflow
The framework follows a simple, repeatable process that ensures no vendor is onboarded without a documented risk decision.

```mermaid
graph LR
    Request[Business Request] -->|Data Scope Identified| VSQ[Vendor Security Questionnaire]
    VSQ -->|Vendor Response| Review[Analyst Review & Evidence Check]
    Review -->|Apply Scoring Matrix| Score{Risk Rating}
    Score -->|High Risk| Reject[Reject or Require Mitigation]
    Score -->|Low/Medium Risk| Report[Due Diligence Report]
    Report -->|Approval| Contract[Contract & Onboarding]
```
Each stage has a clear owner and output, creating traceability from request to decision.

---

## 🧭 Control Alignment
This framework aligns with the supplier relationship controls in ISO/IEC 27001:2022:
1. A.5.19 – Information security in supplier relationships
Overall governance of third-party security expectations.
2. A.5.20 – Addressing information security within supplier agreements
Contractual clauses, breach notification commitments and right-to-audit conditions.
3. A.5.21 – Managing information security in the ICT supply chain
Assessment of SaaS providers, sub-processors, hosting and integrations.
4. A.5.22 – Monitoring, review, and change management of supplier services
Periodic reassessment and conditional approvals based on risk.
5. From an ITIL 4 perspective, the framework supports Information Security Management, Supplier Management, Change Enablement and Knowledge Management.


