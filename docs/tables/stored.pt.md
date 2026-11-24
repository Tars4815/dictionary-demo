# Tabela: `stored`

!!! warning "Tradução assistida por IA"
    Esta página foi traduzida com a assistência de inteligência artificial e pode conter erros. A versão em inglês é a referência. Os nomes das tabelas e dos atributos são idênticos em todas as línguas porque correspondem aos da implementação PostgreSQL.

**Descrição (PT):** Esta tabela representa os produtos armazenados. Na arquitetura de herança da base de dados, funciona como subtipo direto da tabela [`agriculture_product`](agriculture_product.md). Não armazena colunas descritivas redundantes: em vez disso, utiliza uma chave primária partilhada para herdar todos os atributos de alto nível (como nome, localização, tipo de gestão e geometria) do seu registo principal `component`.

## Estrutura das colunas

| Coluna | Tipo de dados | Definição | Exemplo de valor | Restrição? | Geometria? | Comentários |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Identificador único dos produtos agrícolas armazenados | `42` | PK, FK | Não | Chave primária que funciona também como chave estrangeira a referenciar `agriculture_product.id` e, por sua vez, `component.id` |
| `total_stored` | BIGINT | [...] | [...] | - | Não | [...] |

## Relações

* **Herda de (subtipo de):** [`agriculture_product`](agriculture_product.md). A tabela `crop` é uma extensão especializada da tabela `agriculture_product`.
* **Pertence a:** [`enterprise`](enterprise.md) (Um subtipo de componente está associado a uma única empresa)
* **Tem muitos:** `damage` (Um subtipo de componente pode sofrer vários danos ao longo do tempo)

!!! tip "Onde está o resto dos dados?"
    Para encontrar o nome, a localização geográfica (`geometry`, `town`, `country`) ou os detalhes de propriedade de um produto armazenado, tem de juntar esta tabela ao registo `component` que partilha o mesmo `id`.

## Consulta de exemplo

Obtenha uma lista de todos os registos de produtos armazenados, incluindo nomes, municípios e coordenadas espaciais, juntando a tabela à respetiva entidade-mãe `enterprise`:

```sql
SELECT s.* FROM public."stored" AS s
```