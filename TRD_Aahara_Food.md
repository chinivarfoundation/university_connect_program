# Technical Requirement Document (TRD): BELAKU Aahara (Food Program System)

## 1. System Overview
The BELAKU Aahara subsystem controls the implementation of the food distribution arm of the NGO. It directly coordinates Target Entities (Beneficiary NGOs/Partners), Allocation rules, and distribution artifacts (Photos, grocery lists, bills) into auditable Project Events.

## 2. API Endpoints Architecture

| Endpoint                              | Method | Role Required          | Description                                                |
| ------------------------------------- | ------ | ---------------------- | ---------------------------------------------------------- |
| `/api/aahara/projects`                | `GET`  | All Admins             | List all ongoing and completed food distribution projects. |
| `/api/aahara/projects`                | `POST` | HO Admin, Chapter Pres | Create a new food project, tying an allocation ID.         |
| `/api/aahara/projects/{id}/artifacts` | `POST` | Chapter Team           | Upload proof (bills, grocery list, photos) to the project. |
| `/api/aahara/utilizations`            | `GET`  | HO Admin               | Fetch event-level specific utilization metrics.            |

## 3. Database Schema (Entity-Relationship)

```mermaid
%%{init: {'theme': 'base', 'themeVariables': { 'primaryColor': '#ba5e13', 'edgeLabelBackground':'#181919', 'lineColor' : '#222' }}}%%
erDiagram
    AAHARA_PROJECT {
        uuid id PK
        string title
        uuid external_partner_id FK
        uuid allocation_id FK
        text description
        timestamp scheduled_date
        string status "Draft, Active, Completed, Audited"
    }

    ARTIFACT {
        uuid id PK
        uuid project_id FK
        enum document_type "Grocery_List, Bill, Event_Photo"
        string s3_link "URL to object storage"
        decimal claimed_amount
        uuid uploaded_by_user_id FK
    }

    AAHARA_PROJECT ||--o{ ARTIFACT : "validates through"
```

## 4. Module Workflow Logic

### 4.1 Artifact Validation & Auditing
```mermaid
sequenceDiagram
    participant Team as Chapter Volunteer
    participant API as Aahara Controller
    participant AWS as S3 Storage
    participant DB as MySQL

    Team->>API: Upload Artifact (Type: Bill, Image Binary)
    API->>AWS: Secure PutObject(Binary)
    AWS-->>API: Returns S3 URL
    API->>DB: Insert into ARTIFACT (Project ID, URL)
    DB-->>API: Created
    API-->>Team: Artifact Successfully Captured
```

## 5. Security & Isolation Rules
- **Artifact Lockdown:** Once a project status marks as `Audited`, all related `ARTIFACT` records become locked on the backend. No user (not even HO Admin) can execute a standard update query.
