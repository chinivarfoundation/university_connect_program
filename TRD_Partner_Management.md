# Technical Requirement Document (TRD): Partner Management System

## 1. System Overview
The Partner Management system centralizes the profiles and compliance data for all external entities interacting with Chinivar Foundation, including NGO beneficiaries, partner schools, and vendors.
 
## 2. API Endpoints Architecture

| Endpoint                       | Method | Role Required     | Description                                                       |
| ------------------------------ | ------ | ----------------- | ----------------------------------------------------------------- |
| `/api/partners`                | `GET`  | All Admins        | List all partners with filtering by type.                         |
| `/api/partners`                | `POST` | HO Admin          | Onboard a new partner entity.                                     |
| `/api/partners/{id}/documents` | `POST` | Chapter Treasurer | Upload compliance docs (e.g., Trust Deed, PAN, Cancelled Cheque). |
| `/api/partners/{id}/history`   | `GET`  | HO Admin          | View transaction and engagement history with the partner.         |

## 3. Database Schema (Entity-Relationship)

```mermaid
%%{init: {'theme': 'base', 'themeVariables': { 'primaryColor': '#6134b5', 'edgeLabelBackground':'#181919', 'lineColor' : '#222' }}}%%
erDiagram
    PARTNER {
        uuid id PK
        string name
        enum partner_type "NGO, School, Vendor"
        string contact_person
        string phone
        string email
        json dynamic_attributes "Flexible fields per type"
        boolean is_verified
        timestamp created_at
    }

    PARTNER_DOCUMENT {
        uuid id PK
        uuid partner_id FK
        string doc_type "Compliance, Agreement, Identity"
        string file_url
        timestamp expiry_date
        timestamp uploaded_at
    }

    PARTNER ||--o{ PARTNER_DOCUMENT : "provides"
```

## 4. Module Workflow Logic

### 4.1 Partner Verification Flow
```mermaid
sequenceDiagram
    participant Admin as Chapter Lead
    participant API as Partner Controller
    participant HO as HO Finance
    participant DB as MySQL

    Admin->>API: POST /api/partners (Initial Data)
    API->>DB: Save as 'Pending'
    Admin->>API: Upload mandatory documents
    API->>HO: Notify for verification
    HO->>API: PATCH /api/partners/{id}/verify
    API->>DB: Update is_verified = TRUE
    API-->>Admin: Partner Active
```

## 5. Security & Isolation Rules
- **Dynamic Attributes:** Use JSON columns in MySQL to allow for different field sets (e.g., Aadhar for individuals, GST for vendors) without schema migrations for setiap partner type.
- **Sensitive Docs:** Partner documents stored in S3 must use pre-signed URLs with a 5-minute expiry to prevent unauthorized link sharing.
