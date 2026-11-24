# Tabelle: `business`

!!! info "Abweichender Name in der Weboberfläche (GUI)"
    Im PostgreSQL-Backend heißt diese Tabelle `business`, wie im Seitentitel angegeben. In der Oberfläche der Webanwendung erscheint sie als **Economic Activities - Business**. Alle Aliasnamen finden Sie in der [Zuordnungstabelle](../backend-to-gui.md).

!!! warning "KI-gestützte Übersetzung"
    Diese Seite wurde mit Unterstützung künstlicher Intelligenz übersetzt und kann Fehler enthalten. Maßgeblich ist die englische Version. Die Namen der Tabellen und Attribute sind in allen Sprachen identisch, da sie der PostgreSQL-Implementierung entsprechen.

**Beschreibung (DE):** Diese Tabelle stellt Gewerbebetriebe dar. In der Vererbungsarchitektur der Datenbank fungiert sie als direkter Untertyp der Tabelle [`enterprise`](enterprise.md). Sie speichert keine redundanten beschreibenden Spalten: Stattdessen nutzt sie einen gemeinsamen Primärschlüssel, um alle übergeordneten Attribute (wie Name, Lage, Verwaltungsform und Geometrie) von ihrem übergeordneten Datensatz `enterprise` zu erben.

## Spaltenstruktur

| Spalte | Datentyp | Definition | Beispielwert | Einschränkung? | Geometrie? | Kommentare |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Eindeutige Kennung des Gewerbebetriebs-Datensatzes | `8` | PK, FK | Nein | Primärschlüssel, der zugleich als Fremdschlüssel auf `enterprise.id` verweist |
| `share_capital` | BIGINT | Gesamter Geldwert der Mittel des Unternehmens | [...] | - | Nein | [...] |
| `nace_section` | VARCHAR | Klassifizierung der obersten Ebene für die wirtschaftliche Haupttätigkeit des Gewerbebetriebs nach dem Standard NACE | [...] | - | Nein | [...] |

## Beziehungen

* **Erbt von (Untertyp von):** [`enterprise`](enterprise.md). Die Tabelle `business` ist eine spezialisierte Erweiterung der Tabelle `enterprise`.
* **Enthält:** Obwohl es nicht direkt über `business_id` verknüpft ist, besitzt ein Netzsystem Infrastrukturgüter über die Spalte `enterprise_id` in der Tabelle `component`. Zu diesen Komponenten gehören häufig spezialisierte Untertypen, zum Beispiel:
    * `business_operations`

!!! tip "Wo befinden sich die übrigen Daten?"
    Um den Namen, den geografischen Standort (`geometry`, `town`, `country`) oder die Eigentumsangaben eines Netzsystems zu ermitteln, müssen Sie diese Tabelle mit dem Datensatz `enterprise` verknüpfen, der dieselbe `id` besitzt.

## Beispielabfrage

Rufen Sie eine Liste aller Gewerbebetriebs-Datensätze ab, einschließlich Namen, Gemeinden und räumlicher Koordinaten, indem Sie die Tabelle mit ihrer übergeordneten Entität `enterprise` verknüpfen:

```sql
SELECT 
    b.id, 
    e.name, 
    e.town, 
    ST_AsText(e.geometry) as coordinates 
FROM 
    business b
JOIN 
    enterprise e ON b.id = e.id
WHERE 
    e.type = 'BUSINESS';
```