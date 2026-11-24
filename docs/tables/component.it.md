# Tabella: `component`

!!! warning "Traduzione assistita dall'IA"
    Questa pagina è stata tradotta con l'assistenza dell'intelligenza artificiale e può contenere imprecisioni. La versione inglese è il riferimento. I nomi delle tabelle e degli attributi sono identici in tutte le lingue perché corrispondono a quelli dell'implementazione PostgreSQL.

**Descrizione (IT):** Questa tabella memorizza gli attributi universali di alto livello, come l'identificazione e la posizione geografica, per tutti i principali componenti fisici o aziendali. I tipi specifici di componenti (come [corpi aggiunti](added_block.md), [beni artistici](artistic_good.md) o altri) memorizzano i propri dati specializzati in sotto-tabelle separate che condividono lo stesso ID.

## Struttura delle colonne

| Colonna | Tipo di dato | Definizione | Valore di esempio | Vincolo? | Geometria? | Commenti |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Identificativo univoco del componente | `3` | PK | No | Funge da ID universale per tutte le tabelle dei sottotipi |
| `component_kind` | VARCHAR | Colonna discriminante che identifica il sottotipo specifico del componente | `BUILDING_COMPONENT` | NOT NULL | No | Contiene il tipo più specifico. Valori attualmente presenti nei dati: 'BUILDING_COMPONENT', 'TRANSPORT_COMPONENT', 'TRANSPORT_SERVICE', 'ADDED_BLOCK', 'CROP' |
| `enterprise_id` | BIGINT | Identificativo dell'impresa a cui appartiene il componente | `42` | FK | No | Punta all'id dell'entità [enterprise](enterprise.md) |
| `insured` | BOOLEAN | Indica se il componente è coperto da assicurazione | `True` | - | No | - |
| `name` | VARCHAR | Nome o denominazione del componente | `Warehouse A` | - | No | - |
| `country` | VARCHAR | Paese in cui si trova il componente | `Italy` | - | No | - |
| `state` | VARCHAR | Stato o regione in cui si trova il componente | `Lazio` | - | No | - |
| `county` | VARCHAR | Contea o provincia in cui si trova il componente | `Rome` | - | No | - |
| `town` | VARCHAR | Comune in cui si trova il componente | `Rome` | - | No | - |
| `hamlet` | VARCHAR | Frazione o località in cui si trova il componente | `Trastevere` | - | No | - |
| `road` | VARCHAR | Via in cui si trova il componente | `Via Appia` | - | No | - |
| `house_number` | VARCHAR | Numero civico del componente | `10` | - | No | - |
| `postcode` | VARCHAR | Codice postale del componente | `00100` | - | No | - |
| `details` | VARCHAR | Ulteriori dettagli dell'indirizzo del componente | `Building B, second floor` | - | No | - |
| `geometry` | GEOMETRY | Rappresentazione spaziale dell'entità componente | [...] | - | Sì | - |
| `coordinates_inferred` | BOOLEAN | Indica se le coordinate del componente sono state dedotte anziché misurate direttamente | [...] | - | No | - |
| `cultural_heritage` | BOOLEAN | Indica se il componente è un bene del patrimonio culturale | [...] | - | No | - |

## Relazioni

Poiché `component` è una delle entità centrali dello schema, ha numerose relazioni:

* **Ha sottotipi (ereditarietà):** Le tabelle seguenti ereditano da `component` e condividono il suo `id`:
    * [`added_block`](added_block.md)
    * [`artistic_good`](artistic_good.md)
    * [`agriculture_product`](agriculture_product.md), che ha propri sottotipi [`crop`](crop.md) e [`stored`](stored.md)
    * [`building_component`](building_component.md)
    * [`building_functionality`](building_functionality.md)
    * [`business_operations`](business_operations.md)
    * [`electrical_network_component`](electrical_network_component.md)
    * [`fixed_asset`](fixed_asset.md), che ha propri sottotipi [`infrastructure`](infrastructure.md), [`land`](land.md), [`machinery`](machinery.md) e [`material`](material.md)
    * [`livestock`](livestock.md)
    * [`network_service`](network_service.md)
    * [`product`](product.md)
    * [`provision`](provision.md)
    * [`staff`](staff.md)
    * [`tlc_network_component`](tlc_network_component.md)
    * [`transport_network_component`](transport_network_component.md)
* **Appartiene a:** [`enterprise`](enterprise.md) (Un componente è collegato a una sola impresa)
* **Ha molti:** [`damage`](damage.md) (Un componente può subire più danni nel tempo)
