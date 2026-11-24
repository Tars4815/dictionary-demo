# Table : `attachment`

!!! warning "Traduction assistée par IA"
    Cette page a été traduite avec l'assistance de l'intelligence artificielle et peut contenir des erreurs. La version anglaise fait foi. Les noms des tables et des attributs sont identiques dans toutes les langues car ils correspondent à ceux de l'implémentation PostgreSQL.

**Description (FR) :** Cette table stocke les informations et les détails relatifs à une pièce jointe.

## Structure des colonnes

| Colonne | Type de données | Définition | Exemple de valeur | Contrainte ? | Géométrie ? | Commentaires |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Identifiant unique de la pièce jointe | `3` | PK | Non | [...] |
| `damage_id` | BIGINT | Clé étrangère faisant référence à un dommage signalé | [...] | FK | Non | Pointe vers l'id de l'entité [damage](damage.md) |
| `date` | TIMESTAMP | [...] | - | - | Non | - |
| `size` | BIGINT | [...] | - | - | Non | - |
| `description` | VARCHAR | [...] | - | - | Non | - |
| `name` | VARCHAR | [...] | - | - | Non | - |
| `type` | VARCHAR | [...] | - | - | Non | - |
| `data` | BIGINT | [...] | - | - | Non | - |

## Relations

* **Documents** [`damage`](damage.md)