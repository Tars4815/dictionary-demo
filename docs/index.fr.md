# Bienvenue sur le Hub du dictionnaire de données

!!! warning "Traduction assistée par IA"
    Cette page a été traduite avec l'assistance de l'intelligence artificielle et peut contenir des erreurs. La version anglaise fait foi. Les noms des tables et des attributs sont identiques dans toutes les langues car ils correspondent à ceux de l'implémentation PostgreSQL.

Bienvenue sur la plateforme centrale de documentation de la base de données de notre projet. 

Cette plateforme est conçue pour rendre la structure de nos données transparente, accessible et facile à comprendre pour toutes les personnes impliquées dans le projet, qu'il s'agisse de développeurs, d'analystes de données ou d'experts du domaine.

---

## Nos objectifs

Les principaux objectifs de ce dictionnaire de données sont les suivants :

* **Source unique de vérité :** Fournir une référence fiable et normalisée pour toutes les entités de la base de données, leurs attributs et leurs relations.
* **Accessibilité :** Proposer une interface web simple, rapide et facile à partager. Aucune installation logicielle complexe ni aucun identifiant de base de données n'est nécessaire pour comprendre nos données.
* **Clarté et contexte :** Aller au-delà des simples « types de données ». Vous y trouverez des définitions métier, des contraintes, des exemples de valeurs et des règles spécifiques (p. ex. le traitement des données géographiques) pour chaque colonne.
* **Maintenance collaborative :** Permettre aux membres de l'équipe non techniques de garder la documentation vivante et à jour grâce à un flux de travail simplifié.

## Comment naviguer

Trouver l'information dont vous avez besoin est rapide et simple :

1. **Barre de recherche :** Utilisez la puissante barre de recherche en haut de la page. Elle parcourt instantanément les noms des tables, les définitions des colonnes et les commentaires.
2. **Schéma interactif :** Commencez par l'[aperçu du schéma (ER)](schema_er.md) pour avoir une vue d'ensemble des relations entre les différentes tables.
3. **Détail des tables :** Parcourez le menu de navigation latéral pour explorer en détail des domaines et des tables spécifiques. Chaque page propose une description exhaustive de la table sélectionnée.

## Comment contribuer

Une documentation n'est utile que si elle reste à jour. Nous avons conçu cette plateforme pour que **tout le monde puisse contribuer, sans écrire de code**.

!!! info "Mettre à jour le dictionnaire via Excel"

    Pas besoin de connaître Markdown ou Git pour donner un coup de main ! Nous gérons les mises à jour grâce à un simple **modèle Excel**. 
    
    Si vous devez définir une nouvelle table ou mettre à jour une description existante, il vous suffit de remplir un tableur contenant des colonnes comme *Data type, Definition, Example value, etc.* 
    
    L'équipe technique convertira automatiquement votre feuille Excel en ces pages web. Veuillez lire le [guide de contribution](guidelines.md) pour plus de détails.

---
*Si vous constatez des divergences ou si vous avez des questions sur des entités de données spécifiques, veuillez contacter l'équipe d'administration de la base de données.*