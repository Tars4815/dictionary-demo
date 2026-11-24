# Guide de contribution

!!! warning "Traduction assistée par IA"
    Cette page a été traduite avec l'assistance de l'intelligence artificielle et peut contenir des erreurs. La version anglaise fait foi. Les noms des tables et des attributs sont identiques dans toutes les langues car ils correspondent à ceux de l'implémentation PostgreSQL.

Merci de nous aider à maintenir le dictionnaire de données exact et à jour ! 

Une bonne documentation est un travail d'équipe. Vous n'avez pas besoin d'être développeur, de savoir programmer ni de connaître Git pour contribuer à ce projet. Toutes les mises à jour de contenu sont gérées à l'aide d'un simple tableur.

---

## Le flux de travail

La mise à jour du dictionnaire ne demande que trois étapes simples :

1. **Télécharger le modèle :** Récupérez la dernière version du modèle Excel du dictionnaire de données dans notre dossier d'équipe partagé.
2. **Renseigner les données :** Ajoutez ou mettez à jour les lignes correspondant aux tables et aux colonnes de la base de données que vous documentez.
3. **Soumettre pour publication :** Envoyez le fichier Excel mis à jour à l'équipe technique. Nous lancerons un processus automatisé pour convertir votre tableur en pages web, comme celles que vous voyez ici.

---

## Comment remplir le modèle Excel

Chaque feuille du fichier Excel représente une seule table de la base de données. Pour chaque colonne de cette table, veuillez fournir les informations suivantes :

* **Column:** Le nom technique exact du champ dans la base de données (p. ex. `user_id`, `geom`, `created_at`).
* **Data type:** Le format de la donnée (p. ex. `VARCHAR(255)`, `UUID`, `POINT`, `INTEGER`).
* **Definition (IT) & Definition (EN):** Une description claire, compréhensible aussi par des non-spécialistes, de ce que représente la colonne. Veuillez remplir à la fois la colonne italienne et la colonne anglaise, afin de soutenir notre plateforme bilingue.
* **Example value:** Un exemple réaliste de la donnée pour aider les autres à comprendre son format (p. ex. `john.doe@email.com` ou `POINT(12.49 41.89)`).
* **Constraint?:** Indiquez les éventuelles règles de la base de données, comme `PK` (clé primaire), `FK` (clé étrangère) ou `NOT NULL`.
* **Geometry?:** Précisez si le champ contient des données spatiales (p. ex. `Yes - EPSG:4326` ou `No`).
* **Comments (IT) & Comments (EN):** Tout contexte supplémentaire, règle métier ou avertissement sur la façon d'utiliser ou d'interpréter cette donnée.

!!! warning "Gardez une mise en forme simple"
    Veuillez éviter les mises en forme Excel complexes, comme les cellules fusionnées, les couleurs de cellule personnalisées ou les retours à la ligne multiples dans une même cellule. Un texte brut garantit la conversion la plus fluide vers la plateforme web !

---

## Soumettre vos modifications

Une fois votre fichier Excel prêt et relu :

* Téléversez la nouvelle version sur le lecteur partagé désigné.
* Informez l'équipe d'administration de la base de données par e-mail ou via notre messagerie interne.
* L'équipe traitera le fichier et vos modifications seront en ligne dans le dictionnaire de données en quelques minutes !