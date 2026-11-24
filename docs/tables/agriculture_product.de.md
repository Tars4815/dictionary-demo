# Tabelle: `agriculture_product`

!!! warning "KI-gestützte Übersetzung"
    Diese Seite wurde mit Unterstützung künstlicher Intelligenz übersetzt und kann Fehler enthalten. Maßgeblich ist die englische Version. Die Namen der Tabellen und Attribute sind in allen Sprachen identisch, da sie der PostgreSQL-Implementierung entsprechen.

**Beschreibung (DE):** Diese Tabelle stellt landwirtschaftliche Erzeugnisse dar. In der Vererbungsarchitektur der Datenbank fungiert sie als direkter Untertyp der Tabelle [`component`](component.md). Sie speichert keine redundanten beschreibenden Spalten: Stattdessen nutzt sie einen gemeinsamen Primärschlüssel, um alle übergeordneten Attribute (wie Name, Lage, Verwaltungsform und Geometrie) von ihrem übergeordneten Datensatz `component` zu erben.

## Spaltenstruktur

| Spalte | Datentyp | Definition | Beispielwert | Einschränkung? | Geometrie? | Kommentare |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Eindeutige Kennung des landwirtschaftlichen Erzeugnisses | `42` | PK, FK | Nein | Primärschlüssel, der zugleich als Fremdschlüssel auf `component.id` verweist |
| `average_invested` | BIGINT | [...] | [...] | - | Nein | [...] |
| `expected_yield` | BIGINT | [...] | [...] | - | Nein | [...] |
| `gate_price` | BIGINT | [...] | [...] | - | Nein | [...] |
| `year_production` | BIGINT | [...] | [...] | - | Nein | [...] |
| `subtype` | VARCHAR | [...] | [...] | - | Nein | [...] |

## Beziehungen

* **Erbt von (Untertyp von):** [`component`](component.md). Die Tabelle `agriculture_product` ist eine spezialisierte Erweiterung der Tabelle `component`.
* **Hat Untertypen (Vererbung):** Die folgenden Tabellen erben von `agriculture_product` und teilen deren `id`:
    * [`crop`](crop.md)
    * [`stored`](stored.md)
* **Gehört zu:** [`enterprise`](enterprise.md) (Ein Komponenten-Untertyp ist mit genau einem Unternehmen verknüpft)
* **Hat viele:** `damage` (Ein Komponenten-Untertyp kann im Laufe der Zeit mehrfach beschädigt werden)

!!! tip "Wo befinden sich die übrigen Daten?"
    Um den Namen, den geografischen Standort (`geometry`, `town`, `country`) oder die Eigentumsangaben eines landwirtschaftlichen Erzeugnisses zu ermitteln, müssen Sie diese Tabelle mit dem Datensatz `component` verknüpfen, der dieselbe `id` besitzt.

## Beispielabfrage

Rufen Sie eine Liste aller landwirtschaftlichen Erzeugnisse ab, einschließlich Namen, Gemeinden und räumlicher Koordinaten, indem Sie die Tabelle mit ihrer übergeordneten Entität `enterprise` verknüpfen:

```sql
SELECT 
    ap.id, 
    c.name, 
    c.town, 
    ST_AsText(c.geometry) as coordinates 
FROM 
    agriculture_product ap
JOIN 
    component c ON ap.id = c.id
WHERE 
    c.component_kind  = 'AGRICULTURE_PRODUCT';
```
