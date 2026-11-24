# Tabela: `building`

!!! warning "Tradução assistida por IA"
    Esta página foi traduzida com a assistência de inteligência artificial e pode conter erros. A versão em inglês é a referência. Os nomes das tabelas e dos atributos são idênticos em todas as línguas porque correspondem aos da implementação PostgreSQL.

**Descrição (PT):** Esta tabela representa os edifícios. Na arquitetura de herança da base de dados, funciona como subtipo direto da tabela [`enterprise`](enterprise.md). Não armazena colunas descritivas redundantes: em vez disso, utiliza uma chave primária partilhada para herdar todos os atributos de alto nível (como nome, localização, tipo de gestão e geometria) do seu registo principal `enterprise`.

As características estruturais, económicas e físicas de um edifício (ano de construção, materiais, número de pisos, custo, etc.) são armazenadas na tabela [`building_component`](building_component.md).

## Estrutura das colunas

| Coluna | Tipo de dados | Definição | Exemplo de valor | Restrição? | Geometria? | Comentários |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Identificador único do edifício | `3` | PK, FK | Não | Chave primária que funciona também como chave estrangeira a referenciar `enterprise.id` |

## Relações

* **Herda de (subtipo de):** [`enterprise`](enterprise.md). A tabela `building` é uma extensão especializada da tabela `enterprise`.
* **Contém:** Embora não esteja ligado diretamente através de `building_id`, um edifício possui as suas partes físicas através da coluna `enterprise_id` da tabela `component`. Estes componentes incluem frequentemente subtipos especializados, tais como:
    * [`building_component`](building_component.md)
    * [`added_block`](added_block.md)
    * [`building_functionality`](building_functionality.md)

!!! tip "Onde está o resto dos dados?"
    Para encontrar o nome, a localização geográfica (`geometry`, `town`, `country`) ou o NIF de um edifício, tem de juntar esta tabela ao registo `enterprise` que partilha o mesmo `id`. As características estruturais e económicas encontram-se em `building_component`, que está ligada ao edifício através de `component.enterprise_id`.

## Consulta de exemplo

Obtenha as características de cada edifício juntando o respetivo registo de empresa aos seus componentes de edifício:

```sql
SELECT
    e.name,
    e.town,
    bc.n_floors,
    bc.construction_cost,
    bc.economic_value
FROM
    building b
JOIN
    enterprise e ON b.id = e.id
JOIN
    component c ON c.enterprise_id = e.id
JOIN
    building_component bc ON bc.id = c.id
WHERE
    e.type = 'BUILDING';
```
