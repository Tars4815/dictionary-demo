# Tabela: `crop`

!!! warning "Tradução assistida por IA"
    Esta página foi traduzida com a assistência de inteligência artificial e pode conter erros. A versão em inglês é a referência. Os nomes das tabelas e dos atributos são idênticos em todas as línguas porque correspondem aos da implementação PostgreSQL.

**Descrição (PT):** Esta tabela representa as culturas. Na arquitetura de herança da base de dados, funciona como subtipo direto da tabela [`agriculture_product`](agriculture_product.md). Não armazena colunas descritivas redundantes: em vez disso, utiliza uma chave primária partilhada para herdar todos os atributos de alto nível (como nome, localização, tipo de gestão e geometria) do seu registo principal `component`.

## Estrutura das colunas

| Coluna | Tipo de dados | Definição | Exemplo de valor | Restrição? | Geometria? | Comentários |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Identificador único do registo da cultura | `42` | PK, FK | Não | Chave primária que funciona também como chave estrangeira a referenciar `agriculture_product.id` e, por sua vez, `component.id` |
| `area_planted` | BIGINT | [...] | [...] | - | Não | [...] |
| `category` | VARCHAR | [...] | [...] | - | Não | [...] |
| `growth` | VARCHAR | [...] | [...] | - | Não | [...] |
| `duration` | VARCHAR | [...] | [...] | - | Não | [...] |

## Relações

* **Herda de (subtipo de):** [`agriculture_product`](agriculture_product.md). A tabela `crop` é uma extensão especializada da tabela `agriculture_product`.
* **Pertence a:** [`enterprise`](enterprise.md) (Um subtipo de componente está associado a uma única empresa)
* **Tem muitos:** `damage` (Um subtipo de componente pode sofrer vários danos ao longo do tempo)

!!! tip "Onde está o resto dos dados?"
    Para encontrar o nome, a localização geográfica (`geometry`, `town`, `country`) ou os detalhes de propriedade de uma cultura, tem de juntar esta tabela ao registo `component` que partilha o mesmo `id`.

## Consulta de exemplo

Obtenha uma lista de todas as culturas, incluindo nomes, municípios e coordenadas espaciais, juntando a tabela à respetiva entidade-mãe `component`:

```sql
SELECT
    c.id,
    c.area_planted,
    c.category,
    ap.year_production 
FROM 
    crop c join agriculture_product ap on c.id = ap.id 
where ap.subtype = 'CROP'
```