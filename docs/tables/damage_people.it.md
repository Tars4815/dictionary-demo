# Tabella: `damage_people`

!!! warning "Traduzione assistita dall'IA"
    Questa pagina è stata tradotta con l'assistenza dell'intelligenza artificiale e può contenere imprecisioni. La versione inglese è il riferimento. I nomi delle tabelle e degli attributi sono identici in tutte le lingue perché corrispondono a quelli dell'implementazione PostgreSQL.

**Descrizione (IT):** Questa tabella rappresenta i danni segnalati alle persone. Nell'architettura di ereditarietà del database, funge da sottotipo diretto della tabella [`damage`](damage.md). Non memorizza colonne descrittive ridondanti: usa invece una chiave primaria condivisa per ereditare tutti gli attributi di alto livello (come nome, posizione, tipo di gestione e geometria) dal record genitore `damage`.

## Struttura delle colonne

| Colonna | Tipo di dato | Definizione | Valore di esempio | Vincolo? | Geometria? | Commenti |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Identificativo univoco dei danni alle persone | `42` | PK, FK | No | Chiave primaria che funge anche da chiave esterna verso `damage.id` |
| `number_of_dead` | INTEGER | [...] | [...] | - | No | - |
| `number_of_injured` | INTEGER | [...] | [...] | - | No | - |
| `number_of_missing` | INTEGER | [...] | [...] | - | No | - |


## Relazioni

* **Eredita da (sottotipo di):** [`damage`](damage.md). La tabella `damage_people` è un'estensione specializzata della tabella `damage`.
* **Interessa:** [`component`](component.md) (Uno o più danni interessano un componente o le sue sottoclassi)
* **È segnalato da:** [`survey`](survey.md) (Uno o più danni sono segnalati in un rilevamento)
* **Segnalato in:** [`attachment`](attachment.md) (Un danno è segnalato in uno o più allegati)
* **Comporta:** [`economic_loss`](economic_loss.md)

!!! tip "Dove si trova il resto dei dati?"
    Per trovare il nome, la posizione geografica (`geometry`, `town`, `country`) o altri dettagli di un danno alle persone, devi unire questa tabella con il record `damage` che condivide lo stesso `id`.

## Query di esempio

Recupera un elenco di tutti i danni alle persone, includendo descrizioni, comuni e coordinate spaziali, unendo la tabella con la sua entità genitore `damage`:

```sql
SELECT
    dp.*,
    d.*
FROM 
    damage_people dp  join damage d on dp.id = d.id
```