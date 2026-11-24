# Tabela: `survey`

!!! warning "Tradução assistida por IA"
    Esta página foi traduzida com a assistência de inteligência artificial e pode conter erros. A versão em inglês é a referência. Os nomes das tabelas e dos atributos são idênticos em todas as línguas porque correspondem aos da implementação PostgreSQL.

**Descrição (PT):** Esta tabela armazena as informações e os detalhes relativos a um levantamento específico de avaliação de danos, realizado na sequência de um evento importante.

## Estrutura das colunas

| Coluna | Tipo de dados | Definição | Exemplo de valor | Restrição? | Geometria? | Comentários |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Identificador único do levantamento | `3` | PK | Não | [...] |
| `created_on` | TIMESTAMP | Momento de realização do levantamento de avaliação | [...] | NOT NULL | Não | [...] |
| `enterprise_id` | BIGINT | Chave estrangeira que remete para uma empresa | [...] | FK | Não | Aponta para o id da entidade [enterprise](enterprise.md) |
| `event_id` | BIGINT | Momento de realização do levantamento de avaliação | [...] | FK | Não | Aponta para o id da entidade [event](event.md) |

## Relações

Dado que `survey` é uma das entidades centrais do esquema, tem numerosas relações:

* **Comunica** [`damage`](damage.md)
* **Está ligado a** [`enterprise`](enterprise.md)
* **Sucede a um** [`event`](event.md)