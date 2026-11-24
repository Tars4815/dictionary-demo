# Terminologie der grafischen Benutzeroberfläche (GUI)

!!! warning "KI-gestützte Übersetzung"
    Diese Seite wurde mit Unterstützung künstlicher Intelligenz übersetzt und kann Fehler enthalten. Maßgeblich ist die englische Version. Die Namen der Tabellen und Attribute sind in allen Sprachen identisch, da sie der PostgreSQL-Implementierung entsprechen.

Die [Webanwendung von AHEAD](https://ahead-impact.app/lode/) verwendet Aliasnamen für die Entitäten, die beim Ausfüllen der Formulare durch die Nutzenden beteiligt sind. Um die zugrunde liegenden Verbindungen zur Datenbank besser verständlich zu machen, enthält dieser Abschnitt eine Tabelle, die die Begriffe der grafischen Oberfläche den Entitätsnamen in der PostgreSQL-Datenbank zuordnet. Das unterstützt die Nachvollziehbarkeit und Transparenz des Systems.

---

## Zuordnung zwischen Backend und Webanwendung

| Entitätsname in der Datenbank | Alias auf der Website |
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