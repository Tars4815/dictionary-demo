# Tabelle: `damage_staff`

!!! warning "KI-gestützte Übersetzung"
    Diese Seite wurde mit Unterstützung künstlicher Intelligenz übersetzt und kann Fehler enthalten. Maßgeblich ist die englische Version. Die Namen der Tabellen und Attribute sind in allen Sprachen identisch, da sie der PostgreSQL-Implementierung entsprechen.

**Beschreibung (DE):** Diese Tabelle stellt gemeldete Schäden am Personal landwirtschaftlicher Betriebe dar. In der Vererbungsarchitektur der Datenbank fungiert sie als direkter Untertyp der Tabelle [`farm_damage`](farm_damage.md), die ihrerseits ein Untertyp von [`damage`](damage.md) ist. Sie speichert keine redundanten beschreibenden Spalten: Stattdessen nutzt sie einen gemeinsamen Primärschlüssel, um alle übergeordneten Attribute (wie Beschreibung, Daten, Lage und Geometrie) von ihrem übergeordneten Datensatz `damage` zu erben.

## Spaltenstruktur

| Spalte | Datentyp | Definition | Beispielwert | Einschränkung? | Geometrie? | Kommentare |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Eindeutige Kennung des Schadens am Personal eines landwirtschaftlichen Betriebs | `42` | PK, FK | Nein | Primärschlüssel, der zugleich als Fremdschlüssel auf `farm_damage.id` (und seinerseits auf `damage.id`) verweist |
| `duration_of_absence` | INTEGER | Dauer der Abwesenheit des Personals | [...] | - | Nein | - |
| `number_of_absent` | INTEGER | Anzahl der abwesenden Personalmitglieder | [...] | - | Nein | - |
| `number_of_dead` | INTEGER | Anzahl der getöteten Personalmitglieder | [...] | - | Nein | - |
| `number_of_injured` | INTEGER | Anzahl der verletzten Personalmitglieder | [...] | - | Nein | - |
| `further_details` | VARCHAR | Weitere Angaben zum Schaden am Personal | [...] | - | Nein | - |
| `reason_of_absence` | VARCHAR | Grund der Abwesenheit | [...] | - | Nein | - |
| `number_of_missing` | INTEGER | Anzahl der vermissten Personalmitglieder | [...] | - | Nein | - |

## Beziehungen

* **Erbt von (Untertyp von):** [`farm_damage`](farm_damage.md), die ihrerseits von [`damage`](damage.md) erbt. Die Tabelle `damage_staff` ist eine spezialisierte Erweiterung der Tabelle `farm_damage`.
* **Betrifft:** [`component`](component.md) (Ein oder mehrere Schäden betreffen eine Komponente oder ihre Unterklassen)
* **Wird gemeldet durch:** [`survey`](survey.md) (Ein oder mehrere Schäden werden in einer Erhebung gemeldet)
* **Gemeldet in:** [`attachment`](attachment.md) (Ein Schaden wird in einem oder mehreren Anhängen gemeldet)
* **Führt zu:** [`economic_loss`](economic_loss.md)

!!! tip "Wo befinden sich die übrigen Daten?"
    Um die Beschreibung, die Daten, den geografischen Standort (`geometry`, `town`, `country`) oder weitere Angaben zu einem Schaden am Personal zu ermitteln, müssen Sie diese Tabelle mit dem Datensatz `damage` verknüpfen, der dieselbe `id` besitzt.

## Beispielabfrage

Rufen Sie eine Liste aller Schäden am Personal ab, einschließlich Beschreibungen, Gemeinden und räumlicher Koordinaten, indem Sie die Tabelle mit ihrer übergeordneten Entität `damage` verknüpfen:

```sql
SELECT
    ds.*,
    d.*
FROM 
    damage_staff ds JOIN damage d ON ds.id = d.id;
```
