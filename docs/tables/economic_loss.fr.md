# Table : `economic_loss`

!!! warning "Traduction assistée par IA"
    Cette page a été traduite avec l'assistance de l'intelligence artificielle et peut contenir des erreurs. La version anglaise fait foi. Les noms des tables et des attributs sont identiques dans toutes les langues car ils correspondent à ceux de l'implémentation PostgreSQL.

**Description (FR) :** Cette table stocke les coûts associés à un dommage signalé : les montants estimés, approuvés et définitifs.

## Structure des colonnes

| Colonne | Type de données | Définition | Exemple de valeur | Contrainte ? | Géométrie ? | Commentaires |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Identifiant unique de l'enregistrement de perte économique | `3` | PK | Non | [...] |
| `damage_id` | BIGINT | Clé étrangère faisant référence à un dommage signalé | [...] | FK | Non | Pointe vers l'id de l'entité [damage](damage.md) |
| `approved_cost` | DOUBLE PRECISION | Coût approuvé pour le dommage | - | - | Non | - |
| `estimated_cost` | DOUBLE PRECISION | Coût estimé du dommage | - | - | Non | - |
| `final_cost` | DOUBLE PRECISION | Coût définitif du dommage | - | - | Non | - |
| `type_of_cost` | VARCHAR | Type de coût | - | - | Non | - |

## Relations

* **Fait référence à :** [`damage`](damage.md) via `damage_id`. La perte économique est le résultat monétaire d'un dommage signalé.

## Exemple de requête

Récupérez les coûts enregistrés pour chaque dommage :

```sql
SELECT 
    d.id AS damage_id, 
    el.type_of_cost, 
    el.estimated_cost, 
    el.approved_cost, 
    el.final_cost 
FROM 
    economic_loss el
JOIN 
    damage d ON el.damage_id = d.id;
```
