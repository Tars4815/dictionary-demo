# Tabela: `attachment`

!!! warning "Tradução assistida por IA"
    Esta página foi traduzida com a assistência de inteligência artificial e pode conter erros. A versão em inglês é a referência. Os nomes das tabelas e dos atributos são idênticos em todas as línguas porque correspondem aos da implementação PostgreSQL.

**Descrição (PT):** Esta tabela armazena as informações e os detalhes relativos a um anexo.

## Estrutura das colunas

| Coluna | Tipo de dados | Definição | Exemplo de valor | Restrição? | Geometria? | Comentários |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Identificador único do anexo | `3` | PK | Não | [...] |
| `damage_id` | BIGINT | Chave estrangeira que remete para um dano comunicado | [...] | FK | Não | Aponta para o id da entidade [damage](damage.md) |
| `date` | TIMESTAMP | [...] | - | - | Não | - |
| `size` | BIGINT | [...] | - | - | Não | - |
| `description` | VARCHAR | [...] | - | - | Não | - |
| `name` | VARCHAR | [...] | - | - | Não | - |
| `type` | VARCHAR | [...] | - | - | Não | - |
| `data` | BIGINT | [...] | - | - | Não | - |

## Relações

* **Documentos** [`damage`](damage.md)