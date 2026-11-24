# Terminologia dell'interfaccia grafica utente (GUI)

!!! warning "Traduzione assistita dall'IA"
    Questa pagina è stata tradotta con l'assistenza dell'intelligenza artificiale e può contenere imprecisioni. La versione inglese è il riferimento. I nomi delle tabelle e degli attributi sono identici in tutte le lingue perché corrispondono a quelli dell'implementazione PostgreSQL.

L'[applicazione web di AHEAD](https://ahead-impact.app/lode/) utilizza alias per le entità coinvolte nella compilazione dei moduli da parte degli utenti. Per facilitare la comprensione dei collegamenti sottostanti con il database, questa sezione include una tabella che associa i termini dell'interfaccia grafica ai nomi delle entità nel database PostgreSQL, a supporto della replicabilità e della trasparenza del sistema.

---

## Corrispondenza tra backend e applicazione web

| Nome dell'entità nel database | Alias nel sito web |
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