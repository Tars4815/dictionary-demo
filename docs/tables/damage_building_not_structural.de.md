# Tabelle: `damage_building_not_structural`

!!! warning "KI-gestützte Übersetzung"
    Diese Seite wurde mit Unterstützung künstlicher Intelligenz übersetzt und kann Fehler enthalten. Maßgeblich ist die englische Version. Die Namen der Tabellen und Attribute sind in allen Sprachen identisch, da sie der PostgreSQL-Implementierung entsprechen.

**Beschreibung (DE):** Diese Tabelle stellt nicht strukturelle Schäden an Gebäudefunktionen dar. In der Vererbungsarchitektur der Datenbank fungiert sie als direkter Untertyp der Tabelle [`damage`](damage.md). Sie speichert keine redundanten beschreibenden Spalten: Stattdessen nutzt sie einen gemeinsamen Primärschlüssel, um alle übergeordneten Attribute (wie Name, Lage, Verwaltungsform und Geometrie) von ihrem übergeordneten Datensatz `damage` zu erben.

## Spaltenstruktur

| Spalte | Datentyp | Definition | Beispielwert | Einschränkung? | Geometrie? | Kommentare |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Eindeutige Kennung des nicht strukturellen Schadens an einem Gebäude | `42` | PK, FK | Nein | Primärschlüssel, der zugleich als Fremdschlüssel auf `damage.id` verweist |
| `non_structural_element` | VARCHAR | [...] | [...] | - | Nein | [...] |
| `non_structural_damage_type` | VARCHAR | [...] | [...] | - | Nein | [...] |
| `damage_quantification` | VARCHAR | [...] | [...] | - | Nein | [...] |

## Beziehungen

* **Erbt von (Untertyp von):** [`damage`](damage.md). Die Tabelle `damage_building_not_structural` ist eine spezialisierte Erweiterung der Tabelle `damage`.
* **Betrifft:** [`component`](component.md) (Ein oder mehrere Schäden betreffen eine Komponente oder ihre Unterklassen)
* **Wird gemeldet durch:** [`survey`](survey.md) (Ein oder mehrere Schäden werden in einer Erhebung gemeldet)
* **Gemeldet in:** [`attachment`](attachment.md) (Ein Schaden wird in einem oder mehreren Anhängen gemeldet)
* **Führt zu:** [`economic_loss`](economic_loss.md)

!!! tip "Wo befinden sich die übrigen Daten?"
    Um den Namen, den geografischen Standort (`geometry`, `town`, `country`) oder weitere Angaben zu einem nicht strukturellen Schaden an Gebäuden zu ermitteln, müssen Sie diese Tabelle mit dem Datensatz `damage` verknüpfen, der dieselbe `id` besitzt.

## Beispielabfrage

Rufen Sie eine Liste aller nicht strukturellen Schäden an Gebäuden ab, einschließlich Namen, Gemeinden und räumlicher Koordinaten, indem Sie die Tabelle mit ihrer übergeordneten Entität `damage` verknüpfen:

```sql
SELECT
    dbns.*,
    d.*
FROM 
    damage_building_not_structural dbns join damage d on dbns.id = d.id
```