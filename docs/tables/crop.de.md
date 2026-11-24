# Tabelle: `crop`

!!! warning "KI-gestützte Übersetzung"
    Diese Seite wurde mit Unterstützung künstlicher Intelligenz übersetzt und kann Fehler enthalten. Maßgeblich ist die englische Version. Die Namen der Tabellen und Attribute sind in allen Sprachen identisch, da sie der PostgreSQL-Implementierung entsprechen.

**Beschreibung (DE):** Diese Tabelle stellt Kulturen (Anbaupflanzen) dar. In der Vererbungsarchitektur der Datenbank fungiert sie als direkter Untertyp der Tabelle [`agriculture_product`](agriculture_product.md). Sie speichert keine redundanten beschreibenden Spalten: Stattdessen nutzt sie einen gemeinsamen Primärschlüssel, um alle übergeordneten Attribute (wie Name, Lage, Verwaltungsform und Geometrie) von ihrem übergeordneten Datensatz `component` zu erben.

## Spaltenstruktur

| Spalte | Datentyp | Definition | Beispielwert | Einschränkung? | Geometrie? | Kommentare |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Eindeutige Kennung des Kultur-Datensatzes | `42` | PK, FK | Nein | Primärschlüssel, der zugleich als Fremdschlüssel auf `agriculture_product.id` und seinerseits auf `component.id` verweist |
| `area_planted` | BIGINT | [...] | [...] | - | Nein | [...] |
| `category` | VARCHAR | [...] | [...] | - | Nein | [...] |
| `growth` | VARCHAR | [...] | [...] | - | Nein | [...] |
| `duration` | VARCHAR | [...] | [...] | - | Nein | [...] |

## Beziehungen

* **Erbt von (Untertyp von):** [`agriculture_product`](agriculture_product.md). Die Tabelle `crop` ist eine spezialisierte Erweiterung der Tabelle `agriculture_product`.
* **Gehört zu:** [`enterprise`](enterprise.md) (Ein Komponenten-Untertyp ist mit genau einem Unternehmen verknüpft)
* **Hat viele:** `damage` (Ein Komponenten-Untertyp kann im Laufe der Zeit mehrfach beschädigt werden)

!!! tip "Wo befinden sich die übrigen Daten?"
    Um den Namen, den geografischen Standort (`geometry`, `town`, `country`) oder die Eigentumsangaben einer Kultur zu ermitteln, müssen Sie diese Tabelle mit dem Datensatz `component` verknüpfen, der dieselbe `id` besitzt.

## Beispielabfrage

Rufen Sie eine Liste aller Kulturen ab, einschließlich Namen, Gemeinden und räumlicher Koordinaten, indem Sie die Tabelle mit ihrer übergeordneten Entität `component` verknüpfen:

```sql
SELECT
    c.id,
    c.area_planted,
    c.category,
    ap.year_production 
FROM 
    crop c join agriculture_product ap on c.id = ap.id 
where ap.subtype = 'CROP'
```