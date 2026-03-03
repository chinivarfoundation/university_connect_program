# Technical Requirement Document (TRD): Donor & Donation Management System

## 1. System Overview
The Donor & Donation Management System is the primary ingestion module for external funding. It provides an interface for both HO Finance and Chapter Treasurers to log donations (online/offline) and securely manages donor master profiles.

## 2. API Endpoints Architecture

| Endpoint           | Method | Role Required                 | Description                                                                      |
| ------------------ | ------ | ----------------------------- | -------------------------------------------------------------------------------- |
| `/api/donors`      | `GET`  | HO Finance, Chapter Treasurer | Fetch list of all donors (Chapter Treasurers see only localized list unless HO). |
| `/api/donors`      | `POST` | HO Admin                      | Create a new donor profile.                                                      |
| `/api/donors/{id}` | `GET`  | HO Finance, Donor             | Get specific donor details including history.                                    |
| `/api/donations`   | `POST` | HO Finance, Chapter Treasurer | Record a new donation (triggers allocation logic and WhatsApp alert).            |
| `/api/reports/80g` | `GET`  | Donor                         | Generate and download 80G tax receipt.                                           |

## 3. Database Schema (Entity-Relationship)

```mermaid
%%{init: {'theme': 'base', 'themeVariables': { 'primaryColor': '#0883b2', 'edgeLabelBackground':'#181919', 'lineColor' : '#222' }}}%%
erDiagram
    DONOR {
        uuid id PK
        string name "Individual or Institution Name"
        string pan_number "Required for 80G"
        string contact_email
        string contact_phone
        enum donor_type "Individual, Institution"
        timestamp created_at
    }

    DONATION {
        uuid id PK
        uuid donor_id FK
        decimal total_amount
        enum payment_method "Online, Offline, Cheque"
        string reference_id "Transaction/Cheque Number"
        boolean is_80g_issued
        timestamp date_received
    }

    DONOR ||--o{ DONATION : "makes"
```

## 4. Module Workflow Logic

### 4.1 Donation Ingestion Workflow
```mermaid
sequenceDiagram
    participant User as Chapter Treasurer
    participant API as Donation Controller
    participant DB as MySQL Database
    participant Allocation as Allocation Engine
    participant WA as WhatsApp Service

    User->>API: POST /api/donations (Amount, Donor ID)
    API->>DB: Validate Donor Profile
    API->>DB: Insert record to DONATION table
    API->>Allocation: Trigger Partial/Full Allocation rules
    Allocation-->>API: Return Allocation Status
    API->>WA: Queue Async Donor Receipt Message
    API-->>User: 201 Created (Success)
```

## 5. Security & Isolation Rules
- **Chapter Isolation:** Treasurers associated with Chapter A cannot execute `GET /api/donors` without a tenant-scope middleware appending `WHERE chapter_id = X` to the Eloquent query.
- **Audit Trails:** Ensure every manipulation in `DONATION` executes an event listener logging into an `audit_logs` table tracking the specific `user_id` modifying records.
