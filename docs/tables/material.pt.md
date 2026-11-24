# Tabela: `material`

!!! warning "Tradução assistida por IA"
    Esta página foi traduzida com a assistência de inteligência artificial e pode conter erros. A versão em inglês é a referência. Os nomes das tabelas e dos atributos são idênticos em todas as línguas porque correspondem aos da implementação PostgreSQL.

**Descrição (PT):** Esta tabela representa os materiais. Na arquitetura de herança da base de dados, funciona como subtipo direto da tabela [`fixed_asset`](fixed_asset.md). Não armazena colunas descritivas redundantes: em vez disso, utiliza uma chave primária partilhada para herdar todos os atributos de alto nível (como nome, localização, tipo de gestão e geometria) do seu registo principal `component`.

## Estrutura das colunas

| Coluna | Tipo de dados | Definição | Exemplo de valor | Restrição? | Geometria? | Comentários |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Identificador único do registo de material | `42` | PK, FK | Não | Chave primária que funciona também como chave estrangeira a referenciar `fixed_asset.id` e, por sua vez, `component.id` |
| `value` | BIGINT | [...] | [...] | - | Não | [...] |
| `quantity` | VARCHAR | [...] | [...] | - | Não | [...] |
| `material_type` | VARCHAR | [...] | [...] | - | Não | [...] |
| `hazardous` | BOOLEAN | [...] | [...] | - | Não | [...] |

## Relações

* **Herda de (subtipo de):** [`fixed_asset`](fixed_asset.md). A tabela `material` é uma extensão especializada da tabela `fixed_asset`.
* **Pertence a:** [`enterprise`](enterprise.md) (Um subtipo de componente está associado a uma única empresa)
* **Tem muitos:** `damage` (Um subtipo de componente pode sofrer vários danos ao longo do tempo)

!!! tip "Onde está o resto dos dados?"
    Para encontrar o nome, a localização geográfica (`geometry`, `town`, `country`) ou os detalhes de propriedade de um registo de material, tem de juntar esta tabela ao registo `component` que partilha o mesmo `id`.

## Consulta de exemplo

Obtenha uma lista de todos os materiais, incluindo nomes, municípios e coordenadas espaciais, juntando a tabela à respetiva entidade-mãe `component`:

```sql
SELECT m.* FROM public.material AS m
```