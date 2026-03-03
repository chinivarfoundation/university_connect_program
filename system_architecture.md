# System Architecture Document (with Multi-Module Entity Flow)

This document visualizes the macro system architecture for the Chinivar Foundation Platform leveraging Laravel & MySQL architecture alongside frontend logic interactions.

```mermaid
%%{init: {'theme': 'base', 'themeVariables': { 'primaryColor': '#0883b2', 'edgeLabelBackground':'#181919', 'tertiaryColor': '#cc99cc', 'lineColor' : '#222' }}}%%
graph TD
   subgraph External Users
        D([Donors & Mentors - Web Portal]):::external
        V[Vendors & Beneficiaries - Uploads & Verification]:::external
        M((WhatsApp / SMS Channel)):::channel
   end
   
   D -- "Auth & Donate" --> A(Laravel Access Gateway / API):::core
   M -- "Updates & Alerts" --> A
   V -- "Access & Submission" --> A
   
   subgraph Core Laravel Engine 
        A --> |Routing & Middlewares| B
        B{Application Logistics Controller}:::core
        
        B -.-> |Donation Processing| D_MONEY[Donor Module]:::module_don
        B -.-> |Verification & Profile| D_PART[Partner Management Module]:::module_part
        B -.-> |Fund Locks & Grants| D_ALLOC[Allocation Engine]:::module_allo
        
        B -.-> |Sponsorship Workflow| P_SHIKSHANA[Shikshana Module: Student Sponsorship]:::module_shik
        B -.-> |Food & Event Workflow| P_AHARA[Aahara Module: Food Program]:::module_aha
   end

   subgraph Federated Governance (Admin Backoffice)
        HO((Head Office Admin)):::admin --> B
        HOF(Head Office Finance):::admin --> B
        
        CA((Chapter Admins)):::chapterad --> B
        CT(Chapter Treasurer):::chapterad --> B
   end
   
   subgraph Global Database Cluster MySQL
       D_MONEY --> DS[(Donation Tables & Ledger)]:::db
       D_PART --> PS[(User & Partner Records)]:::db
       D_ALLOC --> AS[(Allocated Funds Track)]:::db
       
       P_SHIKSHANA --> SSS[(Student Master & TIMING)]:::db
       P_AHARA --> SAS[(Events, Foods, Target Funds)]:::db
   end 

   %% Color Definitions
   classDef core fill:#0f4b63,stroke:#fff,stroke-width:2px,color:#fff;
   classDef admin fill:#8f1153,stroke:#fff,stroke-width:2px,color:#fff;
   classDef chapterad fill:#9e612f,stroke:#fff,stroke-width:2px,color:#fff;
   classDef external fill:#1e873b,stroke:#000,stroke-width:2px,color:#fff;
   classDef channel fill:#1ca33f,stroke:#fff,color:#fff;
   classDef module_don fill:#4287f5,stroke:#000,color:#fff;
   classDef module_part fill:#6134b5,stroke:#000,color:#fff;
   classDef module_allo fill:#2d51b3,stroke:#000,color:#fff;
   classDef module_shik fill:#b8991a,stroke:#000,color:#fff;
   classDef module_aha fill:#ba5e13,stroke:#000,color:#fff;
   classDef db fill:#363533,stroke:#e8c610,stroke-width:3px,color:#fff;
```

### Module Responsibilities Map:
- **Donors Module ([module_don]):** Inhalation mechanisms. Securing leads and processing payment links for single/re-occurring funds.
- **Partner Management Module ([module_part]):** Managing Vendor/NGO verifications dynamically.
- **Allocation Engine ([module_allo]):** Rigid financial gates to prevent spending unauthorized values to specific restricted chapters.
- **Shikshana Module ([module_shik]):** Workflow mapping background checks vs CARE student approvals, tied directly to matching sponsorship budgets.
- **Aahara Module ([module_aha]):** Creation of events & direct food distribution campaigns matched with grocery lists and partner distribution points.

