# Tabelle: `network_system`

!!! warning "KI-gestützte Übersetzung"
    Diese Seite wurde mit Unterstützung künstlicher Intelligenz übersetzt und kann Fehler enthalten. Maßgeblich ist die englische Version. Die Namen der Tabellen und Attribute sind in allen Sprachen identisch, da sie der PostgreSQL-Implementierung entsprechen.

**Beschreibung (DE):** Diese Tabelle stellt Infrastrukturnetzsysteme dar (z. B. Verkehrs-, Strom- oder Telekommunikationsnetze). In der Vererbungsarchitektur der Datenbank fungiert sie als direkter Untertyp der Tabelle [`enterprise`](enterprise.md). Sie speichert keine redundanten beschreibenden Spalten: Stattdessen nutzt sie einen gemeinsamen Primärschlüssel, um alle übergeordneten Attribute (wie Name, Lage, Verwaltungsform und Geometrie) von ihrem übergeordneten Datensatz `enterprise` zu erben.

## Spaltenstruktur

| Spalte | Datentyp | Definition | Beispielwert | Einschränkung? | Geometrie? | Kommentare |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Eindeutige Kennung des Netzsystems | `8` | PK, FK | Nein | Primärschlüssel, der zugleich als Fremdschlüssel auf `enterprise.id` verweist |

## Beziehungen

* **Erbt von (Untertyp von):** [`enterprise`](enterprise.md). Die Tabelle `network_system` ist eine spezialisierte Erweiterung der Tabelle `enterprise`.
* **Hat Untertypen (Vererbung):** Die folgenden Tabellen erben von `network_system` (und darüber von `enterprise`) und teilen deren `id`:
    * [`electrical_system`](electrical_system.md)
    * [`tlc_system`](tlc_system.md)
    * [`transport_system`](transport_system.md)
* **Enthält:** Obwohl es nicht direkt über `network_system_id` verknüpft ist, besitzt ein Netzsystem Infrastrukturgüter über die Spalte `enterprise_id` in der Tabelle `component`. Zu diesen Komponenten gehören häufig spezialisierte Untertypen, zum Beispiel:
    * `transport_network_component`
    * `electrical_network_component`
    * `tlc_network_component`
    * `network_service`

!!! tip "Wo befinden sich die übrigen Daten?"
    Um den Namen, den geografischen Standort (`geometry`, `town`, `country`) oder weitere Angaben zu einem Netzsystem zu ermitteln, müssen Sie diese Tabelle mit dem Datensatz `enterprise` verknüpfen, der dieselbe `id` besitzt.

## Beispielabfrage

Rufen Sie eine Liste aller Netzsysteme ab, einschließlich Namen, Gemeinden und räumlicher Koordinaten, indem Sie die Tabelle mit ihrer übergeordneten Entität `enterprise` verknüpfen:

```sql
SELECT 
    n.id, 
    e.name, 
    e.town, 
    e.type,
    ST_AsText(e.geometry) as coordinates 
FROM 
    network_system n
JOIN 
    enterprise e ON n.id = e.id;
```
