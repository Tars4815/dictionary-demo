# Tabela: `enterprise_owner`

!!! warning "Tradução assistida por IA"
    Esta página foi traduzida com a assistência de inteligência artificial e pode conter erros. A versão em inglês é a referência. Os nomes das tabelas e dos atributos são idênticos em todas as línguas porque correspondem aos da implementação PostgreSQL.

**Descrição (PT):** Esta entidade funciona como tabela de ligação para a relação muitos-para-muitos entre [`enterprise`](enterprise.md) e [`owner`](owner.md).

## Estrutura das colunas

| Coluna | Tipo de dados | Definição | Exemplo de valor | Restrição? | Geometria? | Comentários |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `enterprise_id` | BIGINT | Identificador da empresa | `3` | FK | Não | Remete para a tabela `enterprise` |
| `owner_id` | BIGINT | Identificador do proprietário | `8` | FK | Não | Remete para a tabela `owner` |


