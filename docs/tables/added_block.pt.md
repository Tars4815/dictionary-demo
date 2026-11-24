# Tabela: `added_block`

!!! info "Nome diferente na interface web (GUI)"
    No backend PostgreSQL, esta tabela chama-se `added_block`, como indicado no título da página. Na interface da aplicação web aparece como **Added block**. Todos os aliases estão na [tabela de correspondência](../backend-to-gui.md).

!!! warning "Tradução assistida por IA"
    Esta página foi traduzida com a assistência de inteligência artificial e pode conter erros. A versão em inglês é a referência. Os nomes das tabelas e dos atributos são idênticos em todas as línguas porque correspondem aos da implementação PostgreSQL.

**Descrição (PT):** Esta tabela representa os corpos adicionados dos edifícios. Na arquitetura de herança da base de dados, funciona como subtipo direto da tabela [`component`](component.md). Não armazena colunas descritivas redundantes: em vez disso, utiliza uma chave primária partilhada para herdar todos os atributos de alto nível (como nome, localização, tipo de gestão e geometria) do seu registo principal `component`.

## Estrutura das colunas

| Coluna | Tipo de dados | Definição | Exemplo de valor | Restrição? | Geometria? | Comentários |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Identificador único do corpo adicionado | `42` | PK, FK | Não | Chave primária que funciona também como chave estrangeira a referenciar `component.id` |
| `position` | VARCHAR | [...] | `EXTERNAL` | - | Não | [...] |
| `vertical_mat` | VARCHAR | [...] | [...] | - | Não | [...] |
| `horizontal_mat` | VARCHAR | [...] | [...] | - | Não | [...] |
| `n_floor` | BIGINT | Número de pisos do corpo adicionado | `2` | - | Não | [...] |
| `total_height` | BIGINT | Altura total do corpo adicionado em [unidade de medida] | `200` | - | Não | [...] |
| `floor_surface` | BIGINT | Superfície total dos pisos do corpo adicionado em [unidade de medida] | `200` | - | Não | [...] |
| `floor_height` | BIGINT | Altura total dos pisos do corpo adicionado em [unidade de medida] | `200` | - | Não | [...] |
| `function` | VARCHAR | [...] | [...] | - | Não | [...] |
| `previous_survey` | VARCHAR | [...] | [...] | - | Não | [...] |

## Relações

* **Herda de (subtipo de):** [`component`](component.md). A tabela `added_block` é uma extensão especializada da tabela `component`.
* **Pertence a:** [`enterprise`](enterprise.md) (Um subtipo de componente está associado a uma única empresa)
* **Tem muitos:** `damage` (Um subtipo de componente pode sofrer vários danos ao longo do tempo)

!!! tip "Onde está o resto dos dados?"
    Para encontrar o nome, a localização geográfica (`geometry`, `town`, `country`) ou os detalhes de propriedade de um registo added_block, tem de juntar esta tabela ao registo `component` que partilha o mesmo `id`.

## Consulta de exemplo

Obtenha uma lista de todos os corpos adicionados, incluindo nomes, municípios e coordenadas espaciais, juntando a tabela à respetiva entidade-mãe `component`:

```sql
SELECT 
    ab.id, 
    c.name, 
    c.town, 
    ST_AsText(c.geometry) as coordinates 
FROM 
    added_block ab
JOIN 
    component c ON ab.id = c.id
WHERE 
    c.component_kind  = 'ADDED_BLOCK';
```