# Chinivar Foundation

# PART A: 1-PAGE EXECUTIVE OVERVIEW (FOR BOARD / VENDORS)

## Objective

To build a **single, scalable digital platform** that enables Chinivar Foundation to operate
as a **federated NGO with chapters and programs** , while ensuring **financial
transparency, compliance, donor trust, and measurable impact** , including running a
**full-fledged school**.

## Key Characteristics

- Single legal entity with federated chapters
- Central governance with local execution
- Program-based impact delivery
- Restricted & unrestricted fund management
- WhatsApp-first external communication
- Portal-based access for donors & mentors

## Scale Vision

- 10+ chapters
- 10,000+ donors
- 5,000+ students
- 1 school (expandable)

## System Outcomes

- Real-time financial visibility
- Chapter-level accountability
- Donor trust through transparency
- Student-centric impact tracking
- Low operational overhead


# PART B: ORGANIZATIONAL STRUCTURE REQUIREMENT

## B1. Legal Entity

- Organization Name: Chinivar Foundation
- Single legal entity
- Centralized compliance & audit
 
## B2. Federated Structure

### Level 1: Head Office (HO)

**Responsibilities** : - Governance & policy - Financial consolidation - Audit & compliance -
Program design & standards - Consolidated reporting

**System Needs** : - Full data visibility - Override & approval rights - Consolidated dashboards

### Level 2: Chapters (Town / City Units)

Each chapter has: - Chapter lead + team + volunteers

**Responsibilities** : - Local fundraising - Local program execution - Chapter-level accounting

- Quarterly reporting to HO

**System Needs** : - Data isolation by chapter - Chapter-level dashboards - Chapter-wise
finance & reports

### Level 3: Vertical Programs

- BELAKU Shikshana (Education Sponsorship)
- BELAKU Aahara (Food Program)
- BELAKU Shaale (School)

**System Needs** : - Program-specific workflows - Program dashboards - Fund tagging by
program

# PART C: APPLICATION-WISE SAMPLE REQUIREMENT

# DOCUMENTS


## APP 1: DONOR & DONATION MANAGEMENT SYSTEM

### Purpose

To manage donors, donations, compliance, fund allocation, and donor transparency.

### Users

- HO finance
- Chapter treasurer
- Donors (portal)

### Core Functional Requirements

- Donor master (individual / institution)
    o Each donor view should show total funds, number of donations, fund
       allocation to projects and link to project
- Donation recording (online / offline)
- Donation splitting across multiple purposes
- Track: received, allocated, utilized, balance
- Generate statutory receipts (e.g., 80G)
- Annual donor documentation (e.g., 10A)
- Partial fund allocation to projects
    Example :

The system must support partial and progressive allocation of a single donation across
multiple programs, projects, events, or beneficiaries, while maintaining real-time tracking
of total amount received, allocated, utilized, and remaining balance. For example, if a
donor contributes ₹10,000.00, the amount may be partially allocated to multiple BELAKU
Aahara projects, with the remaining balance retained for future allocation. Upon donation
receipt and/or allocation, the system must automatically generate a personalized
WhatsApp message summarizing the total contribution, allocation breakup (if applicable),
and remaining unallocated balance.


### Outputs

- Donor dashboard
- Fund utilization statements
- Compliance-ready reports

## APP 2: FUND ALLOCATION & CONTROL ENGINE

### Purpose

To ensure donations are used strictly for intended purposes.

### Functional Requirements

- Multi-line allocation per donation
- Allocation targets:
    o Program
    o Project / Event
    o Student
- Restricted vs unrestricted fund logic
- Prevent over-allocation

### Outputs

- Allocation ledger
- Available balance per fund
- Audit trail

## APP 3: FUNDRAISING & LEAD MANAGEMENT

### Purpose

To manage fundraising campaigns and donor conversion.

### Functional Requirements

- Lead capture
- Campaign management
- Conversion tracking
- Renewal reminders
- Campaign performance analytics


## APP 4: PARTNER MANAGEMENT SYSTEM

### Purpose

To manage all external partner entities.

### Partner Types

- NGO beneficiaries
- Schools
- Vendors

### Functional Requirements

- Partner profiles with dynamic fields
- Compliance tracking
- Document uploads
- Engagement history

## APP 5: BELAKU AAHARA – FOOD PROGRAM SYSTEM

### Purpose

To manage food distribution projects and utilization.

### Functional Requirements

- Create events / projects
- Allocate funds
- Map beneficiary NGOs
- Upload grocery lists, bills, photos
- Event-level utilization tracking

### Outputs

- Project dashboards
- Utilization reports

## APP 6: BELAKU SHIKSHANA – STUDENT SPONSORSHIP SYSTEM

### Purpose

To manage sponsored students end-to-end.


### Student Lifecycle

New → Background Verification → Internal Review → Selected / Rejected

### Functional Requirements

- Student master & documents
- CARE model tracking
- Mentor updates & PTM logs
- Student timeline
- Donor mapping per academic year

### Outputs

- Student dashboard
- Donor-facing student summary


## APP 7: WHATSAPP COMMUNICATION SYSTEM

### Purpose

To serve as the primary external communication channel.

### Functional Requirements

- Automated notifications
- Document delivery
- Event invitations
- Chatbot for donors & mentors
- Communication logs


# PART D: ACCESS & PERMISSION REQUIREMENTS

## User Levels

- HO Admin
- HO Finance
- Chapter President
- Chapter Treasurer
- Chapter Team
- School Admin
- Mentor
- Donor

## Access Principles

- Role-based access
- Chapter-level data isolation
- Donors & mentors via portal (no paid licenses)

# PART E: DASHBOARDS & REPORTING REQUIREMENTS

### Mandatory Dashboards

- HO consolidated dashboard
- Chapter dashboard
- Finance dashboard
- Program dashboards
- Donor impact dashboard
- Student impact dashboard
- Mentorship dashboard

# PART F: NON-FUNCTIONAL REQUIREMENTS

- Modular architecture
- API-first
- Secure & audit-ready
- Scalable to 10x growth


- Cost-effective & open-source friendly

# PART G: IMPLEMENTATION PHASING (SAMPLE)

1. Core foundation & finance
2. Donor & fund allocation
3. Programs (Aahara, Shikshana)
4. WhatsApp & portals
5. School system

**Prepared for:** Chinivar Foundation
**Use:** Sample requirement document for vendors & internal planning


