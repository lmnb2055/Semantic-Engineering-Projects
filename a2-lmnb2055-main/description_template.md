# Description

## Scope and purpose

I'm mapping out “the SILS domain” for the purpose of keeping organized
SILS-related resources such as the SILS website and intranet.

## Information source

My source of information is the SILS website.

## Graph-structured description of entities and relations

```mermaid
flowchart TD
    %% Entities
    
    RS(Ryan Shaw)
    MF(Melanie Feinberg)

    BAMTL(B.A. in Modern Thought & Literature)
    BSSS(B.S. in Symbolic Systems)
    MIMS(Master’s in Information Management & Systems)
    PHDIS(Ph.D. in Information Science)
    PHDIMS(Ph.D. in Information Management & Systems)
    
    SU(Stanford University)
    UCB(UC Berkeley)
    UW(University of Washington)
    
    201(INLS201)
    520(INLS520)
    620(INLS620)
    777(INLS777)
    DC(Data Criticism)
    NC(NC Gazetteer)
    
    %% Relations
    
    SU -->|grants degree| BSSS
    SU -->|grants degree| BAMTL
    UCB -->|grants degree| MIMS
    UCB -->|grants degree| PHDIMS
    UW -->|grants degree| PHDIS

    BSSS -->|granted to| RS
    MIMS -->|granted to| RS
    PHDIMS -->|granted to| RS
    BAMTL -->|granted to| MF
    MIMS -->|granted to| MF
    PHDIS -->|granted to| MF
    
    RS -->|has taught| 620
    RS -->|has taught| NC
    RS -->|has taught| 201
    RS -->|has taught| 520

    MF -->|has taught| 201
    MF -->|has taught| 520
    MF -->|has taught| 777
    MF -->|has taught| DC

```

## Questions this graph can answer

* *Q:* Who has a degree from the University of Washington?

  *A:* Melanie

* *Q:* Which courses have Ryan and Melanie both taught?

  *A:* INLS201 & INLS520
