# Tabelle: `enterprise`

!!! warning "KI-gestützte Übersetzung"
    Diese Seite wurde mit Unterstützung künstlicher Intelligenz übersetzt und kann Fehler enthalten. Maßgeblich ist die englische Version. Die Namen der Tabellen und Attribute sind in allen Sprachen identisch, da sie der PostgreSQL-Implementierung entsprechen.

**Beschreibung (DE):** Dies ist die zentrale übergeordnete Entität (Oberklasse) der Datenbank. Sie speichert die universellen, übergeordneten Attribute, wie Identifikation, geografische Lage und Verwaltungsangaben, für alle wichtigen physischen oder geschäftlichen Vermögenswerte. Spezifische Unternehmenstypen (wie [Gebäude](building.md), [Gewerbebetriebe](business.md), [landwirtschaftliche Betriebe](farm.md) oder [Netzsysteme](network_system.md)) speichern ihre spezialisierten Daten in separaten Untertabellen, die dieselbe ID teilen. Das Eigentum wird hier nicht gespeichert: Es wird in der Verknüpfungstabelle [`enterprise_owner`](enterprise_owner.md) erfasst.

## Spaltenstruktur

| Spalte | Datentyp | Definition | Beispielwert | Einschränkung? | Geometrie? | Kommentare |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Eindeutige Kennung des Unternehmens | `3` | PK | Nein | Dient als universelle ID für alle Untertyp-Tabellen |
| `type` | VARCHAR(255) | Diskriminatorspalte, die den spezifischen Typ des Unternehmens festlegt | `BUILDING` | NOT NULL | Nein | Derzeit in den Daten vorhandene Werte: 'BUILDING', 'FARM', 'TRANSPORT', 'TELECOMMUNICATION' |
| `name` | VARCHAR(255) | Offizieller Name oder Bezeichnung des Unternehmens | `Main Headquarters` |  | Nein |  |
| `management_type` | VARCHAR(255) | Art der Leitung oder Betriebsführung | `PUBLIC` |  | Nein | e.g., 'PUBLIC', 'PRIVATE', 'MIXED' |
| `vat` | VARCHAR(255) | Umsatzsteuer-Identifikationsnummer des Unternehmens | `IT00000000000` |  | Nein |  |
| `description` | VARCHAR(255) | Freitextbeschreibung des Unternehmens | `Regional hospital` |  | Nein |  |
| `country` | VARCHAR(255) | Land, in dem sich das Unternehmen befindet | `Italy` |  | Nein |  |
| `state` | VARCHAR(255) | Bundesland oder Region, in dem bzw. in der sich das Unternehmen befindet | `Lazio` |  | Nein |  |
| `county` | VARCHAR(255) | Landkreis oder Provinz, in dem bzw. in der sich das Unternehmen befindet | `Rome` |  | Nein |  |
| `town` | VARCHAR(255) | Gemeinde, in der sich das Unternehmen befindet | `Rome` |  | Nein |  |
| `hamlet` | VARCHAR(255) | Weiler oder Ortsteil, in dem sich das Unternehmen befindet | `Trastevere` |  | Nein |  |
| `road` | VARCHAR(255) | Straße, in der sich das Unternehmen befindet | `Via Appia` |  | Nein |  |
| `house_number` | VARCHAR(255) | Hausnummer des Unternehmens | `10` |  | Nein |  |
| `postcode` | VARCHAR(255) | Postleitzahl des Unternehmens | `00100` |  | Nein |  |
| `geometry` | GEOMETRY | Räumliche Darstellung des Unternehmens | `POINT(12.49 41.89)` |  | Ja | EPSG:4326. Kann je nach Maßstab ein Punkt oder ein Polygon sein |
| `coordinates_inferred` | BOOLEAN | Gibt an, ob die Koordinaten des Unternehmens abgeleitet statt direkt gemessen wurden | [...] |  | Nein |  |

## Beziehungen

Da `enterprise` der zentrale Knotenpunkt des Schemas ist, hat sie zahlreiche Beziehungen:

* **Hat Untertypen (Vererbung):** Die folgenden Tabellen erben von `enterprise` und teilen deren `id`:
    * [`building`](building.md)
    * [`business`](business.md)
    * [`farm`](farm.md)
    * [`network_system`](network_system.md)
* **Gehört:** [`owner`](owner.md). Ein Unternehmen kann mehrere Eigentümer haben, und ein Eigentümer kann mehrere Unternehmen besitzen. Diese Viele-zu-viele-Beziehung wird über die Verknüpfungstabelle [`enterprise_owner`](enterprise_owner.md) vermittelt.
* **Hat viele:** [`component`](component.md) (Ein Unternehmen besteht aus mehreren Teilkomponenten, etwa Maschinen, Kulturen oder Stromnetzen)
* **Hat viele:** [`survey`](survey.md) (Ein Unternehmen kann im Laufe der Zeit mehrere Schäden oder Bewertungserhebungen erfahren)

## Beispielabfrage

Rufen Sie eine Liste aller Unternehmen in einer bestimmten Gemeinde ab und zeigen Sie deren Namen, deren spezifische Klassifizierung (Typ) und deren Koordinaten an:

```sql
SELECT 
    id, 
    name, 
    type, 
    ST_AsText(geometry) as coordinates 
FROM 
    enterprise 
WHERE 
    town = 'Rome'
ORDER BY 
    type ASC;
```

Rufen Sie die Eigentümer jedes Unternehmens über die Verknüpfungstabelle ab:

```sql
SELECT 
    e.id, 
    e.name, 
    o.full_name 
FROM 
    enterprise e
JOIN 
    enterprise_owner eo ON eo.enterprise_id = e.id
JOIN 
    owner o ON o.id = eo.owner_id;
```
