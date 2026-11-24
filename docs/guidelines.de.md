# Hinweise zur Mitarbeit

!!! warning "KI-gestützte Übersetzung"
    Diese Seite wurde mit Unterstützung künstlicher Intelligenz übersetzt und kann Fehler enthalten. Maßgeblich ist die englische Version. Die Namen der Tabellen und Attribute sind in allen Sprachen identisch, da sie der PostgreSQL-Implementierung entsprechen.

Vielen Dank, dass Sie uns helfen, das Datenwörterbuch korrekt und aktuell zu halten! 

Gute Dokumentation ist Teamarbeit. Sie müssen weder Entwicklerin oder Entwickler sein noch programmieren können oder Git kennen, um zu diesem Projekt beizutragen. Alle inhaltlichen Aktualisierungen werden über eine einfache Tabellenkalkulation verwaltet.

---

## Der Arbeitsablauf

Die Aktualisierung des Wörterbuchs besteht nur aus drei einfachen Schritten:

1. **Vorlage herunterladen:** Laden Sie die neueste Version der Excel-Vorlage des Datenwörterbuchs aus unserem gemeinsamen Teamordner herunter.
2. **Daten eintragen:** Ergänzen oder aktualisieren Sie die Zeilen, die den Tabellen und Spalten der Datenbank entsprechen, die Sie dokumentieren.
3. **Zur Veröffentlichung einreichen:** Senden Sie die aktualisierte Excel-Datei an das technische Team. Wir starten einen automatisierten Prozess, der Ihre Tabellenkalkulation in die Webseiten umwandelt, die Sie hier sehen.

---

## So füllen Sie die Excel-Vorlage aus

Jedes Blatt der Excel-Datei steht für eine einzelne Datenbanktabelle. Bitte machen Sie zu jeder Spalte dieser Tabelle die folgenden Angaben:

* **Column:** Der genaue technische Name des Feldes in der Datenbank (z. B. `user_id`, `geom`, `created_at`).
* **Data type:** Das Format der Daten (z. B. `VARCHAR(255)`, `UUID`, `POINT`, `INTEGER`).
* **Definition (IT) & Definition (EN):** Eine klare, auch für Nicht-Fachleute verständliche Beschreibung dessen, was die Spalte darstellt. Bitte füllen Sie sowohl die italienische als auch die englische Spalte aus, um unsere zweisprachige Plattform zu unterstützen.
* **Example value:** Ein realistisches Beispiel für die Daten, damit andere das Format verstehen (z. B. `john.doe@email.com` oder `POINT(12.49 41.89)`).
* **Constraint?:** Geben Sie vorhandene Datenbankregeln an, etwa `PK` (Primärschlüssel), `FK` (Fremdschlüssel) oder `NOT NULL`.
* **Geometry?:** Geben Sie an, ob das Feld räumliche Daten enthält (z. B. `Yes - EPSG:4326` oder `No`).
* **Comments (IT) & Comments (EN):** Zusätzlicher Kontext, Geschäftslogik oder Hinweise dazu, wie diese Daten verwendet oder interpretiert werden sollen.

!!! warning "Formatierung einfach halten"
    Bitte vermeiden Sie aufwendige Excel-Formatierungen wie verbundene Zellen, individuelle Zellfarben oder mehrere Zeilen innerhalb einer Zelle. Einfacher Text sorgt für die reibungsloseste Umwandlung in die Webplattform!

---

## Änderungen einreichen

Sobald Ihre Excel-Datei fertig und geprüft ist:

* Laden Sie die neue Version im vorgesehenen gemeinsamen Laufwerk hoch.
* Informieren Sie das Datenbank-Administrationsteam per E-Mail oder über unseren internen Chat.
* Das Team verarbeitet die Datei, und Ihre Änderungen sind innerhalb weniger Minuten im Datenwörterbuch sichtbar!