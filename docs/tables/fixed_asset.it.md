# Tabella: `fixed_asset`

!!! info "Nome diverso nell'interfaccia web (GUI)"
    Nel backend PostgreSQL questa tabella si chiama `fixed_asset`, come indicato nel titolo della pagina. Nell'interfaccia della web-app compare come **Elements**. Tutti gli alias sono riportati nella [tabella di corrispondenza](../backend-to-gui.md).

!!! warning "Traduzione assistita dall'IA"
    Questa pagina è stata tradotta con l'assistenza dell'intelligenza artificiale e può contenere imprecisioni. La versione inglese è il riferimento. I nomi delle tabelle e degli attributi sono identici in tutte le lingue perché corrispondono a quelli dell'implementazione PostgreSQL.

**Descrizione (IT):** Questa tabella rappresenta i componenti di tipo immobilizzazione. Nell'architettura di ereditarietà del database, funge da sottotipo diretto della tabella [`component`](component.md). Non memorizza colonne descrittive ridondanti: usa invece una chiave primaria condivisa per ereditare tutti gli attributi di alto livello (come nome, posizione, tipo di gestione e geometria) dal record genitore `component`.

## Struttura delle colonne

| Colonna | Tipo di dato | Definizione | Valore di esempio | Vincolo? | Geometria? | Commenti |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Identificativo univoco del componente di tipo immobilizzazione | `42` | PK, FK | No | Chiave primaria che funge anche da chiave esterna verso `component.id` |

## Relazioni

* **Eredita da (sottotipo di):** [`component`](component.md). La tabella `fixed_asset` è un'estensione specializzata della tabella `component`.
* **Ha sottotipi (ereditarietà):** Le tabelle seguenti ereditano da `fixed_asset` e condividono il suo `id`:
    * [`infrastructure`](infrastructure.md)
    * [`land`](land.md)
    * [`machinery`](machinery.md)
    * [`material`](material.md)
* **Appartiene a:** [`enterprise`](enterprise.md) (Un sottotipo di componente è collegato a una sola impresa)
* **Ha molti:** `damage` (Un sottotipo di componente può subire più danni nel tempo)

!!! tip "Dove si trova il resto dei dati?"
    Per trovare il nome, la posizione geografica (`geometry`, `town`, `country`) o i dettagli sulla proprietà di un record fixed_asset, devi unire questa tabella con il record `component` che condivide lo stesso `id`.

## Query di esempio

Recupera un elenco di tutte le immobilizzazioni, includendo nomi, comuni e coordinate spaziali, unendo la tabella con la sua entità genitore `enterprise`:

```sql
SELECT 
    fa.id, 
    c.name, 
    c.town, 
    ST_AsText(c.geometry) as coordinates 
FROM 
    fixed_asset
JOIN 
    component c ON fa.id = c.id
WHERE 
    c.component_kind  = 'FIXED_ASSET';
```