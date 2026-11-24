# Tabelle: `building`

!!! info "Abweichender Name in der Weboberfläche (GUI)"
    Im PostgreSQL-Backend heißt diese Tabelle `building`, wie im Seitentitel angegeben. In der Oberfläche der Webanwendung erscheint sie als **Built environment**. Alle Aliasnamen finden Sie in der [Zuordnungstabelle](../backend-to-gui.md).

!!! warning "KI-gestützte Übersetzung"
    Diese Seite wurde mit Unterstützung künstlicher Intelligenz übersetzt und kann Fehler enthalten. Maßgeblich ist die englische Version. Die Namen der Tabellen und Attribute sind in allen Sprachen identisch, da sie der PostgreSQL-Implementierung entsprechen.

**Beschreibung (DE):** Diese Tabelle stellt Gebäude dar. In der Vererbungsarchitektur der Datenbank fungiert sie als direkter Untertyp der Tabelle [`enterprise`](enterprise.md). Sie speichert keine redundanten beschreibenden Spalten: Stattdessen nutzt sie einen gemeinsamen Primärschlüssel, um alle übergeordneten Attribute (wie Name, Lage, Verwaltungsform und Geometrie) von ihrem übergeordneten Datensatz `enterprise` zu erben.

Die baulichen, wirtschaftlichen und physischen Merkmale eines Gebäudes (Baujahr, Materialien, Anzahl der Geschosse, Kosten usw.) sind in der Tabelle [`building_component`](building_component.md) gespeichert.

## Spaltenstruktur

| Spalte | Datentyp | Definition | Beispielwert | Einschränkung? | Geometrie? | Kommentare |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Eindeutige Kennung des Gebäudes | `3` | PK, FK | Nein | Primärschlüssel, der zugleich als Fremdschlüssel auf `enterprise.id` verweist |

## Beziehungen

* **Erbt von (Untertyp von):** [`enterprise`](enterprise.md). Die Tabelle `building` ist eine spezialisierte Erweiterung der Tabelle `enterprise`.
* **Enthält:** Obwohl es nicht direkt über `building_id` verknüpft ist, besitzt ein Gebäude seine physischen Teile über die Spalte `enterprise_id` in der Tabelle `component`. Zu diesen Komponenten gehören häufig spezialisierte Untertypen, zum Beispiel:
    * [`building_component`](building_component.md)
    * [`added_block`](added_block.md)
    * [`building_functionality`](building_functionality.md)

!!! tip "Wo befinden sich die übrigen Daten?"
    Um den Namen, den geografischen Standort (`geometry`, `town`, `country`) oder die Umsatzsteuer-Identifikationsnummer eines Gebäudes zu ermitteln, müssen Sie diese Tabelle mit dem Datensatz `enterprise` verknüpfen, der dieselbe `id` besitzt. Die baulichen und wirtschaftlichen Merkmale befinden sich in `building_component`, die über `component.enterprise_id` mit dem Gebäude verknüpft ist.

## Beispielabfrage

Rufen Sie die Merkmale jedes Gebäudes ab, indem Sie dessen Unternehmensdatensatz mit seinen Gebäudekomponenten verknüpfen:

```sql
SELECT
    e.name,
    e.town,
    bc.n_floors,
    bc.construction_cost,
    bc.economic_value
FROM
    building b
JOIN
    enterprise e ON b.id = e.id
JOIN
    component c ON c.enterprise_id = e.id
JOIN
    building_component bc ON bc.id = c.id
WHERE
    e.type = 'BUILDING';
```
