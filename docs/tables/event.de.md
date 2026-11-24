# Tabelle: `event`

!!! warning "KI-gestützte Übersetzung"
    Diese Seite wurde mit Unterstützung künstlicher Intelligenz übersetzt und kann Fehler enthalten. Maßgeblich ist die englische Version. Die Namen der Tabellen und Attribute sind in allen Sprachen identisch, da sie der PostgreSQL-Implementierung entsprechen.

**Beschreibung (DE):** Diese Tabelle speichert die Informationen und Einzelheiten zu einem bestimmten größeren Ereignis.

## Spaltenstruktur

| Spalte | Datentyp | Definition | Beispielwert | Einschränkung? | Geometrie? | Kommentare |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Eindeutige Kennung des Ereignisses | `3` | PK | Nein | [...] |
| `date` | TIMESTAMP | Zeitpunkt des Eintretens des Ereignisses | [...] | - | Nein | [...] |
| `date_end` | TIMESTAMP | Zeitpunkt des Endes des Ereignisses | [...] | - | Nein | [...] |
| `parent_event_id` | BIGINT | Verweis bei einem Mehrfachereignis | [...] | FK | Nein | Verweist auf die id der Entität [event](event.md) |
| `name` | VARCHAR | Name des Ereignisses | `Storm Example` | - | Nein | - |
| `severity` | VARCHAR | Schweregrad des Ereignisses | [...] | - | Nein | - |
| `type` | VARCHAR | Art des Ereignisses | [...] | - | Nein | - |
| `country` | VARCHAR | Land, in dem sich das Ereignis befindet | `Italy` | - | Nein | - |
| `state` | VARCHAR | Bundesland oder Region, in dem bzw. in der sich das Ereignis befindet | `Lazio` | - | Nein | - |
| `county` | VARCHAR | Landkreis oder Provinz, in dem bzw. in der sich das Ereignis befindet | `Rome` | - | Nein | - |
| `town` | VARCHAR | Gemeinde, in der sich das Ereignis befindet | `Rome` | - | Nein | - |
| `hamlet` | VARCHAR | Weiler oder Ortsteil, in dem sich das Ereignis befindet | `Trastevere` | - | Nein | - |
| `road` | VARCHAR | Straße, in der sich das Ereignis befindet | `Via Appia` | - | Nein | - |
| `house_number` | VARCHAR | Hausnummer des Ereignisses | `10` | - | Nein | - |
| `postcode` | VARCHAR | Postleitzahl des Ereignisses | `00100` | - | Nein | - |
| `geometry` | GEOMETRY | Räumliche Darstellung des Ereignisses | [...] | - | Ja | - |
| `coordinates_inferred` | BOOLEAN | Gibt an, ob die Koordinaten des Ereignisses abgeleitet statt direkt gemessen wurden | [...] | - | Nein | - |

## Beziehungen

* **Hat viele:** [`survey`](survey.md) (Auf ein Ereignis können mehrere Schadensbewertungserhebungen folgen)
* **Ist Teil von / hat Teile:** [`event`](event.md) über `parent_event_id`. Ein Mehrfachereignis kann in untergeordnete Ereignisse aufgeteilt werden, die auf das übergeordnete Ereignis verweisen.
