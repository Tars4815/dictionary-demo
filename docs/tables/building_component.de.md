# Tabelle: `building_component`

!!! info "Abweichender Name in der Weboberfläche (GUI)"
    Im PostgreSQL-Backend heißt diese Tabelle `building_component`, wie im Seitentitel angegeben. In der Oberfläche der Webanwendung erscheint sie als **Principal structure**. Alle Aliasnamen finden Sie in der [Zuordnungstabelle](../backend-to-gui.md).

!!! warning "KI-gestützte Übersetzung"
    Diese Seite wurde mit Unterstützung künstlicher Intelligenz übersetzt und kann Fehler enthalten. Maßgeblich ist die englische Version. Die Namen der Tabellen und Attribute sind in allen Sprachen identisch, da sie der PostgreSQL-Implementierung entsprechen.

**Beschreibung (DE):** Diese Tabelle speichert die baulichen, wirtschaftlichen und physischen Merkmale von Gebäuden, einschließlich Konstruktionsdetails, Materialarten und Abmessungen. In der Vererbungsarchitektur der Datenbank fungiert sie als direkter Untertyp der Tabelle [`component`](component.md). Sie speichert keine redundanten beschreibenden Spalten: Stattdessen nutzt sie einen gemeinsamen Primärschlüssel, um alle übergeordneten Attribute (wie Name, Lage und Geometrie) von ihrem übergeordneten Datensatz `component` zu erben.

## Spaltenstruktur

| Spalte | Datentyp | Definition | Beispielwert | Einschränkung? | Geometrie? | Kommentare |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Eindeutige Kennung der Gebäudekomponente | `42` | PK, FK | Nein | Primärschlüssel, der zugleich als Fremdschlüssel auf `component.id` verweist |
| `principal` | BOOLEAN | Gibt an, ob es sich um die Hauptgebäudekomponente handelt | `true` | - | Nein | [...] |
| `subtype` | VARCHAR(255) | [...] | [...] | - | Nein | [...] |
| `public_service_code` | VARCHAR(255) | [...] | [...] | - | Nein | [...] |
| `heritage_tier` | VARCHAR(255) | [...] | [...] | - | Nein | [...] |
| `year` | INTEGER | Baujahr | `1999` | - | Nein |  |
| `quality` | VARCHAR(255) | Gesamtqualität | `GOOD` | - | Nein | Mögliche Werte: POOR, GOOD, ACCEPTABLE, NOT_IDENTIFIABLE |
| `conservation` | VARCHAR(255) | Erhaltungszustand des Gebäudes | `POORLY_MANTAINED` | CHECK | Nein | Mögliche Werte: POORLY_MANTAINED, MODERATELY_MAINTAINED, WELL_MAINTAINED, NOT_IDENTIFIABLE |
| `retrofitting` | VARCHAR(255) | Stand der nachträglichen Ertüchtigung (Retrofitting) | `NOT_IDENTIFIABLE` | CHECK | Nein | Mögliche Werte: NONE, VERTICAL, HORIZONTAL, COMPLETE, NOT_IDENTIFIABLE usw. |
| `regularity` | VARCHAR(255) | Regelmäßigkeit der Struktur | `NOT_IDENTIFIABLE` | CHECK | Nein | Mögliche Werte: NOT_REGULAR, COMPLETELY_REGULAR usw. |
| `inhabitants` | INTEGER | Anzahl der Bewohner des betreffenden Gebäudes | `6` | - | Nein |  |
| `construction_cost` | INTEGER | Baukosten | `500000` | - | Nein |  |
| `economic_value` | INTEGER | Wirtschaftlicher Wert | `1000000` | - | Nein |  |
| `vertical_mat` | VARCHAR(255) | Baumaterial der vertikalen Strukturen | `NOT_IDENTIFIABLE` | CHECK | Nein | Mögliche Werte: STEEL, WOOD, MASONRY_ADOBE usw. |
| `horizontal_mat` | VARCHAR(255) | Baumaterial der horizontalen Strukturen | `MASONRY_ADOBE` | CHECK | Nein | Mögliche Werte: STEEL, WOOD, MASONRY_ADOBE usw. |
| `roof_mat` | VARCHAR(255) | Material des Dachelements | `NOT_IDENTIFIABLE` | CHECK | Nein | Mögliche Werte: STEEL, WOOD, MASONRY_ADOBE usw. |
| `build_position` | VARCHAR(255) | Lage des Gebäudes | `SINGLE_DETACHED` | CHECK | Nein | Mögliche Werte: SINGLE_DETACHED, SEMI_DETACHED, ROW, NOT_IDENTIFICABLE |
| `ground_floor` | VARCHAR(255) | Typologie des Erdgeschosses | `OPEN` | CHECK | Nein | Mögliche Werte: OPEN, CLOSE, NOT_IDENTIFIABLE |
| `n_floors` | INTEGER | Anzahl der oberirdischen Geschosse | `3` | - | Nein |  |
| `floor_height` | INTEGER | Durchschnittliche Geschosshöhe | `4` | - | Nein |  |
| `n_under_floors` | INTEGER | Anzahl der unterirdischen Geschosse | `1` | - | Nein |  |
| `floor_area` | INTEGER | Geschossfläche in Quadratmetern | `1000` | - | Nein |  |
| `usage` | VARCHAR(255) | [...] | [...] | - | Nein | [...] |
| `foundation_typology` | VARCHAR(255) | Typologie der Fundamente | [...] | - | Nein | [...] |
| `main_use` | VARCHAR(255) | Hauptnutzung des Gebäudes | [...] | - | Nein | [...] |

## Beziehungen

* **Erbt von (Untertyp von):** [`component`](component.md). Die Tabelle `building_component` ist eine spezialisierte Erweiterung der Tabelle `component`.
* **Gehört zu:** [`enterprise`](enterprise.md) (Ein Komponenten-Untertyp ist mit genau einem Unternehmen verknüpft)
* **Hat viele:** `damage` (Ein Komponenten-Untertyp kann im Laufe der Zeit mehrfach beschädigt werden)

!!! tip "Wo befinden sich die übrigen Daten?"
    Um den Namen, den geografischen Standort (`geometry`, `town`, `country`) oder die Eigentumsangaben einer Gebäudekomponente zu ermitteln, müssen Sie diese Tabelle mit dem Datensatz `component` verknüpfen, der dieselbe `id` besitzt.

## Beispielabfrage

Rufen Sie eine Liste aller Gebäudekomponenten ab, einschließlich Namen, Gemeinden und räumlicher Koordinaten, indem Sie die Tabelle mit ihrer übergeordneten Entität `component` verknüpfen:

```sql
SELECT 
    bc.id, 
    c.name, 
    c.town, 
    ST_AsText(c.geometry) as coordinates 
FROM 
    building_component bc
JOIN 
    component c ON bc.id = c.id
WHERE 
    c.component_kind = 'BUILDING_COMPONENT';
```
