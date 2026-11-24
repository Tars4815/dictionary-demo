# Tabelle: `livestock`

!!! warning "KI-gestützte Übersetzung"
    Diese Seite wurde mit Unterstützung künstlicher Intelligenz übersetzt und kann Fehler enthalten. Maßgeblich ist die englische Version. Die Namen der Tabellen und Attribute sind in allen Sprachen identisch, da sie der PostgreSQL-Implementierung entsprechen.

**Beschreibung (DE):** Diese Tabelle stellt Komponenten vom Typ Viehbestand dar. In der Vererbungsarchitektur der Datenbank fungiert sie als direkter Untertyp der Tabelle [`component`](component.md). Sie speichert keine redundanten beschreibenden Spalten: Stattdessen nutzt sie einen gemeinsamen Primärschlüssel, um alle übergeordneten Attribute (wie Name, Lage, Verwaltungsform und Geometrie) von ihrem übergeordneten Datensatz `component` zu erben.

## Spaltenstruktur

| Spalte | Datentyp | Definition | Beispielwert | Einschränkung? | Geometrie? | Kommentare |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Eindeutige Kennung des Viehbestands | `42` | PK, FK | Nein | Primärschlüssel, der zugleich als Fremdschlüssel auf `component.id` verweist |
| `age` | BIGINT | [...] | `2` | - | Nein | - |
| `breeding_cost` | BIGINT | [...] | `2` | - | Nein | - |
| `gate_price` | BIGINT | [...] | `2` | - | Nein | - |
| `weight` | BIGINT | [...] | `2` | - | Nein | - |
| `year_production` | BIGINT | [...] | `2` | - | Nein | - |
| `subtype` | VARCHAR | [...] | - | - | Nein | - |
| `purpose` | VARCHAR | [...] | - | - | Nein | - |

## Beziehungen

* **Erbt von (Untertyp von):** [`component`](component.md). Die Tabelle `livestock` ist eine spezialisierte Erweiterung der Tabelle `component`.
* **Gehört zu:** [`enterprise`](enterprise.md) (Ein Komponenten-Untertyp ist mit genau einem Unternehmen verknüpft)
* **Hat viele:** `damage` (Ein Komponenten-Untertyp kann im Laufe der Zeit mehrfach beschädigt werden)

!!! tip "Wo befinden sich die übrigen Daten?"
    Um den Namen, den geografischen Standort (`geometry`, `town`, `country`) oder die Eigentumsangaben eines Nutztiers zu ermitteln, müssen Sie diese Tabelle mit dem Datensatz `component` verknüpfen, der dieselbe `id` besitzt.

## Beispielabfrage

Rufen Sie eine Liste aller Viehbestandsdatensätze ab, einschließlich Namen, Gemeinden und räumlicher Koordinaten, indem Sie die Tabelle mit ihrer übergeordneten Entität `component` verknüpfen:

```sql
SELECT 
    l.id, 
    c.name, 
    c.town, 
    ST_AsText(c.geometry) as coordinates 
FROM 
    livestock l
JOIN 
    component c ON l.id = c.id
WHERE 
    c.component_kind  = 'LIVESTOCK';
```