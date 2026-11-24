# Tabelle: `damage_network_service`

!!! warning "KI-gestützte Übersetzung"
    Diese Seite wurde mit Unterstützung künstlicher Intelligenz übersetzt und kann Fehler enthalten. Maßgeblich ist die englische Version. Die Namen der Tabellen und Attribute sind in allen Sprachen identisch, da sie der PostgreSQL-Implementierung entsprechen.

**Beschreibung (DE):** Diese Tabelle stellt strukturelle Schäden an Netzdiensten dar. In der Vererbungsarchitektur der Datenbank fungiert sie als direkter Untertyp der Tabelle [`damage`](damage.md). Sie speichert keine redundanten beschreibenden Spalten: Stattdessen nutzt sie einen gemeinsamen Primärschlüssel, um alle übergeordneten Attribute (wie Name, Lage, Verwaltungsform und Geometrie) von ihrem übergeordneten Datensatz `damage` zu erben.

## Spaltenstruktur

| Spalte | Datentyp | Definition | Beispielwert | Einschränkung? | Geometrie? | Kommentare |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Eindeutige Kennung des Schadens an Netzdiensten | `42` | PK, FK | Nein | Primärschlüssel, der zugleich als Fremdschlüssel auf `damage.id` verweist |
| `affected_users` | BIGINT | [...] | [...] | - | Nein | [...] |
| `loss_of_service` | BIGINT | [...] | [...] | - | Nein | [...] |
| `electrical_outage` | VARCHAR | [...] | [...] | - | Nein | [...] |
| `telecom_outage` | VARCHAR | [...] | [...] | - | Nein | [...] |
| `transport_outage` | VARCHAR | [...] | [...] | - | Nein | [...] |

## Beziehungen

* **Erbt von (Untertyp von):** [`damage`](damage.md). Die Tabelle `damage_network_service` ist eine spezialisierte Erweiterung der Tabelle `damage`.
* **Betrifft:** [`component`](component.md) (Ein oder mehrere Schäden betreffen eine Komponente oder ihre Unterklassen)
* **Wird gemeldet durch:** [`survey`](survey.md) (Ein oder mehrere Schäden werden in einer Erhebung gemeldet)
* **Gemeldet in:** [`attachment`](attachment.md) (Ein Schaden wird in einem oder mehreren Anhängen gemeldet)
* **Führt zu:** [`economic_loss`](economic_loss.md)

!!! tip "Wo befinden sich die übrigen Daten?"
    Um den Namen, den geografischen Standort (`geometry`, `town`, `country`) oder weitere Angaben zu einem Schaden an Netzdiensten zu ermitteln, müssen Sie diese Tabelle mit dem Datensatz `damage` verknüpfen, der dieselbe `id` besitzt.

## Beispielabfrage

Rufen Sie eine Liste aller Schäden an Netzdiensten ab, einschließlich Beschreibungen, Gemeinden und räumlicher Koordinaten, indem Sie die Tabelle mit ihrer übergeordneten Entität `damage` verknüpfen:

```sql
SELECT
    dns.*,
    d.*
FROM 
    damage_network_service dns join damage d on dns.id = d.id
```