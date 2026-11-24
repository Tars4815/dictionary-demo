# Tabela: `event`

!!! warning "Tradução assistida por IA"
    Esta página foi traduzida com a assistência de inteligência artificial e pode conter erros. A versão em inglês é a referência. Os nomes das tabelas e dos atributos são idênticos em todas as línguas porque correspondem aos da implementação PostgreSQL.

**Descrição (PT):** Esta tabela armazena as informações e os detalhes relativos a um evento importante específico.

## Estrutura das colunas

| Coluna | Tipo de dados | Definição | Exemplo de valor | Restrição? | Geometria? | Comentários |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Identificador único do evento | `3` | PK | Não | [...] |
| `date` | TIMESTAMP | Momento de ocorrência do evento | [...] | - | Não | [...] |
| `date_end` | TIMESTAMP | Momento de fim do evento | [...] | - | Não | [...] |
| `parent_event_id` | BIGINT | Referência em caso de evento múltiplo | [...] | FK | Não | Aponta para o id da entidade [event](event.md) |
| `name` | VARCHAR | Nome do evento | `Storm Example` | - | Não | - |
| `severity` | VARCHAR | Nível de gravidade do evento | [...] | - | Não | - |
| `type` | VARCHAR | Tipo de evento | [...] | - | Não | - |
| `country` | VARCHAR | País onde o evento se situa | `Italy` | - | Não | - |
| `state` | VARCHAR | Estado ou região onde o evento se situa | `Lazio` | - | Não | - |
| `county` | VARCHAR | Condado ou província onde o evento se situa | `Rome` | - | Não | - |
| `town` | VARCHAR | Município onde o evento se situa | `Rome` | - | Não | - |
| `hamlet` | VARCHAR | Lugar ou localidade onde o evento se situa | `Trastevere` | - | Não | - |
| `road` | VARCHAR | Rua onde o evento se situa | `Via Appia` | - | Não | - |
| `house_number` | VARCHAR | Número de porta do evento | `10` | - | Não | - |
| `postcode` | VARCHAR | Código postal do evento | `00100` | - | Não | - |
| `geometry` | GEOMETRY | Representação espacial do evento | [...] | - | Sim | - |
| `coordinates_inferred` | BOOLEAN | Indica se as coordenadas do evento foram inferidas em vez de medidas diretamente | [...] | - | Não | - |

## Relações

* **Tem muitos:** [`survey`](survey.md) (Um evento pode ser seguido de vários levantamentos de avaliação dos danos)
* **Faz parte de / tem partes:** [`event`](event.md) através de `parent_event_id`. Um evento múltiplo pode ser dividido em eventos filhos que apontam para o evento principal.
