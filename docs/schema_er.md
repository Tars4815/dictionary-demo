# Schema overview

This diagram illustrates the core entities of our database and how they relate to one another. It highlights the main architecture, including ownership, physical components, and the recording of damage events.

```mermaid
erDiagram
    OWNER ||--o{ ENTERPRISE : owns
    ENTERPRISE ||--o{ COMPONENT : contains
    
    ENTERPRISE ||--|| BUILDING : extends_as
    ENTERPRISE ||--|| FARM : extends_as
    ENTERPRISE ||--|| NETWORK_SYSTEM : extends_as

    EVENT ||--o{ SURVEY : triggers
    ENTERPRISE ||--o{ SURVEY : undergoes
    SURVEY ||--o{ DAMAGE : records
    COMPONENT ||--o{ DAMAGE : suffers
    
    DAMAGE ||--o{ ATTACHMENT : documented_by
    DAMAGE ||--|| ECONOMIC_LOSS : quantifies

    ENTERPRISE {
        int id PK
        string type
        string name
        string geometry
    }
    BUILDING {
        int id PK
        int construction_cost
        int n_floors
    }
    FARM {
        int id PK
    }
    COMPONENT {
        int id PK
        int enterprise_id FK
        string component_category
        boolean cultural_heritage
    }
```

### Relationship Legend
* `||--o{` : **One-to-Many**. *Example: An enterprise contains many components.*
* `||--||` : **One-to-One**. *Example: The Building record is a direct extension of an Enterprise record.*
* `}o--||` : **Many-to-One**. *Example: Many enterprises can belong to a single owner.*