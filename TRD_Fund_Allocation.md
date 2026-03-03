# Technical Requirement Document (TRD): Fund Allocation & Control Engine

## 1. System Overview
The Fund Allocation & Control Engine dictates how incoming funds are tracked, locked into designated accounts (Programs, Projects, or specific Students), and ultimately prevents double-spending or over-allocation.

## 2. API Endpoints Architecture

| Endpoint                     | Method | Role Required               | Description                                                        |
| ---------------------------- | ------ | --------------------------- | ------------------------------------------------------------------ |
| `/api/allocations`           | `GET`  | HO Admin, Chapter Treasurer | View current allocations, available balances.                      |
| `/api/allocations`           | `POST` | HO Admin                    | Perform partial/full fund allocations from a master donation fund. |
| `/api/allocations/{fund_id}` | `GET`  | HO Admin                    | See complete audit ledger for a specific fund chunk.               |

## 3. Database Schema (Entity-Relationship)

```mermaid
%%{init: {'theme': 'base', 'themeVariables': { 'primaryColor': '#2d51b3', 'edgeLabelBackground':'#181919', 'lineColor' : '#222' }}}%%
erDiagram
    FUND {
        uuid id PK
        string restriction_level "Unrestricted, Program-restricted, Student-restricted"
        decimal total_pool
        decimal allocated_amount
        decimal available_balance
        timestamp created_at
    }

    ALLOCATION_LEDGER {
        uuid id PK
        uuid fund_id FK
        uuid target_id "Polymorphic: Project ID or Student ID"
        string target_model "Type: Project, Student, Event"
        decimal allocated_amount
        uuid assigned_by_user_id FK
        timestamp allocated_at
    }

    FUND ||--o{ ALLOCATION_LEDGER : "distributes into"
```

## 4. Module Workflow Logic

### 4.1 Strict Allocation Lock Logic
The logic preventing fund over-allocation will be handled at the database constraints and internal Service class level.
```mermaid
sequenceDiagram
    participant Admin as HO Admin
    participant FundService
    participant DB

    Admin->>FundService: Allocate $500 to Event A (from Fund #200)
    FundService->>DB: Check FUND.available_balance (must be >= $500)
    alt Balance Insufficient
        DB-->>FundService: Return False
        FundService-->>Admin: Error: Insufficient Balance
    else Balance Sufficient
        FundService->>DB: Insert ALLOCATION_LEDGER entry
        FundService->>DB: Update FUND.allocated_amount
        DB-->>FundService: Success
        FundService-->>Admin: Allocation Completed
    end
```

## 5. Security & Isolation Rules
- **Immutability:** Financial ledger entries inside `ALLOCATION_LEDGER` are read-only (`insert` and `select` only, never `update` or `delete`). Reversals require a compensatory reverse-entry.
