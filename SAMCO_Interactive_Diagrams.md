# SAMCO Interactive Architecture Diagrams

> **How to navigate:** Click any highlighted node to jump to the detailed diagram for that layer.
> Each detail diagram has a **⬆ Back to Overview** link to return here.

---

## Overview

```mermaid
graph TB
    subgraph Presentation["Presentation Layer"]
        PRES["🖥 Presentation Layer<br/>Menus · Display Files · Printer Files"]
    end

    subgraph Business["Business Logic Layer"]
        BIZ["⚙ Business Logic Layer<br/>Programs · Service Programs · CL · Utilities"]
    end

    subgraph Data["Data Access Layer"]
        DAT["🗄 Data Access Layer<br/>Physical Files · Logical Files · SQL Objects"]
    end

    subgraph Integration["Integration Layer"]
        INT["🔗 Integration Layer<br/>Data Areas · Message Files · IBM APIs · IFS"]
    end

    PRES --> BIZ
    BIZ --> DAT
    BIZ --> INT

    click PRES "https://github.com/jmhossain/mermaid-diagrams/blob/main/SAMCO_Interactive_Diagrams.md#presentation-layer-detail"
    click BIZ "https://github.com/jmhossain/mermaid-diagrams/blob/main/SAMCO_Interactive_Diagrams.md#business-logic-layer-detail"
    click DAT "https://github.com/jmhossain/mermaid-diagrams/blob/main/SAMCO_Interactive_Diagrams.md#data-access-layer-detail"
    click INT "https://github.com/jmhossain/mermaid-diagrams/blob/main/SAMCO_Interactive_Diagrams.md#integration-layer-detail"

    style Presentation fill:#e1f5ff
    style Business fill:#fff3e0
    style Data fill:#f3e5f5
    style Integration fill:#e8f5e9
    style PRES color:#0066cc,cursor:pointer
    style BIZ color:#cc6600,cursor:pointer
    style DAT color:#660099,cursor:pointer
    style INT color:#006600,cursor:pointer
```

> 💡 **Tip:** In GitHub-rendered Markdown, clicking a highlighted node jumps directly to that section below.

---

## Presentation Layer Detail

