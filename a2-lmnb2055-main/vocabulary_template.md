# Vocabulary

## Class definitions

| Class | Description |
| ----- | ----------- |
| Employee | A person who has been hired by UNC SILS |
| Staff | A person who has held a staff position at UNC SILS. Sub-class of Employee |
| Faculty Member | A person who has taught at least one course at UNC SILS. Sub-class of Employee |
| Degree | An academic qualification conferred by college or university |
| University | A degree-granting institution |
| Course | A course that has been taught at UNC SILS |

## Property definitions

| Property | Description |
| -------- | ----------- |
| grants degree | relates a University to a Degree that it grants |
| granted to | relates a Degree to a Faculty Member who has it |
| has taught | relates a Faculty Member to a course they have taught |

## Graph-structured description of classes and properties

```mermaid
flowchart TD
    %% Classes

    E(Employee)
    S(Staff)
    FM(Faculty Member)
    D(Degree)
    U(University)
    C(Course)
    
    %% Properties
    
    GD(grants degree)
    GT(granted to)
    HT(has taught)
    
    %% Property domains and ranges
    
    GD -->|domain| U
    GD -->|range| D
    GT -->|domain| D
    GT -->|range| E
    HT -->|domain| FM
    HT -->|range| C

    %% Sub-class relations
    
    S -->|sub-class of| E
    FM -->|sub-class of| E
```

## Questions this graph can answer

* *Q:* Which Faculty Members have a degree from which Universities?
* *Q:* Which Courses have been taught by which Faculty Members?
