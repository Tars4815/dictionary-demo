# Tabelle: `component`

!!! info "Abweichender Name in der Weboberfläche (GUI)"
    Im PostgreSQL-Backend heißt diese Tabelle `component`, wie im Seitentitel angegeben. In der Oberfläche der Webanwendung erscheint sie als **Elements & production (all subclasses)**. Alle Aliasnamen finden Sie in der [Zuordnungstabelle](../backend-to-gui.md).

!!! warning "KI-gestützte Übersetzung"
    Diese Seite wurde mit Unterstützung künstlicher Intelligenz übersetzt und kann Fehler enthalten. Maßgeblich ist die englische Version. Die Namen der Tabellen und Attribute sind in allen Sprachen identisch, da sie der PostgreSQL-Implementierung entsprechen.

**Beschreibung (DE):** Diese Tabelle speichert die universellen, übergeordneten Attribute, wie Identifikation und geografische Lage, für alle wichtigen physischen oder geschäftlichen Komponenten. Spezifische Komponententypen (wie [Anbauten](added_block.md), [Kunstgüter](artistic_good.md) oder andere) speichern ihre spezialisierten Daten in separaten Untertabellen, die dieselbe ID teilen.

## Spaltenstruktur

| Spalte | Datentyp | Definition | Beispielwert | Einschränkung? | Geometrie? | Kommentare |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Eindeutige Kennung der Komponente | `3` | PK | Nein | Dient als universelle ID für alle Untertyp-Tabellen |
| `component_kind` | VARCHAR | Diskriminatorspalte, die den spezifischen Untertyp der Komponente angibt | `BUILDING_COMPONENT` | NOT NULL | Nein | Enthält den spezifischsten Typ. Derzeit in den Daten vorhandene Werte: 'BUILDING_COMPONENT', 'TRANSPORT_COMPONENT', 'TRANSPORT_SERVICE', 'ADDED_BLOCK', 'CROP' |
| `enterprise_id` | BIGINT | Kennung des Unternehmens, zu dem die Komponente gehört | `42` | FK | Nein | Verweist auf die id der Entität [enterprise](enterprise.md) |
| `insured` | BOOLEAN | Gibt an, ob die Komponente versichert ist | `True` | - | Nein | - |
| `name` | VARCHAR | Name oder Bezeichnung der Komponente | `Warehouse A` | - | Nein | - |
| `country` | VARCHAR | Land, in dem sich die Komponente befindet | `Italy` | - | Nein | - |
| `state` | VARCHAR | Bundesland oder Region, in dem bzw. in der sich die Komponente befindet | `Lazio` | - | Nein | - |
| `county` | VARCHAR | Landkreis oder Provinz, in dem bzw. in der sich die Komponente befindet | `Rome` | - | Nein | - |
| `town` | VARCHAR | Gemeinde, in der sich die Komponente befindet | `Rome` | - | Nein | - |
| `hamlet` | VARCHAR | Weiler oder Ortsteil, in dem sich die Komponente befindet | `Trastevere` | - | Nein | - |
| `road` | VARCHAR | Straße, in der sich die Komponente befindet | `Via Appia` | - | Nein | - |
| `house_number` | VARCHAR | Hausnummer der Komponente | `10` | - | Nein | - |
| `postcode` | VARCHAR | Postleitzahl der Komponente | `00100` | - | Nein | - |
| `details` | VARCHAR | Zusätzliche Adressangaben zur Komponente | `Building B, second floor` | - | Nein | - |
| `geometry` | GEOMETRY | Räumliche Darstellung der Komponentenentität | [...] | - | Ja | - |
| `coordinates_inferred` | BOOLEAN | Gibt an, ob die Koordinaten der Komponente abgeleitet statt direkt gemessen wurden | [...] | - | Nein | - |
| `cultural_heritage` | BOOLEAN | Gibt an, ob die Komponente ein Kulturerbe-Objekt ist | [...] | - | Nein | - |

## Beziehungen

Da `component` eine der zentralen Entitäten des Schemas ist, hat sie zahlreiche Beziehungen:

* **Hat Untertypen (Vererbung):** Die folgenden Tabellen erben von `component` und teilen deren `id`:
    * [`added_block`](added_block.md)
    * [`artistic_good`](artistic_good.md)
    * [`agriculture_product`](agriculture_product.md), das eigene Untertypen [`crop`](crop.md) und [`stored`](stored.md) hat
    * [`building_component`](building_component.md)
    * [`building_functionality`](building_functionality.md)
    * [`business_operations`](business_operations.md)
    * [`electrical_network_component`](electrical_network_component.md)
    * [`fixed_asset`](fixed_asset.md), das eigene Untertypen [`infrastructure`](infrastructure.md), [`land`](land.md), [`machinery`](machinery.md) und [`material`](material.md) hat
    * [`livestock`](livestock.md)
    * [`network_service`](network_service.md)
    * [`product`](product.md)
    * [`provision`](provision.md)
    * [`staff`](staff.md)
    * [`tlc_network_component`](tlc_network_component.md)
    * [`transport_network_component`](transport_network_component.md)
* **Gehört zu:** [`enterprise`](enterprise.md) (Eine Komponente ist mit genau einem Unternehmen verknüpft)
* **Hat viele:** [`damage`](damage.md) (Eine Komponente kann im Laufe der Zeit mehrfach beschädigt werden)
