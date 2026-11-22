# edtech-portal-agile-delivery-lab
# EdTech Student Portal Rollout — Agile Scrum, Dependency & Vendor Delivery Lab

A hands-on Agile Scrum, Technical Program Management (TPM), and Security Governance case study simulating a **2-sprint rollout of a K-12 & Higher-Ed Student Learning Portal (`EDTECH-PORTAL`)**.

This lab demonstrates how a technical facilitator bridges **Engineering**, **Product**, **EdTech Curriculum**, and an **External LMS Implementation Vendor** while enforcing **IAM / SSO / MFA security controls** and **Third-Party Risk Management (TPRM)**.

---

## 1. Project Scope & Objectives
* **Product:** Cloud-based K-12 / Higher-Ed Student Learning Portal supporting district Single Sign-On (SSO), assignment submissions, teacher grading rubrics, WCAG 2.1 AA accessibility, and nightly LMS gradebook sync.
* **Delivery Cadence:** Two 2-week Scrum sprints (`Sprint 1: Completed`, `Sprint 2: Active`).
* **Governance Focus:** Backlog refinement, cross-team dependency unpacking, scope trade-off facilitation, external vendor SLA enforcement, and identity/access readiness.

---

## 2. Sprint Backlog & Execution Summary

### Sprint 1 — Foundation, IAM Controls & API Contracts *(Completed — 16 Story Points)*
| ID | Epic | User Story | Points | Status | Key Acceptance Criteria |
| :--- | :--- | :--- | :---: | :---: | :--- |
| **ED-101** | District SSO & Identity Access | Configure SAML/OAuth SSO login for K-12 teachers & students | 5 | Done | District IdP login works; RBAC separates Teacher vs. Student views. |
| **ED-102** | District SSO & Identity Access | Implement MFA enforcement for school district admin accounts | 3 | Done | Admin accounts require MFA on every login; sign-in audit logs enabled. |
| **ED-103** | Core Course & Assignment Hub | Build student assignment submission & due-date dashboard | 5 | Done | Students view active courses, upload files, and verify submission status. |
| **ED-107** | External LMS Vendor Integration | Define REST API payload contract with external LMS data vendor | 3 | Done | Vendor signs off on JSON schema & data privacy checklist for grade sync. |

### Sprint 2 — Grading Workflows, Accessibility & Vendor Integration *(Active — 18 Committed Points)*
| ID | Epic | User Story | Points | Status | Key Acceptance Criteria & Facilitation Notes |
| :--- | :--- | :--- | :---: | :---: | :--- |
| **ED-104** | Core Course & Assignment Hub | Create teacher grading rubric & feedback workflow | 5 | In Progress | Teachers score submissions and publish feedback within 5 seconds. |
| **ED-105** | Core Course & Assignment Hub | Add WCAG 2.1 AA screen-reader & keyboard accessibility support | 3 | In Progress | Portal navigation passes automated accessibility audit for K-12 compliance. |
| **ED-108** | External LMS Vendor Integration | Build webhook listener for external vendor gradebook sync | 5 | **Blocked** | **Blocker:** Awaiting vendor sandbox SSL cert (escalated via Vendor SLA tracker). |
| **ED-109** | External LMS Vendor Integration | Execute end-to-end UAT with 3 pilot school district coordinators | 5 | To Do | Zero Sev-1/Sev-2 defects across roster import, SSO login, and grading. |
| **ED-106** | Core Course & Assignment Hub | Build custom district analytics export *(Descoped via Trade-Off)* | 8 | **Backlog** | Deferred to Sprint 3 to protect WCAG compliance and pilot UAT timeline. |

---

## 3. Cross-Team Dependency & Trade-Off Log
| ID | Dependency / Bottleneck | Teams Involved | Technical Assumption Unpacked | Trade-Off & Resolution Facilitated |
| :--- | :--- | :--- | :--- | :--- |
| **DEP-01** | **Gradebook Sync Webhook (`ED-108`)** blocked by delayed sandbox credentials from External LMS Partner | **Engineering** ↔ **External Vendor** | Engineering assumed vendor sandbox keys were self-service; vendor required manual security review (5-day SLA). | Triggered 48-hour vendor escalation; unblocked Engineering using mock JSON payloads while keeping UAT (`ED-109`) on schedule. |
| **DEP-02** | **Sprint 2 Capacity Conflict** between Custom Analytics (`ED-106`) and Accessibility Compliance (`ED-105`) | **Product** ↔ **Engineering** ↔ **EdTech Curriculum** | Product assumed both fit in Sprint 2; probing engineering dependencies revealed shared UI components would create merge risk. | Facilitated trade-off alignment: **deferred `ED-106` (8 pts) to Sprint 3** to guarantee WCAG 2.1 AA compliance and on-time district UAT. |
| **DEP-03** | **District SSO Role Mapping (`ED-101`)** required standardized teacher/student attribute naming | **Engineering** ↔ **District IT Admins** | District IT used custom SAML attribute claims; Engineering built a configurable attribute-mapping table instead of hardcoding. | Eliminated onboarding rework across pilot school districts. |

---

## 4. External Implementation Partner — Milestone & Quality Gate Tracker
| Milestone | RACI Ownership | Target Date | Quality Gate / Exit Criteria | Current Status & Escalation Action |
| :--- | :--- | :---: | :--- | :--- |
| **M1: API Schema & Security Sign-Off** | Vendor Tech Lead (**R**), Agile/TPM Lead (**A**), Security (**C**) | Sprint 1, Day 4 | Signed OpenAPI spec + FERPA/data privacy checklist verified | **Complete** — Approved with zero revisions. |
| **M2: Sandbox Environment & Test Roster** | Vendor Implementation (**R**), Engineering (**C**), Agile Lead (**I**) | Sprint 2, Day 2 | Valid SSL endpoint + 500 anonymized K-12 student records loaded | **Delayed (+2 Days)** — Escalated to Vendor Account Manager; daily 15-min check-in instituted until resolved. |
| **M3: Pilot District UAT Sign-Off** | EdTech Curriculum Lead (**R**), Agile/TPM Lead (**A**), Vendor (**C**) | Sprint 2, Day 9 | >= 99% roster sync accuracy; zero Sev-1/Sev-2 defects | **Scheduled** — UAT test scripts distributed to 3 pilot district coordinators. |

---

## 5. Sprint 1 Retrospective Summary
* **What Went Well:** Probing SAML attribute assumptions during backlog refinement prevented mid-sprint rework on `ED-101`. Delivered **16/16 committed story points (100% predictability)** in Sprint 1.
* **What Could Be Improved:** Assumed external vendor sandbox provisioning (`ED-108`) was automated rather than gated by a manual security review, creating a Sprint 2 blocker.
* **Action Items for Sprint 2:**
  1. **Update Definition of Ready (DoR):** Require confirmed third-party sandbox credentials *one full sprint prior* to scheduling integration stories.
  2. **Protect Team Focus:** Descope `ED-106` (Custom Analytics, 8 pts) to Sprint 3 so Engineering can complete `ED-104`, `ED-105`, and pilot UAT without quality compromises.
