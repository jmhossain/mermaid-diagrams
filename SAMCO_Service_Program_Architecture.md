# SAMCO Service Program Architecture

> Nested subgraph view of the four layers: Interactive Programs → Service Programs → Modules → Database Files.

```mermaid
graph LR
    subgraph Tier1["① Interactive Programs"]
        subgraph Programs["Programs"]
            ART200[ART200]
            CUS200[CUS200]
            ORD200[ORD200]
            PRO200[PRO200]
        end
    end

    subgraph Tier2["② Service Programs"]
        subgraph ServicePrograms["Service Programs"]
            FARTICLE[FARTICLE<br/>Article Functions]
            FCUSTOMER[FCUSTOMER<br/>Customer Functions]
            FCOUNTRY[FCOUNTRY<br/>Country Functions]
            FPROVIDER[FPROVIDER<br/>Provider Functions]
            LOG[LOG<br/>Logging Functions]
        end
    end

    subgraph Tier3["③ Service Program Modules"]
        subgraph Modules["Modules"]
            ART300[ART300<br/>Article CRUD]
            ART301[ART301<br/>Article SQL]
            CUS300[CUS300<br/>Customer CRUD]
            PRO300[PRO300<br/>Provider CRUD]
            LOG300[LOG300<br/>Log Writer]
        end
    end

    subgraph Tier4["④ Database Files"]
        subgraph Database["Database"]
            ARTICLE[(ARTICLE)]
            CUSTOMER[(CUSTOMER)]
            PROVIDER[(PROVIDER)]
            COUNTRY[(COUNTRY)]
        end
    end

    %% Programs → Service Programs
    ART200 --> FARTICLE
    CUS200 --> FCUSTOMER
    ORD200 --> FARTICLE
    ORD200 --> FCUSTOMER
    PRO200 --> FPROVIDER

    %% Service Programs → Modules
    FARTICLE --> ART300 & ART301 & LOG
    FCUSTOMER --> CUS300 & LOG
    FPROVIDER --> PRO300 & LOG
    LOG --> LOG300

    %% Modules → Database Files
    ART300 & ART301 --> ARTICLE
    CUS300 --> CUSTOMER
    PRO300 --> PROVIDER
    FCOUNTRY --> COUNTRY

    %% Tier styles
    style Tier1 fill:#e3f2fd,stroke:#1565c0,stroke-width:2px
    style Tier2 fill:#fff3e0,stroke:#e65100,stroke-width:2px
    style Tier3 fill:#f3e5f5,stroke:#6a1b9a,stroke-width:2px
    style Tier4 fill:#e8f5e9,stroke:#1b5e20,stroke-width:2px

    %% Inner subgraph styles
    style Programs fill:#bbdefb,stroke:#1565c0
    style ServicePrograms fill:#ffe0b2,stroke:#e65100
    style Modules fill:#e1bee7,stroke:#6a1b9a
    style Database fill:#c8e6c9,stroke:#1b5e20
```

---

| Tier | Contents | Responsibility |
|------|----------|----------------|
| **① Interactive Programs** | ART200, CUS200, ORD200, PRO200 | Screen-driven entry points called from menus |
| **② Service Programs** | FARTICLE, FCUSTOMER, FCOUNTRY, FPROVIDER, LOG | Shared business-logic facades bound to programs at activation |
| **③ Service Program Modules** | ART300, ART301, CUS300, PRO300, LOG300 | Compiled modules packaged into each service program |
| **④ Database Files** | ARTICLE, CUSTOMER, PROVIDER, COUNTRY | Physical files accessed by the modules |
