# Tabelle: `survey`

!!! warning "KI-gestützte Übersetzung"
    Diese Seite wurde mit Unterstützung künstlicher Intelligenz übersetzt und kann Fehler enthalten. Maßgeblich ist die englische Version. Die Namen der Tabellen und Attribute sind in allen Sprachen identisch, da sie der PostgreSQL-Implementierung entsprechen.

**Beschreibung (DE):** Diese Tabelle speichert die Informationen und Einzelheiten zu einer bestimmten Schadensbewertungserhebung, die im Anschluss an ein größeres Ereignis durchgeführt wurde.

## Spaltenstruktur

| Spalte | Datentyp | Definition | Beispielwert | Einschränkung? | Geometrie? | Kommentare |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Eindeutige Kennung der Erhebung | `3` | PK | Nein | [...] |
| `created_on` | TIMESTAMP | Zeitpunkt der Durchführung der Bewertungserhebung | [...] | NOT NULL | Nein | [...] |
| `enterprise_id` | BIGINT | Fremdschlüssel, der auf ein Unternehmen verweist | [...] | FK | Nein | Verweist auf die id der Entität [enterprise](enterprise.md) |
| `event_id` | BIGINT | Zeitpunkt der Durchführung der Bewertungserhebung | [...] | FK | Nein | Verweist auf die id der Entität [event](event.md) |

## Beziehungen

Da `survey` eine der zentralen Entitäten des Schemas ist, hat sie zahlreiche Beziehungen:

* **Meldet** [`damage`](damage.md)
* **Ist verknüpft mit** [`enterprise`](enterprise.md)
* **Folgt auf ein** [`event`](event.md)