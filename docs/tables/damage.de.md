# Tabelle: `damage`

!!! warning "KI-gestützte Übersetzung"
    Diese Seite wurde mit Unterstützung künstlicher Intelligenz übersetzt und kann Fehler enthalten. Maßgeblich ist die englische Version. Die Namen der Tabellen und Attribute sind in allen Sprachen identisch, da sie der PostgreSQL-Implementierung entsprechen.

**Beschreibung (DE):** Diese Tabelle speichert die universellen, übergeordneten Attribute, wie Identifikation und geografische Lage, für alle Schäden, die nach dem Eintreten eines Ereignisses auftreten. Spezifische Schadenstypen (wie [Schäden an Kunstgütern](damage_artistic_good.md), [Schäden an der Gebäudefunktionalität](damage_building_functionality.md) oder andere) speichern ihre spezialisierten Daten in separaten Untertabellen, die dieselbe ID teilen.

## Spaltenstruktur

| Spalte | Datentyp | Definition | Beispielwert | Einschränkung? | Geometrie? | Kommentare |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Eindeutige Kennung des Schadens | `3` | PK | Nein | Dient als universelle ID für alle Untertyp-Tabellen |
| `estimated_value` | BIGINT | [...] | - | - | Nein | - |
| `component_id` | BIGINT | [...] | - | FK | Nein | Verweist auf die id der Entität [component](component.md) |
| `date` | TIMESTAMP | [...] | [...] | - | Nein | - |
| `end_date` | TIMESTAMP | [...] | [...] | - | Nein | - |
| `start_end` | TIMESTAMP | [...] | [...] | - | Nein | - |
| `survey_id` | BIGINT | [...] | [...] | FK | Nein | Verweist auf die id der Entität [survey](survey.md) |
| `country` | VARCHAR | [...] | [...] | - | Nein | - |
| `county` | VARCHAR | [...] | [...] | - | Nein | - |
| `description` | VARCHAR | [...] | [...] | - | Nein | - |
| `hamlet` | VARCHAR | [...] | [...] | - | Nein | - |
| `house_number` | VARCHAR | [...] | [...] | - | Nein | - |
| `postcode` | VARCHAR | [...] | [...] | - | Nein | - |
| `road` | VARCHAR | [...] | [...] | - | Nein | - |
| `state` | VARCHAR | [...] | [...] | - | Nein | - |
| `town` | VARCHAR | [...] | [...] | - | Nein | - |
| `geometry` | GEOMETRY | Räumliche Darstellung der Schadensentität | [...] | - | Nein | - |
| `coordinates_inferred` | BOOLEAN | [...] | [...] | - | Nein | - |
| `sendai_indicator` | VARCHAR | [...] | [...] | - | Nein | - |

## Beziehungen

Da `damage` eine der zentralen Entitäten des Schemas ist, hat sie zahlreiche Beziehungen:

* **Hat Untertypen (Vererbung):** Die folgenden Tabellen erben von `damage` und teilen deren `id`:
    * [`damage_artistic_good`](damage_artistic_good.md)
    * [`damage_building_functionality`](damage_building_functionality.md)
    * [`damage_building_not_structural`](damage_building_not_structural.md)
    * [`damage_building_structural`](damage_building_structural.md)
    * [`damage_business_operations`](damage_business_operations.md)
    * [`damage_church_structure`](damage_church_structure.md)
    * [`damage_goods`](damage_goods.md)
    * [`damage_network_component`](damage_network_component.md)
    * [`damage_network_service`](damage_network_service.md)
    * [`damage_people`](damage_people.md)
    * [`damage_product`](damage_product.md)
    * [`damage_vehicles`](damage_vehicles.md)
    * [`damage_whole_structure`](damage_whole_structure.md)
    * [`farm_damage`](farm_damage.md)
* **Betrifft:** [`component`](component.md) (Ein oder mehrere Schäden betreffen eine Komponente oder ihre Unterklassen)
* **Wird erfasst durch:** [`survey`](survey.md) (Ein oder mehrere Schäden werden in einer Erhebung gemeldet)
* **Wird dokumentiert in:** [`attachment`](attachment.md) (Ein Schaden wird in einem oder mehreren Anhängen gemeldet)
* **Führt zu:** [`economic_loss`](economic_loss.md)