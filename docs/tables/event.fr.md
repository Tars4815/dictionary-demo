# Table : `event`

!!! warning "Traduction assistée par IA"
    Cette page a été traduite avec l'assistance de l'intelligence artificielle et peut contenir des erreurs. La version anglaise fait foi. Les noms des tables et des attributs sont identiques dans toutes les langues car ils correspondent à ceux de l'implémentation PostgreSQL.

**Description (FR) :** Cette table stocke les informations et les détails relatifs à un événement majeur précis.

## Structure des colonnes

| Colonne | Type de données | Définition | Exemple de valeur | Contrainte ? | Géométrie ? | Commentaires |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Identifiant unique de l'événement | `3` | PK | Non | [...] |
| `date` | TIMESTAMP | Moment de survenue de l'événement | [...] | - | Non | [...] |
| `date_end` | TIMESTAMP | Moment de fin de l'événement | [...] | - | Non | [...] |
| `parent_event_id` | BIGINT | Référence en cas d'événement multiple | [...] | FK | Non | Pointe vers l'id de l'entité [event](event.md) |
| `name` | VARCHAR | Nom de l'événement | `Storm Example` | - | Non | - |
| `severity` | VARCHAR | Niveau de gravité de l'événement | [...] | - | Non | - |
| `type` | VARCHAR | Type de l'événement | [...] | - | Non | - |
| `country` | VARCHAR | Pays où se situe l'événement | `Italy` | - | Non | - |
| `state` | VARCHAR | État ou région où se situe l'événement | `Lazio` | - | Non | - |
| `county` | VARCHAR | Comté ou province où se situe l'événement | `Rome` | - | Non | - |
| `town` | VARCHAR | Commune où se situe l'événement | `Rome` | - | Non | - |
| `hamlet` | VARCHAR | Hameau ou lieu-dit où se situe l'événement | `Trastevere` | - | Non | - |
| `road` | VARCHAR | Rue où se situe l'événement | `Via Appia` | - | Non | - |
| `house_number` | VARCHAR | Numéro de voie de l'événement | `10` | - | Non | - |
| `postcode` | VARCHAR | Code postal de l'événement | `00100` | - | Non | - |
| `geometry` | GEOMETRY | Représentation spatiale de l'événement | [...] | - | Oui | - |
| `coordinates_inferred` | BOOLEAN | Indique si les coordonnées de l'événement ont été déduites plutôt que mesurées directement | [...] | - | Non | - |

## Relations

* **A plusieurs :** [`survey`](survey.md) (Un événement peut être suivi de plusieurs relevés d'évaluation des dommages)
* **Fait partie de / a pour parties :** [`event`](event.md) via `parent_event_id`. Un événement multiple peut être divisé en événements enfants qui pointent vers l'événement parent.
