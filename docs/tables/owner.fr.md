# Table : `owner`

!!! info "Nom différent dans l'interface web (GUI)"
    Dans le backend PostgreSQL, cette table s'appelle `owner`, comme indiqué dans le titre de la page. Dans l'interface de l'application web, elle apparaît sous le nom **Owner profiles**. Tous les alias figurent dans le [tableau de correspondance](../backend-to-gui.md).

!!! warning "Traduction assistée par IA"
    Cette page a été traduite avec l'assistance de l'intelligence artificielle et peut contenir des erreurs. La version anglaise fait foi. Les noms des tables et des attributs sont identiques dans toutes les langues car ils correspondent à ceux de l'implémentation PostgreSQL.

**Description (FR) :** Cette entité stocke les attributs universels de haut niveau, comme l'identification et les coordonnées de contact, des enregistrements de propriétaires.

## Structure des colonnes

| Colonne | Type de données | Définition | Exemple de valeur | Contrainte ? | Géométrie ? | Commentaires |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Identifiant unique du propriétaire | `3` | PK | Non | - |
| `email` | VARCHAR | Adresse e-mail du propriétaire | `example@mail.com` | - | Non | - |
| `fiscal_code` | VARCHAR | Code fiscal du propriétaire | `AB0123CDEF` | - | Non | La limite de caractères et la configuration peuvent varier d'un pays à l'autre |
| `full_name` | VARCHAR | Nom complet du propriétaire | `John Doe` | - | Non | - |
| `phone` | VARCHAR | Numéro de téléphone et indicatif international du propriétaire | `+390123456789` | - | Non | - |

## Relations

* **Possède :** [`enterprise`](enterprise.md) (Un propriétaire possède une entreprise). Cette relation plusieurs-à-plusieurs est assurée par la table de liaison [`enterprise_owner`](enterprise_owner.md).

## Exemple de requête

Récupérez la liste de tous les propriétaires, en affichant leur nom et leurs coordonnées de contact :

```sql
SELECT *
FROM 
    owner o
ORDER BY 
    o.full_name ASC;
```

