# Tabelle: `economic_loss`

!!! warning "KI-gestützte Übersetzung"
    Diese Seite wurde mit Unterstützung künstlicher Intelligenz übersetzt und kann Fehler enthalten. Maßgeblich ist die englische Version. Die Namen der Tabellen und Attribute sind in allen Sprachen identisch, da sie der PostgreSQL-Implementierung entsprechen.

**Beschreibung (DE):** Diese Tabelle speichert die Kosten, die mit einem gemeldeten Schaden verbunden sind: die geschätzten, genehmigten und endgültigen Beträge.

## Spaltenstruktur

| Spalte | Datentyp | Definition | Beispielwert | Einschränkung? | Geometrie? | Kommentare |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Eindeutige Kennung des Datensatzes zum wirtschaftlichen Verlust | `3` | PK | Nein | [...] |
| `damage_id` | BIGINT | Fremdschlüssel, der auf einen gemeldeten Schaden verweist | [...] | FK | Nein | Verweist auf die id der Entität [damage](damage.md) |
| `approved_cost` | DOUBLE PRECISION | Für den Schaden genehmigte Kosten | - | - | Nein | - |
| `estimated_cost` | DOUBLE PRECISION | Geschätzte Kosten des Schadens | - | - | Nein | - |
| `final_cost` | DOUBLE PRECISION | Endgültige Kosten des Schadens | - | - | Nein | - |
| `type_of_cost` | VARCHAR | Kostenart | - | - | Nein | - |

## Beziehungen

* **Bezieht sich auf:** [`damage`](damage.md) über `damage_id`. Der wirtschaftliche Verlust ist das monetäre Ergebnis eines gemeldeten Schadens.

## Beispielabfrage

Rufen Sie die für jeden Schaden erfassten Kosten ab:

```sql
SELECT 
    d.id AS damage_id, 
    el.type_of_cost, 
    el.estimated_cost, 
    el.approved_cost, 
    el.final_cost 
FROM 
    economic_loss el
JOIN 
    damage d ON el.damage_id = d.id;
```
