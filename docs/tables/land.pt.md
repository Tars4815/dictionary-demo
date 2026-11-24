# Tabela: `land`

!!! warning "Tradução assistida por IA"
    Esta página foi traduzida com a assistência de inteligência artificial e pode conter erros. A versão em inglês é a referência. Os nomes das tabelas e dos atributos são idênticos em todas as línguas porque correspondem aos da implementação PostgreSQL.

**Descrição (PT):** Esta tabela representa os terrenos. Na arquitetura de herança da base de dados, funciona como subtipo direto da tabela [`fixed_asset`](fixed_asset.md). Não armazena colunas descritivas redundantes: em vez disso, utiliza uma chave primária partilhada para herdar todos os atributos de alto nível (como nome, localização, tipo de gestão e geometria) do seu registo principal `component`.

## Estrutura das colunas

| Coluna | Tipo de dados | Definição | Exemplo de valor | Restrição? | Geometria? | Comentários |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Identificador único dos registos de terrenos | `42` | PK, FK | Não | Chave primária que funciona também como chave estrangeira a referenciar `fixed_asset.id` e, por sua vez, `component.id` |
| `dimension` | BIGINT | [...] | [...] | - | Não | [...] |
| `value` | BIGINT | [...] | [...] | - | Não | [...] |
| `soil` | VARCHAR | [...] | [...] | - | Não | [...] |
| `configuration` | VARCHAR | [...] | [...] | - | Não | [...] |
| `function` | VARCHAR | [...] | [...] | - | Não | [...] |

## Relações

* **Herda de (subtipo de):** [`fixed_asset`](fixed_asset.md). A tabela `land` é uma extensão especializada da tabela `fixed_asset`.
* **Pertence a:** [`enterprise`](enterprise.md) (Um subtipo de componente está associado a uma única empresa)
* **Tem muitos:** `damage` (Um subtipo de componente pode sofrer vários danos ao longo do tempo)

!!! tip "Onde está o resto dos dados?"
    Para encontrar o nome, a localização geográfica (`geometry`, `town`, `country`) ou os detalhes de propriedade de um registo de terreno, tem de juntar esta tabela ao registo `component` que partilha o mesmo `id`.

## Consulta de exemplo

Obtenha uma lista de todos os terrenos, incluindo nomes, municípios e coordenadas espaciais, juntando a tabela à respetiva entidade-mãe `component`:

```sql
SELECT l.* FROM public.land AS l
```