# Tabella: `damage`

!!! warning "Traduzione assistita dall'IA"
    Questa pagina è stata tradotta con l'assistenza dell'intelligenza artificiale e può contenere imprecisioni. La versione inglese è il riferimento. I nomi delle tabelle e degli attributi sono identici in tutte le lingue perché corrispondono a quelli dell'implementazione PostgreSQL.

**Descrizione (IT):** Questa tabella memorizza gli attributi universali di alto livello, come l'identificazione e la posizione geografica, per tutti i danni che seguono il verificarsi di un evento. I tipi specifici di danno (come [danni ai beni artistici](damage_artistic_good.md), [danni alla funzionalità dell'edificio](damage_building_functionality.md) o altri) memorizzano i propri dati specializzati in sotto-tabelle separate che condividono lo stesso ID.

## Struttura delle colonne

| Colonna | Tipo di dato | Definizione | Valore di esempio | Vincolo? | Geometria? | Commenti |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Identificativo univoco del danno | `3` | PK | No | Funge da ID universale per tutte le tabelle dei sottotipi |
| `estimated_value` | BIGINT | [...] | - | - | No | - |
| `component_id` | BIGINT | [...] | - | FK | No | Punta all'id dell'entità [component](component.md) |
| `date` | TIMESTAMP | [...] | [...] | - | No | - |
| `end_date` | TIMESTAMP | [...] | [...] | - | No | - |
| `start_end` | TIMESTAMP | [...] | [...] | - | No | - |
| `survey_id` | BIGINT | [...] | [...] | FK | No | Punta all'id dell'entità [survey](survey.md) |
| `country` | VARCHAR | [...] | [...] | - | No | - |
| `county` | VARCHAR | [...] | [...] | - | No | - |
| `description` | VARCHAR | [...] | [...] | - | No | - |
| `hamlet` | VARCHAR | [...] | [...] | - | No | - |
| `house_number` | VARCHAR | [...] | [...] | - | No | - |
| `postcode` | VARCHAR | [...] | [...] | - | No | - |
| `road` | VARCHAR | [...] | [...] | - | No | - |
| `state` | VARCHAR | [...] | [...] | - | No | - |
| `town` | VARCHAR | [...] | [...] | - | No | - |
| `geometry` | GEOMETRY | Rappresentazione spaziale dell'entità danno | [...] | - | No | - |
| `coordinates_inferred` | BOOLEAN | [...] | [...] | - | No | - |
| `sendai_indicator` | VARCHAR | [...] | [...] | - | No | - |

## Relazioni

Poiché `damage` è una delle entità centrali dello schema, ha numerose relazioni:

* **Ha sottotipi (ereditarietà):** Le tabelle seguenti ereditano da `damage` e condividono il suo `id`:
    * [`damage_artistic_good`](damage_artistic_good.md)
    * [`damage_building_functionality`](damage_building_functionality.md)
    * [`damage_building_not_structural`](damage_building_not_structural.md)
    * [`damage_building_structural`](damage_building_structural.md)
    * [`damage_business_operations`](damage_business_operations.md)
    * [`damage_church_structure`](damage_church_structure.md)
    * [`damage_goods`](damage_goods.md)
    * [`damage_network_component`](damage_network_component.md)
    * [`damage_network_service`](damage_network_service.md)
    * [`damage_people`](damage_people.md)
    * [`damage_product`](damage_product.md)
    * [`damage_vehicles`](damage_vehicles.md)
    * [`damage_whole_structure`](damage_whole_structure.md)
    * [`farm_damage`](farm_damage.md)
* **Interessa:** [`component`](component.md) (Uno o più danni interessano un componente o le sue sottoclassi)
* **È registrato da:** [`survey`](survey.md) (Uno o più danni sono segnalati in un rilevamento)
* **È documentato in:** [`attachment`](attachment.md) (Un danno è segnalato in uno o più allegati)
* **Comporta:** [`economic_loss`](economic_loss.md)