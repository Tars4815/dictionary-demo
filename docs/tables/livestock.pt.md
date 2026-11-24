# Tabela: `livestock`

!!! warning "Tradução assistida por IA"
    Esta página foi traduzida com a assistência de inteligência artificial e pode conter erros. A versão em inglês é a referência. Os nomes das tabelas e dos atributos são idênticos em todas as línguas porque correspondem aos da implementação PostgreSQL.

**Descrição (PT):** Esta tabela representa os componentes do tipo gado. Na arquitetura de herança da base de dados, funciona como subtipo direto da tabela [`component`](component.md). Não armazena colunas descritivas redundantes: em vez disso, utiliza uma chave primária partilhada para herdar todos os atributos de alto nível (como nome, localização, tipo de gestão e geometria) do seu registo principal `component`.

## Estrutura das colunas

| Coluna | Tipo de dados | Definição | Exemplo de valor | Restrição? | Geometria? | Comentários |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Identificador único do gado | `42` | PK, FK | Não | Chave primária que funciona também como chave estrangeira a referenciar `component.id` |
| `age` | BIGINT | [...] | `2` | - | Não | - |
| `breeding_cost` | BIGINT | [...] | `2` | - | Não | - |
| `gate_price` | BIGINT | [...] | `2` | - | Não | - |
| `weight` | BIGINT | [...] | `2` | - | Não | - |
| `year_production` | BIGINT | [...] | `2` | - | Não | - |
| `subtype` | VARCHAR | [...] | - | - | Não | - |
| `purpose` | VARCHAR | [...] | - | - | Não | - |

## Relações

* **Herda de (subtipo de):** [`component`](component.md). A tabela `livestock` é uma extensão especializada da tabela `component`.
* **Pertence a:** [`enterprise`](enterprise.md) (Um subtipo de componente está associado a uma única empresa)
* **Tem muitos:** `damage` (Um subtipo de componente pode sofrer vários danos ao longo do tempo)

!!! tip "Onde está o resto dos dados?"
    Para encontrar o nome, a localização geográfica (`geometry`, `town`, `country`) ou os detalhes de propriedade de um animal de criação, tem de juntar esta tabela ao registo `component` que partilha o mesmo `id`.

## Consulta de exemplo

Obtenha uma lista de todos os registos de gado, incluindo nomes, municípios e coordenadas espaciais, juntando a tabela à respetiva entidade-mãe `component`:

```sql
SELECT 
    l.id, 
    c.name, 
    c.town, 
    ST_AsText(c.geometry) as coordinates 
FROM 
    livestock l
JOIN 
    component c ON l.id = c.id
WHERE 
    c.component_kind  = 'LIVESTOCK';
```