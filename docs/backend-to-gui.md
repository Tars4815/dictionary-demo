# Graphic User Interface terminology

The [web-app application of AHEAD](https://ahead-impact.app/lode/) adopts aliases for the entities involved in the user form compilations. To improve understanding of the underlying connections to the database, this section includes a table mapping GUI interface terms to entity names in the PostgreSQL database, to support replicability and transparency of the system.

---

## Backend to web-app correspondence

| Entity name in the database | Website alias | 
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