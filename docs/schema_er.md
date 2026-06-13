# Diagramma Entità-Relazione

```mermaid
erDiagram
    USERS ||--o{ LOCATIONS : "crea"
    USERS {
        uuid id PK
        string username
    }
    LOCATIONS {
        uuid id PK
        uuid user_id FK
        point geom
        string name
    }
```