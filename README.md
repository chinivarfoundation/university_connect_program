![Chinivar Foundation Logo](https://chinivarfoundation.org/Chinivar-Foundation-Horizontal-Logo-Transperent-Small.png)

# Chinivar Foundation - Digital Platform

Welcome to the documentation repository for the Chinivar Foundation digital platform. This project aims to build a single, scalable ecosystem to manage the foundation's federated operations, focusing on transparency and measurable impact.

## About Chinivar Foundation
Chinivar Foundation is a Section 8 not-for-profit organization headquartered in India, dedicated to breaking the cycle of generational poverty. The foundation operates under the **BELAKU** initiative—a guiding light representing their core values of care, transparency, and holistic child development.

**Core Mission:**
- **Education:** Providing quality learning opportunities through programs like *BELAKU Shikshana* and *BELAKU Shaale*.
- **Food Security:** Ensuring nutritional support through the *BELAKU Aahara* program.
- **Holistic Development:** Treating every child as our own to ensure a future filled with hope.

## Requirement Overview
The digital platform is designed to consolidate the foundation's federated operations into a single, high-visibility technical framework. Below is the summary of requirements captured from the [Initial Requirements Document](./initial_requirements.md).

### 1. Unified Organizational Structure
- **Head Office (HO):** Centralized governance, compliance, auditing, and global data visibility.
- **Chapters (Town/City Units):** Local fundraising and execution with chapter-level data isolation and accountability.
- **Vertical Programs:** Dedicated workflows for specialized initiatives (Ahara, Shikshana, Shaale).

### 2. Core Functional Modules
- **Donor & Donation Management:** Tracking individual/institutional donors, progressive donation allocation, and statutory receipting (80G/10A).
- **Fund Allocation Engine:** Strict lock mechanisms to prevent over-allocation and ensure funds are utilized as per donor intent.
- **Fundraising & Leads:** Pipeline management for potential donors with automated conversion tracking.
- **Partner Management:** Verification and document management for NGO beneficiaries and vendors.
- **Program Systems:** End-to-end lifecycle management for Food Distribution (Aahara) and Student Sponsorship (Shikshana).
- **Communication Gateway:** A "WhatsApp-first" approach for real-time donor updates and automated notifications.

### 3. Key Technical Pillars
- **Access Control:** Role-based access (HO Admin to Mentors) with strict data segregation between chapters.
- **Transparency:** Real-time consolidated dashboards for HO and granular impact tracking for donors.
- **Scalability:** Built on a modular Laravel/MySQL stack, ready for a 10x growth trajectory.

## Technology Stack
- **Backend Framework:** Laravel
- **Database:** MySQL

## Documentation Index

1. **[Product Requirement Document (PRD)](./PRD.md)**
   - Functional and non-functional requirements.
2. **[Project Roadmap](./ROADMAP.md)**
   - 4-month implementation timeline (April - July).
3. **[System Architecture](./system_architecture.md)**
   - Colorful high-level system diagram and module map.

### Technical Requirement Documents (TRDs)
- [Donor & Donation Management](./TRD_Donor_Management.md)
- [Fund Allocation & Control](./TRD_Fund_Allocation.md)
- [Fundraising & Lead Management](./TRD_Fundraising.md)
- [BELAKU Aahara (Food Program)](./TRD_Aahara_Food.md)
- [Partner Management](./TRD_Partner_Management.md)
- [BELAKU Shikshana (Student Sponsorship)](./TRD_Shikshana_Sponsorship.md)
- [WhatsApp Communication System](./TRD_WhatsApp_Communication.md)
