# Tabelle: `farm`

!!! info "Abweichender Name in der Weboberfläche (GUI)"
    Im PostgreSQL-Backend heißt diese Tabelle `farm`, wie im Seitentitel angegeben. In der Oberfläche der Webanwendung erscheint sie als **Economic Activities - Farm**. Alle Aliasnamen finden Sie in der [Zuordnungstabelle](../backend-to-gui.md).

!!! warning "KI-gestützte Übersetzung"
    Diese Seite wurde mit Unterstützung künstlicher Intelligenz übersetzt und kann Fehler enthalten. Maßgeblich ist die englische Version. Die Namen der Tabellen und Attribute sind in allen Sprachen identisch, da sie der PostgreSQL-Implementierung entsprechen.

**Beschreibung (DE):** Diese Tabelle stellt landwirtschaftliche Unternehmen dar. In der Vererbungsarchitektur der Datenbank fungiert sie als direkter Untertyp der Tabelle [`enterprise`](enterprise.md). Sie speichert keine redundanten beschreibenden Spalten: Stattdessen nutzt sie einen gemeinsamen Primärschlüssel, um alle übergeordneten Attribute (wie Name, Lage, Verwaltungsform und Geometrie) von ihrem übergeordneten Datensatz `enterprise` zu erben.

## Spaltenstruktur

| Spalte | Datentyp | Definition | Beispielwert | Einschränkung? | Geometrie? | Kommentare |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Eindeutige Kennung des landwirtschaftlichen Betriebs | `42` | PK, FK | Nein | Primärschlüssel, der zugleich als Fremdschlüssel auf `enterprise.id` verweist |

## Beziehungen

* **Erbt von (Untertyp von):** [`enterprise`](enterprise.md). Die Tabelle `farm` ist eine spezialisierte Erweiterung der Tabelle `enterprise`.
* **Enthält:** Obwohl er nicht direkt über `farm_id` verknüpft ist, besitzt ein landwirtschaftlicher Betrieb landwirtschaftliche Vermögenswerte über die Spalte `enterprise_id` in der Tabelle `component`. Zu diesen Komponenten gehören häufig spezialisierte landwirtschaftliche Untertypen, zum Beispiel:
    * [`agriculture_product`](agriculture_product.md) und seine Untertypen [`crop`](crop.md) und [`stored`](stored.md)
    * [`livestock`](livestock.md)
    * [`fixed_asset`](fixed_asset.md) und seine Untertypen (z. B. [`machinery`](machinery.md), etwa Traktoren)

!!! tip "Wo befinden sich die übrigen Daten?"
    Um den Namen, den geografischen Standort (`geometry`, `town`, `country`) oder weitere Angaben zu einem landwirtschaftlichen Betrieb zu ermitteln, müssen Sie diese Tabelle mit dem Datensatz `enterprise` verknüpfen, der dieselbe `id` besitzt.

## Beispielabfrage

Rufen Sie eine Liste aller landwirtschaftlichen Betriebe ab, einschließlich Namen, Gemeinden und räumlicher Koordinaten, indem Sie die Tabelle mit ihrer übergeordneten Entität `enterprise` verknüpfen:

```sql
SELECT 
    f.id, 
    e.name, 
    e.town, 
    ST_AsText(e.geometry) as coordinates 
FROM 
    farm f
JOIN 
    enterprise e ON f.id = e.id
WHERE 
    e.type = 'FARM';
```