[⬆ Back to Overview](#overview)

```mermaid
graph TB
    subgraph Presentation["Presentation Layer"]
        MENU["SAMMNU<br/>Main Menu"]
        DSPF["Display Files<br/>ORD100D · ORD200D<br/>ART200D · CUS200D"]
        PRTF["Printer Files<br/>ORD500O"]
    end

    MENU -->|"navigates to"| DSPF
    MENU -->|"triggers"| PRTF

    click MENU "https://github.com/jmhossain/mermaid-diagrams/blob/main/SAMCO_Interactive_Diagrams.md#business-logic-layer-detail" "Jump to Business Logic"
    click DSPF "https://github.com/jmhossain/mermaid-diagrams/blob/main/SAMCO_Interactive_Diagrams.md#business-logic-layer-detail" "Jump to Business Logic"
    click PRTF "https://github.com/jmhossain/mermaid-diagrams/blob/main/SAMCO_Interactive_Diagrams.md#business-logic-layer-detail" "Jump to Business Logic"

    style Presentation fill:#e1f5ff
    style MENU color:#0066cc,cursor:pointer
    style DSPF color:#0066cc,cursor:pointer
    style PRTF color:#0066cc,cursor:pointer
```

---

## Business Logic Layer Detail

[⬆ Back to Overview](#overview)

```mermaid
graph TB
    subgraph Business["Business Logic Layer"]
        PGM["Interactive Programs<br/>ORD100 · ORD200<br/>ART200 · CUS200"]
        SRVPGM["Service Programs<br/>FARTICLE · FCUSTOMER<br/>FCOUNTRY · FPROVIDER"]
        CL["CL Programs<br/>ORD100C · ORD500C · PAR201"]
        UTIL["Utilities<br/>LOG100 · DAT001 · TXT001 · XML001"]
    end

    PGM --> SRVPGM
    PGM --> CL
    PGM --> UTIL

    click PGM "https://github.com/jmhossain/mermaid-diagrams/blob/main/SAMCO_Interactive_Diagrams.md#order-creation-workflow" "See Order Creation Workflow"
    click SRVPGM "https://github.com/jmhossain/mermaid-diagrams/blob/main/SAMCO_Interactive_Diagrams.md#service-program-architecture" "See Service Program Architecture"

    style Business fill:#fff3e0
    style PGM color:#cc6600,cursor:pointer
    style SRVPGM color:#cc6600,cursor:pointer
```

---

## Data Access Layer Detail

[⬆ Back to Overview](#overview)

```mermaid
graph TB
    subgraph Data["Data Access Layer"]
        PF["Physical Files<br/>ARTICLE · CUSTOMER<br/>ORDER · DETORD"]
        LF["Logical Files<br/>ARTICLE2 · CUSTOME1 · ORDER1"]
        SQL["SQL Objects<br/>Views · Procedures<br/>Functions · Triggers"]
    end

    PF -->|"indexed by"| LF
    PF -->|"abstracted by"| SQL

    click PF "https://github.com/jmhossain/mermaid-diagrams/blob/main/SAMCO_Interactive_Diagrams.md#entity-relationship-diagram" "See Entity Relationship Diagram"
    click SQL "https://github.com/jmhossain/mermaid-diagrams/blob/main/SAMCO_Interactive_Diagrams.md#entity-relationship-diagram" "See Entity Relationship Diagram"

    style Data fill:#f3e5f5
    style PF color:#660099,cursor:pointer
    style SQL color:#660099,cursor:pointer
```

---

## Integration Layer Detail

[⬆ Back to Overview](#overview)

```mermaid
graph TB
    subgraph Integration["Integration Layer"]
        DTAARA["Data Areas<br/>LASTORDNO"]
        MSGF["Message Files<br/>SAMMSGF · SGSMSGF"]
        API["IBM System APIs"]
        IFS["IFS Files<br/>Data Exchange"]
    end

    DTAARA -->|"order sequencing"| API
    MSGF -->|"error reporting"| API

    style Integration fill:#e8f5e9
```

---

## Entity Relationship Diagram

[⬆ Back to Overview](#overview) | [⬆ Data Access Layer](#data-access-layer-detail)

```mermaid
erDiagram
    CUSTOMER ||--o{ ORDER : places
    ORDER ||--|{ DETORD : contains
    DETORD }o--|| ARTICLE : references
    ARTICLE }o--|| FAMILLY : belongs_to
    ARTICLE }o--o{ ARTIPROV : has
    ARTIPROV }o--|| PROVIDER : links
    CUSTOMER }o--|| COUNTRY : located_in

    CUSTOMER { decimal CUSNUM PK; string CUSNAM; string CUSCOU FK }
    ORDER     { decimal ORDNUM PK; decimal ORDCUS FK; string ORDSTA }
    DETORD    { decimal DETORD PK_FK; string DETART FK; decimal DETQTY }
    ARTICLE   { string ARTNUM PK; decimal ARTPRI; string ARTFAM FK }
    FAMILLY   { string FAMCOD PK; decimal FAMVAT }
```

---

## Order Creation Workflow

[⬆ Back to Overview](#overview) | [⬆ Business Logic Layer](#business-logic-layer-detail)

```mermaid
flowchart TD
    Start([User Selects Order Entry]) --> Menu[SAMMNU Menu]
    Menu --> ORD100[ORD100: Order List]
    ORD100 --> Choice{Create New\nor Maintain?}

    Choice -->|Create New| ORD101[ORD101: Order Header Entry]
    Choice -->|Maintain|   ORD200[ORD200: Order Maintenance]

    ORD101 --> ValidCust{Validate Customer}
    ValidCust -->|Invalid| CustError[Display Error] --> ORD101
    ValidCust -->|Valid|   GenOrdNum[Generate Order Number]

    GenOrdNum --> CreateHeader[Create ORDER Record]
    CreateHeader --> ORD202[ORD202: Order Line Entry]

    ORD202 --> ValidArt{Validate Article}
    ValidArt -->|Invalid| ArtError[Display Error] --> ORD202
    ValidArt -->|Valid|   CheckQty{Check Quantity}

    CheckQty -->|Insufficient| QtyError[Display Warning] --> ORD202
    CheckQty -->|Sufficient|   CalcLine[Calculate Line Amount]

    CalcLine --> CalcVAT[Calculate VAT] --> AddLine[Add DETORD Record]
    AddLine --> MoreLines{Add More Lines?}
    MoreLines -->|Yes| ORD202
    MoreLines -->|No|  CalcTotal[Calculate Order Total]

    CalcTotal --> UpdateHeader[Update ORDER with Totals]
    UpdateHeader --> Commit{Commit Transaction?}
    Commit -->|Yes| CommitTrans[Commit Changes]
    Commit -->|No|  Rollback[Rollback Changes]

    CommitTrans --> Print{Print Confirmation?}
    Print -->|Yes| ORD500[ORD500: Print Order] --> End([End])
    Print -->|No|  End
    Rollback --> End

    ORD200 --> ORD201[ORD201: Header Maintenance] --> ORD202

    style Start fill:#4caf50
    style End fill:#f44336
    style ValidCust fill:#ff9800
    style ValidArt fill:#ff9800
    style CheckQty fill:#ff9800
    style Commit fill:#2196f3
```

---

## Service Program Architecture

[⬆ Back to Overview](#overview) | [⬆ Business Logic Layer](#business-logic-layer-detail)

```mermaid
graph LR
    subgraph Programs["Interactive Programs"]
        ART200[ART200]
        CUS200[CUS200]
        ORD200[ORD200]
        PRO200[PRO200]
    end

    subgraph ServicePrograms["Service Programs"]
        FARTICLE[FARTICLE<br/>Article Functions]
        FCUSTOMER[FCUSTOMER<br/>Customer Functions]
        FCOUNTRY[FCOUNTRY<br/>Country Functions]
        FPROVIDER[FPROVIDER<br/>Provider Functions]
        LOG[LOG<br/>Logging Functions]
    end

    subgraph Modules["Service Program Modules"]
        ART300[ART300<br/>Article CRUD]
        ART301[ART301<br/>Article SQL]
        CUS300[CUS300<br/>Customer CRUD]
        PRO300[PRO300<br/>Provider CRUD]
        LOG300[LOG300<br/>Log Writer]
    end

    subgraph Database["Database Files"]
        ARTICLE[(ARTICLE)]
        CUSTOMER[(CUSTOMER)]
        PROVIDER[(PROVIDER)]
        COUNTRY[(COUNTRY)]
    end

    ART200 --> FARTICLE
    CUS200 --> FCUSTOMER
    ORD200 --> FARTICLE
    ORD200 --> FCUSTOMER
    PRO200 --> FPROVIDER

    FARTICLE --> ART300 & ART301 & LOG
    FCUSTOMER --> CUS300 & LOG
    FPROVIDER --> PRO300 & LOG
    LOG --> LOG300

    ART300 & ART301 --> ARTICLE
    CUS300 --> CUSTOMER
    PRO300 --> PROVIDER
    FCOUNTRY --> COUNTRY

    style Programs fill:#e3f2fd
    style ServicePrograms fill:#fff3e0
    style Modules fill:#f3e5f5
    style Database fill:#e8f5e9
```
