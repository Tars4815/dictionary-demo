# Tabelle: `material`

!!! info "Abweichender Name in der Weboberfläche (GUI)"
    Im PostgreSQL-Backend heißt diese Tabelle `material`, wie im Seitentitel angegeben. In der Oberfläche der Webanwendung erscheint sie als **Stocks - Stored inputs**. Alle Aliasnamen finden Sie in der [Zuordnungstabelle](../backend-to-gui.md).

!!! warning "KI-gestützte Übersetzung"
    Diese Seite wurde mit Unterstützung künstlicher Intelligenz übersetzt und kann Fehler enthalten. Maßgeblich ist die englische Version. Die Namen der Tabellen und Attribute sind in allen Sprachen identisch, da sie der PostgreSQL-Implementierung entsprechen.

**Beschreibung (DE):** Diese Tabelle stellt Materialien dar. In der Vererbungsarchitektur der Datenbank fungiert sie als direkter Untertyp der Tabelle [`fixed_asset`](fixed_asset.md). Sie speichert keine redundanten beschreibenden Spalten: Stattdessen nutzt sie einen gemeinsamen Primärschlüssel, um alle übergeordneten Attribute (wie Name, Lage, Verwaltungsform und Geometrie) von ihrem übergeordneten Datensatz `component` zu erben.

## Spaltenstruktur

| Spalte | Datentyp | Definition | Beispielwert | Einschränkung? | Geometrie? | Kommentare |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Eindeutige Kennung des Materialdatensatzes | `42` | PK, FK | Nein | Primärschlüssel, der zugleich als Fremdschlüssel auf `fixed_asset.id` und seinerseits auf `component.id` verweist |
| `value` | BIGINT | [...] | [...] | - | Nein | [...] |
| `quantity` | VARCHAR | [...] | [...] | - | Nein | [...] |
| `material_type` | VARCHAR | [...] | [...] | - | Nein | [...] |
| `hazardous` | BOOLEAN | [...] | [...] | - | Nein | [...] |

## Beziehungen

* **Erbt von (Untertyp von):** [`fixed_asset`](fixed_asset.md). Die Tabelle `material` ist eine spezialisierte Erweiterung der Tabelle `fixed_asset`.
* **Gehört zu:** [`enterprise`](enterprise.md) (Ein Komponenten-Untertyp ist mit genau einem Unternehmen verknüpft)
* **Hat viele:** `damage` (Ein Komponenten-Untertyp kann im Laufe der Zeit mehrfach beschädigt werden)

!!! tip "Wo befinden sich die übrigen Daten?"
    Um den Namen, den geografischen Standort (`geometry`, `town`, `country`) oder die Eigentumsangaben eines Materialdatensatzes zu ermitteln, müssen Sie diese Tabelle mit dem Datensatz `component` verknüpfen, der dieselbe `id` besitzt.

## Beispielabfrage

Rufen Sie eine Liste aller Materialien ab, einschließlich Namen, Gemeinden und räumlicher Koordinaten, indem Sie die Tabelle mit ihrer übergeordneten Entität `component` verknüpfen:

```sql
SELECT m.* FROM public.material AS m
```