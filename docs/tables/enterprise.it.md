# Tabella: `enterprise`

!!! warning "Traduzione assistita dall'IA"
    Questa pagina è stata tradotta con l'assistenza dell'intelligenza artificiale e può contenere imprecisioni. La versione inglese è il riferimento. I nomi delle tabelle e degli attributi sono identici in tutte le lingue perché corrispondono a quelli dell'implementazione PostgreSQL.

**Descrizione (IT):** Questa è l'entità genitore principale (superclasse) del database. Memorizza gli attributi universali di alto livello, come l'identificazione, la posizione geografica e i dettagli amministrativi, per tutti i principali asset fisici o aziendali. I tipi specifici di imprese (come [edifici](building.md), [attività commerciali](business.md), [aziende agricole](farm.md) o [sistemi di rete](network_system.md)) memorizzano i propri dati specializzati in sotto-tabelle separate che condividono lo stesso ID. La proprietà non è memorizzata qui: è registrata nella tabella di collegamento [`enterprise_owner`](enterprise_owner.md).

## Struttura delle colonne

| Colonna | Tipo di dato | Definizione | Valore di esempio | Vincolo? | Geometria? | Commenti |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Identificativo univoco dell'impresa | `3` | PK | No | Funge da ID universale per tutte le tabelle dei sottotipi |
| `type` | VARCHAR(255) | Colonna discriminante che definisce il tipo specifico di impresa | `BUILDING` | NOT NULL | No | Valori attualmente presenti nei dati: 'BUILDING', 'FARM', 'TRANSPORT', 'TELECOMMUNICATION' |
| `name` | VARCHAR(255) | Nome ufficiale o denominazione dell'impresa | `Main Headquarters` |  | No |  |
| `management_type` | VARCHAR(255) | Tipo di gestione o amministrazione aziendale | `PUBLIC` |  | No | e.g., 'PUBLIC', 'PRIVATE', 'MIXED' |
| `vat` | VARCHAR(255) | Partita IVA dell'impresa | `IT00000000000` |  | No |  |
| `description` | VARCHAR(255) | Descrizione a testo libero dell'impresa | `Regional hospital` |  | No |  |
| `country` | VARCHAR(255) | Paese in cui si trova l'impresa | `Italy` |  | No |  |
| `state` | VARCHAR(255) | Stato o regione in cui si trova l'impresa | `Lazio` |  | No |  |
| `county` | VARCHAR(255) | Contea o provincia in cui si trova l'impresa | `Rome` |  | No |  |
| `town` | VARCHAR(255) | Comune in cui si trova l'impresa | `Rome` |  | No |  |
| `hamlet` | VARCHAR(255) | Frazione o località in cui si trova l'impresa | `Trastevere` |  | No |  |
| `road` | VARCHAR(255) | Via in cui si trova l'impresa | `Via Appia` |  | No |  |
| `house_number` | VARCHAR(255) | Numero civico dell'impresa | `10` |  | No |  |
| `postcode` | VARCHAR(255) | Codice postale dell'impresa | `00100` |  | No |  |
| `geometry` | GEOMETRY | Rappresentazione spaziale dell'impresa | `POINT(12.49 41.89)` |  | Sì | EPSG:4326. Può essere un punto o un poligono a seconda della scala |
| `coordinates_inferred` | BOOLEAN | Indica se le coordinate dell'impresa sono state dedotte anziché misurate direttamente | [...] |  | No |  |

## Relazioni

Poiché `enterprise` è il nodo centrale dello schema, ha numerose relazioni:

* **Ha sottotipi (ereditarietà):** Le tabelle seguenti ereditano da `enterprise` e condividono il suo `id`:
    * [`building`](building.md)
    * [`business`](business.md)
    * [`farm`](farm.md)
    * [`network_system`](network_system.md)
* **È posseduta da:** [`owner`](owner.md). Un'impresa può avere più proprietari e un proprietario può detenere più imprese. Questa relazione molti-a-molti è mediata dalla tabella di collegamento [`enterprise_owner`](enterprise_owner.md).
* **Ha molti:** [`component`](component.md) (Un'impresa è composta da più sotto-componenti, come macchinari, colture o reti elettriche)
* **Ha molti:** [`survey`](survey.md) (Un'impresa può essere oggetto di più danni o rilevamenti di valutazione nel tempo)

## Query di esempio

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
    town = 'Rome'
ORDER BY 
    type ASC;
```

Recupera i proprietari di ciascuna impresa attraverso la tabella di collegamento:

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
