# Tabelle: `tlc_system`

!!! warning "KI-gestützte Übersetzung"
    Diese Seite wurde mit Unterstützung künstlicher Intelligenz übersetzt und kann Fehler enthalten. Maßgeblich ist die englische Version. Die Namen der Tabellen und Attribute sind in allen Sprachen identisch, da sie der PostgreSQL-Implementierung entsprechen.

**Beschreibung (DE):** Diese Tabelle stellt Telekommunikationsnetzsysteme dar. In der Vererbungsarchitektur der Datenbank fungiert sie als direkter Untertyp der Tabelle [`network_system`](network_system.md). Sie speichert keine redundanten beschreibenden Spalten: Stattdessen nutzt sie einen gemeinsamen Primärschlüssel, um alle übergeordneten Attribute (wie Name, Lage, Verwaltungsform und Geometrie) von ihrem übergeordneten Datensatz `network_system` zu erben, der seinerseits ein Kind eines Datensatzes [`enterprise`](enterprise.md) ist.

## Spaltenstruktur

| Spalte | Datentyp | Definition | Beispielwert | Einschränkung? | Geometrie? | Kommentare |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Eindeutige Kennung des Telekommunikationsnetzsystems | `8` | PK, FK | Nein | Primärschlüssel, der zugleich als Fremdschlüssel auf `network_system.id` und `enterprise.id` verweist |

## Beziehungen

* **Erbt von (Untertyp von):** [`network_system`](network_system.md). Die Tabelle `tlc_system` ist eine spezialisierte Erweiterung der Tabelle `network_system`.
* **Enthält:** Obwohl es nicht direkt über `tlc_system_id` verknüpft ist, besitzt ein Telekommunikationssystem Infrastrukturgüter über die Spalte `enterprise_id` in der Tabelle `component`. Zu diesen Komponenten gehören häufig spezialisierte Untertypen, zum Beispiel:
    * `tlc_network_component`

!!! tip "Wo befinden sich die übrigen Daten?"
    Um den Namen, den geografischen Standort (`geometry`, `town`, `country`) oder die Eigentumsangaben eines Netzsystems zu ermitteln, müssen Sie diese Tabelle mit dem Datensatz `enterprise` verknüpfen, der dieselbe `id` besitzt.

## Beispielabfrage

Rufen Sie eine Liste aller Stromsysteme ab, einschließlich Namen, Gemeinden und räumlicher Koordinaten, indem Sie die Tabelle mit ihrer übergeordneten Entität `network_system` - `enterprise` verknüpfen:

```sql
SELECT 
    tlc.id, 
    e.name, 
    e.town, 
    ST_AsText(e.geometry) as coordinates 
FROM 
    tlc_system tlc
JOIN 
    enterprise e ON tlc.id = e.id
WHERE 
    e.type = 'TLC_SYSTEM';