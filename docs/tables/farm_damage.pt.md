# Tabela: `farm_damage`

!!! warning "Tradução assistida por IA"
    Esta página foi traduzida com a assistência de inteligência artificial e pode conter erros. A versão em inglês é a referência. Os nomes das tabelas e dos atributos são idênticos em todas as línguas porque correspondem aos da implementação PostgreSQL.

**Descrição (PT):** Esta tabela representa os danos comunicados em explorações agrícolas. Na arquitetura de herança da base de dados, funciona como subtipo direto da tabela [`damage`](damage.md). Não armazena colunas descritivas redundantes: em vez disso, utiliza uma chave primária partilhada para herdar todos os atributos de alto nível (como descrição, datas, localização e geometria) do seu registo principal `damage`.

## Estrutura das colunas

| Coluna | Tipo de dados | Definição | Exemplo de valor | Restrição? | Geometria? | Comentários |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Identificador único do dano a uma exploração agrícola | `42` | PK, FK | Não | Chave primária que funciona também como chave estrangeira a referenciar `damage.id` |

## Relações

* **Herda de (subtipo de):** [`damage`](damage.md). A tabela `farm_damage` é uma extensão especializada da tabela `damage`.
* **Afeta:** [`component`](component.md) (Um ou mais danos afetam um componente ou as suas subclasses)
* **É comunicado por:** [`survey`](survey.md) (Um ou mais danos são comunicados num levantamento)
* **Comunicado em:** [`attachment`](attachment.md) (Um dano é comunicado em um ou mais anexos)
* **Resulta em:** [`economic_loss`](economic_loss.md)
* **Tem subtipos (herança):** As tabelas seguintes herdam de `farm_damage` e partilham o seu `id`:
    * [`damage_agriculture_product`](damage_agriculture_product.md)
    * [`damage_fixed_asset`](damage_fixed_asset.md)
    * [`damage_livestock`](damage_livestock.md)
    * [`damage_provision`](damage_provision.md)
    * [`damage_staff`](damage_staff.md)

!!! tip "Onde está o resto dos dados?"
    Para encontrar a descrição, as datas, a localização geográfica (`geometry`, `town`, `country`) ou outros detalhes de um dano a explorações agrícolas, tem de juntar esta tabela ao registo `damage` que partilha o mesmo `id`.

## Consulta de exemplo

Obtenha uma lista de todos os danos a explorações agrícolas, incluindo descrições, municípios e coordenadas espaciais, juntando a tabela à respetiva entidade-mãe `damage`:

```sql
SELECT
    fd.*,
    d.*
FROM 
    farm_damage fd JOIN damage d ON fd.id = d.id;
```
