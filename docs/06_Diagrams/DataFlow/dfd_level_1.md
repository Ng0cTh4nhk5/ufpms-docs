# DFD Level 1 - UFPMS Modules

> 📊 **Level**: 1  
> 🎯 **Scope**: 6 modules decomposition

---

## 📊 Data Flow Diagram Level 1

```mermaid
flowchart TD
    subgraph Actors["External Entities"]
        RES[Researcher]
        REV[Reviewers]
        ADM[Admin]
        PUB[Public]
    end
    
    subgraph Processes["UFPMS Processes"]
        P1[1.0<br/>Publication<br/>Management]
        P2[2.0<br/>Approval<br/>Workflow]
        P3[3.0<br/>Search &<br/>Browse]
        P4[4.0<br/>Researcher<br/>Profile]
        P5[5.0<br/>Reporting &<br/>Analytics]
        P6[6.0<br/>Admin &<br/>User Mgmt]
    end
    
    subgraph DataStores["Data Stores"]
        D1[(D1: Publications)]
        D2[(D2: Users)]
        D3[(D3: Review History)]
        D4[(D4: Audit Logs)]
    end
    
    %% Researcher flows
    RES -->|Publication data| P1
    P1 -->|Created publication| RES
    RES -->|Submit| P2
    P2 -->|Status updates| RES
    RES -->|Profile updates| P4
    P4 -->|Profile data| RES
    
    %% Reviewer flows
    REV -->|Review decision| P2
    P2 -->|Review assignments| REV
    REV -->|Report requests| P5
    P5 -->|Reports| REV
    
    %% Admin flows
    ADM -->|User management| P6
    P6 -->|System status| ADM
    ADM -->|System config| P6
    
    %% Public flows
    PUB -->|Search query| P3
    P3 -->|Search results| PUB
    PUB -->|Profile view request| P4
    P4 -->|Public profile| PUB
    
    %% Process to Data Store flows
    P1 <-->|CRUD publications| D1
    P2 <-->|Read publications| D1
    P2 -->|Write history| D3
    P3 -->|Read published| D1
    P4 <-->|Read users, publications| D2
    P4 <-->|Read publications| D1
    P5 -->|Read all data| D1
    P5 -->|Read users| D2
    P5 -->|Read history| D3
    P6 <-->|CRUD users| D2
    P6 <-->|Write audit| D4
    
    %% Inter-process flows
    P1 -.->|Trigger review| P2
    P2 -.->|Update pub status| P1
    
    style P1 fill:#6bcf7f
    style P2 fill:#ff6b9d
    style P3 fill:#4d96ff,color:#fff
    style P4 fill:#ffd93d
    style P5 fill:#c8b6ff
    style P6 fill:#ff9f43
```

---

## 📋 Processes

### 1.0 Publication Management
**Inputs**: Publication data (from Researcher)  
**Outputs**: Created/updated publications  
**Data Stores**: D1 (Publications)

### 2.0 Approval Workflow
**Inputs**: Submit requests, Review decisions  
**Outputs**: Status updates, Notifications  
**Data Stores**: D1 (Publications), D3 (Review History)

### 3.0 Search & Browse
**Inputs**: Search queries (from Public)  
**Outputs**: Search results  
**Data Stores**: D1 (Publications - READ ONLY, PUBLISHED only)

### 4.0 Researcher Profile
**Inputs**: Profile updates, View requests  
**Outputs**: Profile data  
**Data Stores**: D1 (Publications), D2 (Users)

### 5.0 Reporting & Analytics
**Inputs**: Report requests  
**Outputs**: Reports  
**Data Stores**: D1, D2, D3 (READ ONLY)

### 6.0 Admin & User Management
**Inputs**: User CRUD, System config  
**Outputs**: System status  
**Data Stores**: D2 (Users), D4 (Audit Logs)

---

## 💾 Data Stores

### D1: Publications
- publications table
- publication_authors table
- publication_types lookup

### D2: Users
- users table
- user_roles table
- departments, faculties tables

### D3: Review History
- review_history table
- review_comments table

### D4: Audit Logs
- audit_logs table

---

**Related**: dfd_level_0.md, dfd_level_2_approval.md  
**Created**: 10/02/2026
