# Table : `survey`

!!! warning "Traduction assistée par IA"
    Cette page a été traduite avec l'assistance de l'intelligence artificielle et peut contenir des erreurs. La version anglaise fait foi. Les noms des tables et des attributs sont identiques dans toutes les langues car ils correspondent à ceux de l'implémentation PostgreSQL.

**Description (FR) :** Cette table stocke les informations et les détails relatifs à un relevé d'évaluation des dommages précis, réalisé à la suite d'un événement majeur.

## Structure des colonnes

| Colonne | Type de données | Définition | Exemple de valeur | Contrainte ? | Géométrie ? | Commentaires |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Identifiant unique du relevé | `3` | PK | Non | [...] |
| `created_on` | TIMESTAMP | Moment de réalisation du relevé d'évaluation | [...] | NOT NULL | Non | [...] |
| `enterprise_id` | BIGINT | Clé étrangère faisant référence à une entreprise | [...] | FK | Non | Pointe vers l'id de l'entité [enterprise](enterprise.md) |
| `event_id` | BIGINT | Moment de réalisation du relevé d'évaluation | [...] | FK | Non | Pointe vers l'id de l'entité [event](event.md) |

## Relations

Comme `survey` est l'une des entités centrales du schéma, elle a de nombreuses relations :

* **Signale** [`damage`](damage.md)
* **Est lié à** [`enterprise`](enterprise.md)
* **Fait suite à un** [`event`](event.md)