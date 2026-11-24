# Tabelle: `owner`

!!! info "Abweichender Name in der Weboberfläche (GUI)"
    Im PostgreSQL-Backend heißt diese Tabelle `owner`, wie im Seitentitel angegeben. In der Oberfläche der Webanwendung erscheint sie als **Owner profiles**. Alle Aliasnamen finden Sie in der [Zuordnungstabelle](../backend-to-gui.md).

!!! warning "KI-gestützte Übersetzung"
    Diese Seite wurde mit Unterstützung künstlicher Intelligenz übersetzt und kann Fehler enthalten. Maßgeblich ist die englische Version. Die Namen der Tabellen und Attribute sind in allen Sprachen identisch, da sie der PostgreSQL-Implementierung entsprechen.

**Beschreibung (DE):** Diese Entität speichert die universellen, übergeordneten Attribute, wie Identifikation und Kontaktdaten, für Eigentümerdatensätze.

## Spaltenstruktur

| Spalte | Datentyp | Definition | Beispielwert | Einschränkung? | Geometrie? | Kommentare |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Eindeutige Kennung des Eigentümers | `3` | PK | Nein | - |
| `email` | VARCHAR | E-Mail-Adresse des Eigentümers | `example@mail.com` | - | Nein | - |
| `fiscal_code` | VARCHAR | Steuernummer des Eigentümers | `AB0123CDEF` | - | Nein | Zeichenbegrenzung und Aufbau können von Land zu Land variieren |
| `full_name` | VARCHAR | Vollständiger Name des Eigentümers | `John Doe` | - | Nein | - |
| `phone` | VARCHAR | Telefonnummer und internationale Vorwahl des Eigentümers | `+390123456789` | - | Nein | - |

## Beziehungen

* **Besitzt:** [`enterprise`](enterprise.md) (Ein Eigentümer besitzt ein Unternehmen). Diese Viele-zu-viele-Beziehung wird über die Verknüpfungstabelle [`enterprise_owner`](enterprise_owner.md) vermittelt.

## Beispielabfrage

Rufen Sie eine Liste aller Eigentümer ab und zeigen Sie deren Namen und spezifische Kontaktdaten an:

```sql
SELECT *
FROM 
    owner o
ORDER BY 
    o.full_name ASC;
```

