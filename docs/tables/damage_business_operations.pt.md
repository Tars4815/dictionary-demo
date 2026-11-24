# Tabela: `damage_business_operations`

!!! warning "Tradução assistida por IA"
    Esta página foi traduzida com a assistência de inteligência artificial e pode conter erros. A versão em inglês é a referência. Os nomes das tabelas e dos atributos são idênticos em todas as línguas porque correspondem aos da implementação PostgreSQL.

**Descrição (PT):** Esta tabela representa os danos estruturais às operações empresariais. Na arquitetura de herança da base de dados, funciona como subtipo direto da tabela [`damage`](damage.md). Não armazena colunas descritivas redundantes: em vez disso, utiliza uma chave primária partilhada para herdar todos os atributos de alto nível (como nome, localização, tipo de gestão e geometria) do seu registo principal `damage`.

## Estrutura das colunas

| Coluna | Tipo de dados | Definição | Exemplo de valor | Restrição? | Geometria? | Comentários |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Identificador único do dano às operações empresariais | `42` | PK, FK | Não | Chave primária que funciona também como chave estrangeira a referenciar `damage.id` |
| `disruption_type` | VARCHAR | [...] | [...] | - | Não | [...] |
| `disruption_level` | VARCHAR | [...] | [...] | - | Não | [...] |

## Relações

* **Herda de (subtipo de):** [`damage`](damage.md). A tabela `damage_business_operations` é uma extensão especializada da tabela `damage`.
* **Afeta:** [`component`](component.md) (Um ou mais danos afetam um componente ou as suas subclasses)
* **É comunicado por:** [`survey`](survey.md) (Um ou mais danos são comunicados num levantamento)
* **Comunicado em:** [`attachment`](attachment.md) (Um dano é comunicado em um ou mais anexos)
* **Resulta em:** [`economic_loss`](economic_loss.md)

!!! tip "Onde está o resto dos dados?"
    Para encontrar o nome, a localização geográfica (`geometry`, `town`, `country`) ou outros detalhes de um dano às operações empresariais, tem de juntar esta tabela ao registo `damage` que partilha o mesmo `id`.

## Consulta de exemplo

Obtenha uma lista de todos os danos às operações empresariais, incluindo descrições, municípios e coordenadas espaciais, juntando a tabela à respetiva entidade-mãe `damage`:

```sql
SELECT
    dbo.*,
    d.*
FROM 
    damage_business_operations dbo    join damage d on dbo.id = d.id
```