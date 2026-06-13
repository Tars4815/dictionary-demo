# Tabella: `enterprise`

**Descrizione (IT):** Questa è l'entità genitore principale (superclasse) del database. Memorizza gli attributi universali di alto livello, come l'identificazione, la posizione geografica e i dettagli sulla proprietà, per tutti i principali asset fisici o aziendali. Tipi specifici di imprese (come [edifici](building.it.md), aziende agricole o sistemi di rete) memorizzano i loro dati specializzati in sotto-tabelle separate che condividono lo stesso ID.

## Struttura delle colonne

| Colonna | Tipo di dato | Definizione | Valore di esempio | Vincolo? | Geometria? | Commenti |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Identificativo univoco dell'impresa | `3` | PK | No | Funge da ID universale per tutte le tabelle di sottotipo |
| `type` | VARCHAR(255) | Colonna discriminante che definisce il tipo specifico di impresa | `BUILDING` | NOT NULL | No | Valori previsti: 'BUILDING', 'FARM', 'NETWORK_SYSTEM' |
| `name` | VARCHAR(255) | Nome ufficiale o denominazione dell'impresa | `Sede Centrale` | | No | |
| `management_type` | VARCHAR(255) | Tipo di gestione o amministrazione aziendale | `PUBLIC` | | No | es. 'PUBLIC', 'PRIVATE', 'MIXED' |
| `town` | VARCHAR(255) | Comune in cui si trova l'impresa | `Roma` | | No | |
| `country` | VARCHAR(255) | Paese in cui si trova l'impresa | `Italia` | | No | |
| `geometry` | GEOMETRY | Rappresentazione spaziale dell'impresa | `POINT(12.49 41.89)` | | Sì | EPSG:4326. Può essere un Punto o un Poligono a seconda della scala |
| `owner_id` | BIGINT | Identificativo del proprietario dell'entità | `42` | FK | No | Fa riferimento alla tabella `owner` |

## Relazioni

Poiché `enterprise` è il nodo centrale dello schema, possiede relazioni estese:

* **Ha Sottotipi (Ereditarietà):** Le seguenti tabelle ereditano da `enterprise` e condividono il suo `id`:
    * [`building`](building.md)
    * `farm`
    * `network_system`
* **Appartiene a:** `owner` (Un'impresa è posseduta da un proprietario)
* **Ha molti:** [`component`](component.md) (Un'impresa è composta da più sotto-componenti come macchinari, colture o reti elettriche)
* **Ha molti:** `survey` (Un'impresa può subire più perizie di danno o valutazioni nel tempo)

## Query di Esempio

Recupera un elenco di tutte le imprese situate in un comune specifico, mostrando il loro nome, la loro classificazione specifica (tipo) e le loro coordinate:

```sql
SELECT 
    id, 
    name, 
    type, 
    ST_AsText(geometry) as coordinates 
FROM 
    enterprise 
WHERE 
    town = 'Roma'
ORDER BY 
    type ASC;
```