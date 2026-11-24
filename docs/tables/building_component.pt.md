# Tabela: `building_component`

!!! warning "Tradução assistida por IA"
    Esta página foi traduzida com a assistência de inteligência artificial e pode conter erros. A versão em inglês é a referência. Os nomes das tabelas e dos atributos são idênticos em todas as línguas porque correspondem aos da implementação PostgreSQL.

**Descrição (PT):** Esta tabela armazena as características estruturais, económicas e físicas dos edifícios, incluindo os detalhes de construção, os tipos de material e as dimensões. Na arquitetura de herança da base de dados, funciona como subtipo direto da tabela [`component`](component.md). Não armazena colunas descritivas redundantes: em vez disso, utiliza uma chave primária partilhada para herdar todos os atributos de alto nível (como nome, localização e geometria) do seu registo principal `component`.

## Estrutura das colunas

| Coluna | Tipo de dados | Definição | Exemplo de valor | Restrição? | Geometria? | Comentários |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Identificador único do componente de edifício | `42` | PK, FK | Não | Chave primária que funciona também como chave estrangeira a referenciar `component.id` |
| `principal` | BOOLEAN | Indica se se trata do componente de edifício principal | `true` | - | Não | [...] |
| `subtype` | VARCHAR(255) | [...] | [...] | - | Não | [...] |
| `public_service_code` | VARCHAR(255) | [...] | [...] | - | Não | [...] |
| `heritage_tier` | VARCHAR(255) | [...] | [...] | - | Não | [...] |
| `year` | INTEGER | Ano de construção | `1999` | - | Não |  |
| `quality` | VARCHAR(255) | Qualidade global | `GOOD` | - | Não | Valores possíveis: POOR, GOOD, ACCEPTABLE, NOT_IDENTIFIABLE |
| `conservation` | VARCHAR(255) | Estado de conservação do edifício | `POORLY_MANTAINED` | CHECK | Não | Valores possíveis: POORLY_MANTAINED, MODERATELY_MAINTAINED, WELL_MAINTAINED, NOT_IDENTIFIABLE |
| `retrofitting` | VARCHAR(255) | Estado do reforço (retrofitting) | `NOT_IDENTIFIABLE` | CHECK | Não | Valores possíveis: NONE, VERTICAL, HORIZONTAL, COMPLETE, NOT_IDENTIFIABLE, etc. |
| `regularity` | VARCHAR(255) | Regularidade da estrutura | `NOT_IDENTIFIABLE` | CHECK | Não | Valores possíveis: NOT_REGULAR, COMPLETELY_REGULAR, etc. |
| `inhabitants` | INTEGER | Número de habitantes do edifício em causa | `6` | - | Não |  |
| `construction_cost` | INTEGER | Custo de construção | `500000` | - | Não |  |
| `economic_value` | INTEGER | Valor económico | `1000000` | - | Não |  |
| `vertical_mat` | VARCHAR(255) | Material de construção das estruturas verticais | `NOT_IDENTIFIABLE` | CHECK | Não | Valores possíveis: STEEL, WOOD, MASONRY_ADOBE, etc. |
| `horizontal_mat` | VARCHAR(255) | Material de construção das estruturas horizontais | `MASONRY_ADOBE` | CHECK | Não | Valores possíveis: STEEL, WOOD, MASONRY_ADOBE, etc. |
| `roof_mat` | VARCHAR(255) | Material do elemento de cobertura | `NOT_IDENTIFIABLE` | CHECK | Não | Valores possíveis: STEEL, WOOD, MASONRY_ADOBE, etc. |
| `build_position` | VARCHAR(255) | Posição do edifício | `SINGLE_DETACHED` | CHECK | Não | Valores possíveis: SINGLE_DETACHED, SEMI_DETACHED, ROW, NOT_IDENTIFICABLE |
| `ground_floor` | VARCHAR(255) | Tipologia do rés do chão | `OPEN` | CHECK | Não | Valores possíveis: OPEN, CLOSE, NOT_IDENTIFIABLE |
| `n_floors` | INTEGER | Número de pisos acima do solo | `3` | - | Não |  |
| `floor_height` | INTEGER | Altura média dos pisos | `4` | - | Não |  |
| `n_under_floors` | INTEGER | Número de pisos subterrâneos | `1` | - | Não |  |
| `floor_area` | INTEGER | Superfície dos pisos em metros quadrados | `1000` | - | Não |  |
| `usage` | VARCHAR(255) | [...] | [...] | - | Não | [...] |
| `foundation_typology` | VARCHAR(255) | Tipologia das fundações | [...] | - | Não | [...] |
| `main_use` | VARCHAR(255) | Utilização principal do edifício | [...] | - | Não | [...] |

## Relações

* **Herda de (subtipo de):** [`component`](component.md). A tabela `building_component` é uma extensão especializada da tabela `component`.
* **Pertence a:** [`enterprise`](enterprise.md) (Um subtipo de componente está associado a uma única empresa)
* **Tem muitos:** `damage` (Um subtipo de componente pode sofrer vários danos ao longo do tempo)

!!! tip "Onde está o resto dos dados?"
    Para encontrar o nome, a localização geográfica (`geometry`, `town`, `country`) ou os detalhes de propriedade de um componente de edifício, tem de juntar esta tabela ao registo `component` que partilha o mesmo `id`.

## Consulta de exemplo

Obtenha uma lista de todos os componentes de edifício, incluindo nomes, municípios e coordenadas espaciais, juntando a tabela à respetiva entidade-mãe `component`:

```sql
SELECT 
    bc.id, 
    c.name, 
    c.town, 
    ST_AsText(c.geometry) as coordinates 
FROM 
    building_component bc
JOIN 
    component c ON bc.id = c.id
WHERE 
    c.component_kind = 'BUILDING_COMPONENT';
```
