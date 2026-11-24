# Terminologie de l'interface utilisateur graphique (GUI)

!!! warning "Traduction assistée par IA"
    Cette page a été traduite avec l'assistance de l'intelligence artificielle et peut contenir des erreurs. La version anglaise fait foi. Les noms des tables et des attributs sont identiques dans toutes les langues car ils correspondent à ceux de l'implémentation PostgreSQL.

L'[application web de AHEAD](https://ahead-impact.app/lode/) utilise des alias pour les entités concernées par la saisie des formulaires par les utilisateurs. Pour faciliter la compréhension des liens sous-jacents avec la base de données, cette section comprend un tableau qui associe les termes de l'interface graphique aux noms des entités de la base de données PostgreSQL, afin de favoriser la reproductibilité et la transparence du système.

---

## Correspondance entre le backend et l'application web

| Nom de l'entité dans la base de données | Alias sur le site web |
| :--- | :--- | 
| `building` | Built environment | 
| `business` | Economic Activities - Business |
| `farm` | Economic Activities - Farm |  
| `electrical_system` | Lifelines - Electrical |
| `transport_system` | Lifelines - Transport |
| `tlc_system` | Lifelines - Telecommunication |
| `owner` | Owner profiles |
| `component` | Elements & production (all subclasses) |
| `added_block` | Added block |
| `building_component` | Principal structure |
| `fixed_asset` | Elements |
| `material` | Stocks - Stored inputs |
| `network_service` | Telecom service/Electrical service/Transport service |
| `transport_network_component` | Transport element |
| `tlc_network_component` | Telecom element |