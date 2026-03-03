# Product Requirement Document (PRD)

## 1. Executive Summary

### 1.1 Objective
To build a **single, scalable digital platform** that enables Chinivar Foundation to operate as a **federated NGO with chapters and programs**, while ensuring **financial transparency, compliance, donor trust, and measurable impact**, including the operations for running a **full-fledged school**.

### 1.2 Scale Vision & Outcomes
- **Scale targets:** 10+ chapters, 10,000+ donors, 5,000+ students, 1 school (expandable).
- **Core outcomes:**
  - Real-time financial visibility
  - Chapter-level accountability
  - Donor trust through transparency
  - Student-centric impact tracking
  - Low operational overhead

## 2. Technology Stack & Architecture
- **Web Application Framework:** Laravel (PHP)
- **Database:** MySQL
- **Architecture Philosophy:** Modular, API-first, Secure & Audit-ready.
- **Cost Efficiency:** Priority on cost-effective, open-source-friendly tooling.

## 3. Organizational Structure & Access Configuration

### 3.1 Federated Structure
- **Level 1: Head Office (HO)**
  - Single legal entity, centralized compliance and audit.
  - Controls governance, policy, financial consolidation, and program standards.
  - Requires full data visibility, override/approval rights, and consolidated dashboards.
- **Level 2: Chapters (Town / City Units)**
  - Local fundraising, local program execution.
  - Chapter-level accounting and quarterly reporting to HO.
  - Requires data isolation (by chapter) and chapter-level dashboards.
- **Level 3: Vertical Programs**
  - BELAKU Shikshana (Education Sponsorship)
  - BELAKU Aahara (Food Program)
  - BELAKU Shaale (School)
  - Requires program-specific workflows, specific program dashboards, and fund tagging.

### 3.2 User Roles & Access
Role-based access controls with deep chapter-level data isolation:
- HO Admin
- HO Finance
- Chapter President
- Chapter Treasurer
- Chapter Team
- School Admin
- Mentor (Portal access with no license cost)
- Donor (Portal access with no license cost)

## 4. Sub-Systems & Core Functional Requirements

### 4.1 Donor & Donation Management System
*Users: HO Finance, Chapter Treasurer, Donors*
- **Management:** Track donors (individuals/institutions). View total funds, history, and fund allocations across projects.
- **Processing:** Online and offline donations, splitting donations across multiple purposes.
- **Compliance:** Statutory receipt generation (e.g., 80G) and annual donor documentation (10A).
- **Automated Workflow:** Let donations be partially allocated. When a donation is received or allocated, send automated WhatsApp updates regarding contribution, allocation distribution, and remaining balance.

### 4.2 Fund Allocation & Control Engine
- Control logic restricting donations strictly to their intended purposes.
- Multi-line allocation (Program vs. Project/Event vs. Student targets).
- Management of Restricted vs. Unrestricted funds.
- Over-allocation prevention constraints resulting in an uneditable allocation ledger.

### 4.3 Fundraising & Lead Management
- Tools for Lead Capture and Campaign mapping.
- Lead conversion tracking and renewal/reminder automations.
- Campaign performance analytics evaluating return on impact/funding.

### 4.4 Partner Management System
- Profile management for external entities: NGO beneficiaries, schools, and vendors.
- Features dynamic fields, compliance tracking, direct document uploads, and comprehensive engagement history mapping.

### 4.5 BELAKU Aahara (Food Program System)
- Event and Project creation tied with fund allocation parameters.
- Beneficiary NGO mapping.
- Direct uploads for bills, grocery lists, and visual proof (photos).
- Deep utilization tracking at the granular event level.

### 4.6 BELAKU Shikshana (Student Sponsorship System)
- End-to-end management of the sponsored student lifecycle (New -> Background Verification -> Internal Review -> Selected/Rejected).
- Central Student Master handling documents, CARE model tracking, mentor updates, and PTM logs.
- Map donors strictly per academic year matching to the student timeline.
- Donor-facing student summaries generated automatically.

### 4.7 WhatsApp Communication System
- Principal external channel for communication.
- Automated core notifications, document/receipt deliveries, and event invites.
- Internal chatbot capability assisting Donors and Mentors.
- Central persistence for all communication logs.

## 5. Dashboards & Reporting Requirements
Real-time insights mandate the following interactive dashboards:
- HO Consolidated Dashboard
- Chapter Dashboard
- Finance Dashboard
- Specific Program Dashboards
- Donor Impact Dashboard
- Student Impact Dashboard
- Mentorship Dashboard

## 6. Implementation Phasing
1. **Phase 1:** Core foundation & finance (HO/Chapter setup, Base Laravel Setup, Auth).
2. **Phase 2:** Donor & fund allocation logic.
3. **Phase 3:** Vertical Programs (Aahara, Shikshana implementation).
4. **Phase 4:** WhatsApp integration & external portals.
5. **Phase 5:** School management system (BELAKU Shaale).
