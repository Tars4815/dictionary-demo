# Tabela: `economic_loss`

!!! warning "Tradução assistida por IA"
    Esta página foi traduzida com a assistência de inteligência artificial e pode conter erros. A versão em inglês é a referência. Os nomes das tabelas e dos atributos são idênticos em todas as línguas porque correspondem aos da implementação PostgreSQL.

**Descrição (PT):** Esta tabela armazena os custos associados a um dano comunicado: os montantes estimados, aprovados e finais.

## Estrutura das colunas

| Coluna | Tipo de dados | Definição | Exemplo de valor | Restrição? | Geometria? | Comentários |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Identificador único do registo de perda económica | `3` | PK | Não | [...] |
| `damage_id` | BIGINT | Chave estrangeira que remete para um dano comunicado | [...] | FK | Não | Aponta para o id da entidade [damage](damage.md) |
| `approved_cost` | DOUBLE PRECISION | Custo aprovado para o dano | - | - | Não | - |
| `estimated_cost` | DOUBLE PRECISION | Custo estimado do dano | - | - | Não | - |
| `final_cost` | DOUBLE PRECISION | Custo final do dano | - | - | Não | - |
| `type_of_cost` | VARCHAR | Tipo de custo | - | - | Não | - |

## Relações

* **Remete para:** [`damage`](damage.md) através de `damage_id`. A perda económica é o resultado monetário de um dano comunicado.

## Consulta de exemplo

Obtenha os custos registados para cada dano:

```sql
SELECT 
    d.id AS damage_id, 
    el.type_of_cost, 
    el.estimated_cost, 
    el.approved_cost, 
    el.final_cost 
FROM 
    economic_loss el
JOIN 
    damage d ON el.damage_id = d.id;
```
