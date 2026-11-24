# Tabella: `damage_fixed_asset`

!!! warning "Traduzione assistita dall'IA"
    Questa pagina è stata tradotta con l'assistenza dell'intelligenza artificiale e può contenere imprecisioni. La versione inglese è il riferimento. I nomi delle tabelle e degli attributi sono identici in tutte le lingue perché corrispondono a quelli dell'implementazione PostgreSQL.

**Descrizione (IT):** Questa tabella rappresenta i danni segnalati alle immobilizzazioni delle aziende agricole. Nell'architettura di ereditarietà del database, funge da sottotipo diretto della tabella [`farm_damage`](farm_damage.md), che è a sua volta un sottotipo di [`damage`](damage.md). Non memorizza colonne descrittive ridondanti: usa invece una chiave primaria condivisa per ereditare tutti gli attributi di alto livello (come descrizione, date, posizione e geometria) dal record genitore `damage`.

## Struttura delle colonne

| Colonna | Tipo di dato | Definizione | Valore di esempio | Vincolo? | Geometria? | Commenti |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Identificativo univoco del danno a un'immobilizzazione di un'azienda agricola | `42` | PK, FK | No | Chiave primaria che funge anche da chiave esterna verso `farm_damage.id` (e, a sua volta, verso `damage.id`) |
| `perc_area` | DOUBLE PRECISION | Percentuale dell'area interessata | [...] | - | No | - |
| `size` | DOUBLE PRECISION | Dimensione dell'immobilizzazione interessata | [...] | - | No | - |

## Relazioni

* **Eredita da (sottotipo di):** [`farm_damage`](farm_damage.md), che a sua volta eredita da [`damage`](damage.md). La tabella `damage_fixed_asset` è un'estensione specializzata della tabella `farm_damage`.
* **Interessa:** [`component`](component.md) (Uno o più danni interessano un componente o le sue sottoclassi)
* **È segnalato da:** [`survey`](survey.md) (Uno o più danni sono segnalati in un rilevamento)
* **Segnalato in:** [`attachment`](attachment.md) (Un danno è segnalato in uno o più allegati)
* **Comporta:** [`economic_loss`](economic_loss.md)

!!! tip "Dove si trova il resto dei dati?"
    Per trovare la descrizione, le date, la posizione geografica (`geometry`, `town`, `country`) o altri dettagli di un danno alle immobilizzazioni delle aziende agricole, devi unire questa tabella con il record `damage` che condivide lo stesso `id`.

## Query di esempio

Recupera un elenco di tutti i danni alle immobilizzazioni delle aziende agricole, includendo descrizioni, comuni e coordinate spaziali, unendo la tabella con la sua entità genitore `damage`:

```sql
SELECT
    dfa.*,
    d.*
FROM 
    damage_fixed_asset dfa JOIN damage d ON dfa.id = d.id;
```
