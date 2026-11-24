# Tabelle: `enterprise_owner`

!!! warning "KI-gestützte Übersetzung"
    Diese Seite wurde mit Unterstützung künstlicher Intelligenz übersetzt und kann Fehler enthalten. Maßgeblich ist die englische Version. Die Namen der Tabellen und Attribute sind in allen Sprachen identisch, da sie der PostgreSQL-Implementierung entsprechen.

**Beschreibung (DE):** Diese Entität dient als Verknüpfungstabelle für die Viele-zu-viele-Beziehung zwischen [`enterprise`](enterprise.md) und [`owner`](owner.md).

## Spaltenstruktur

| Spalte | Datentyp | Definition | Beispielwert | Einschränkung? | Geometrie? | Kommentare |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `enterprise_id` | BIGINT | Kennung des Unternehmens | `3` | FK | Nein | Verweist auf die Tabelle `enterprise` |
| `owner_id` | BIGINT | Kennung des Eigentümers | `8` | FK | Nein | Verweist auf die Tabelle `owner` |


