# Tabelle: `damage_provision`

!!! warning "KI-gestützte Übersetzung"
    Diese Seite wurde mit Unterstützung künstlicher Intelligenz übersetzt und kann Fehler enthalten. Maßgeblich ist die englische Version. Die Namen der Tabellen und Attribute sind in allen Sprachen identisch, da sie der PostgreSQL-Implementierung entsprechen.

**Beschreibung (DE):** Diese Tabelle stellt gemeldete Schäden an Vorräten dar. In der Vererbungsarchitektur der Datenbank fungiert sie als direkter Untertyp der Tabelle [`farm_damage`](farm_damage.md), die ihrerseits ein Untertyp von [`damage`](damage.md) ist. Sie speichert keine redundanten beschreibenden Spalten: Stattdessen nutzt sie einen gemeinsamen Primärschlüssel, um alle übergeordneten Attribute (wie Beschreibung, Daten, Lage und Geometrie) von ihrem übergeordneten Datensatz `damage` zu erben.

## Spaltenstruktur

| Spalte | Datentyp | Definition | Beispielwert | Einschränkung? | Geometrie? | Kommentare |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Eindeutige Kennung des Schadens an Vorräten | `42` | PK, FK | Nein | Primärschlüssel, der zugleich als Fremdschlüssel auf `farm_damage.id` (und seinerseits auf `damage.id`) verweist |
| `additional_food` | INTEGER | Zusätzliche Futterkosten | [...] | - | Nein | - |
| `additional_veterinary` | INTEGER | Zusätzliche Tierarztkosten | [...] | - | Nein | - |
| `losses_fees` | INTEGER | Gebührenausfälle | [...] | - | Nein | - |
| `losses_premature_sale` | INTEGER | Verluste durch vorzeitigen Verkauf | [...] | - | Nein | - |
| `losses_value` | INTEGER | Wert der Verluste | [...] | - | Nein | - |
| `relocation_cost` | INTEGER | Umsiedlungskosten | [...] | - | Nein | - |
| `replanting_cost` | INTEGER | Kosten der Neubepflanzung | [...] | - | Nein | - |
| `additional_materials` | INTEGER | Kosten für zusätzliche Materialien | [...] | - | Nein | - |
| `restoration_cost` | INTEGER | Wiederherstellungskosten | [...] | - | Nein | - |

## Beziehungen

* **Erbt von (Untertyp von):** [`farm_damage`](farm_damage.md), die ihrerseits von [`damage`](damage.md) erbt. Die Tabelle `damage_provision` ist eine spezialisierte Erweiterung der Tabelle `farm_damage`.
* **Betrifft:** [`component`](component.md) (Ein oder mehrere Schäden betreffen eine Komponente oder ihre Unterklassen)
* **Wird gemeldet durch:** [`survey`](survey.md) (Ein oder mehrere Schäden werden in einer Erhebung gemeldet)
* **Gemeldet in:** [`attachment`](attachment.md) (Ein Schaden wird in einem oder mehreren Anhängen gemeldet)
* **Führt zu:** [`economic_loss`](economic_loss.md)

!!! tip "Wo befinden sich die übrigen Daten?"
    Um die Beschreibung, die Daten, den geografischen Standort (`geometry`, `town`, `country`) oder weitere Angaben zu einem Schaden an Vorräten zu ermitteln, müssen Sie diese Tabelle mit dem Datensatz `damage` verknüpfen, der dieselbe `id` besitzt.

## Beispielabfrage

Rufen Sie eine Liste aller Schäden an Vorräten ab, einschließlich Beschreibungen, Gemeinden und räumlicher Koordinaten, indem Sie die Tabelle mit ihrer übergeordneten Entität `damage` verknüpfen:

```sql
SELECT
    dp.*,
    d.*
FROM 
    damage_provision dp JOIN damage d ON dp.id = d.id;
```
