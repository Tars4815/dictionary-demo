# Tabelle: `attachment`

!!! warning "KI-gestützte Übersetzung"
    Diese Seite wurde mit Unterstützung künstlicher Intelligenz übersetzt und kann Fehler enthalten. Maßgeblich ist die englische Version. Die Namen der Tabellen und Attribute sind in allen Sprachen identisch, da sie der PostgreSQL-Implementierung entsprechen.

**Beschreibung (DE):** Diese Tabelle speichert die Informationen und Einzelheiten zu einem Anhang.

## Spaltenstruktur

| Spalte | Datentyp | Definition | Beispielwert | Einschränkung? | Geometrie? | Kommentare |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Eindeutige Kennung des Anhangs | `3` | PK | Nein | [...] |
| `damage_id` | BIGINT | Fremdschlüssel, der auf einen gemeldeten Schaden verweist | [...] | FK | Nein | Verweist auf die id der Entität [damage](damage.md) |
| `date` | TIMESTAMP | [...] | - | - | Nein | - |
| `size` | BIGINT | [...] | - | - | Nein | - |
| `description` | VARCHAR | [...] | - | - | Nein | - |
| `name` | VARCHAR | [...] | - | - | Nein | - |
| `type` | VARCHAR | [...] | - | - | Nein | - |
| `data` | BIGINT | [...] | - | - | Nein | - |

## Beziehungen

* **Dokumente** [`damage`](damage.md)