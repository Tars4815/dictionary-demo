# Tabela: `damage_provision`

!!! warning "Tradução assistida por IA"
    Esta página foi traduzida com a assistência de inteligência artificial e pode conter erros. A versão em inglês é a referência. Os nomes das tabelas e dos atributos são idênticos em todas as línguas porque correspondem aos da implementação PostgreSQL.

**Descrição (PT):** Esta tabela representa os danos comunicados em provisões. Na arquitetura de herança da base de dados, funciona como subtipo direto da tabela [`farm_damage`](farm_damage.md), que é ela própria um subtipo de [`damage`](damage.md). Não armazena colunas descritivas redundantes: em vez disso, utiliza uma chave primária partilhada para herdar todos os atributos de alto nível (como descrição, datas, localização e geometria) do seu registo principal `damage`.

## Estrutura das colunas

| Coluna | Tipo de dados | Definição | Exemplo de valor | Restrição? | Geometria? | Comentários |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Identificador único do dano a provisões | `42` | PK, FK | Não | Chave primária que funciona também como chave estrangeira a referenciar `farm_damage.id` (e, por sua vez, `damage.id`) |
| `additional_food` | INTEGER | Custo adicional de alimentação | [...] | - | Não | - |
| `additional_veterinary` | INTEGER | Custo veterinário adicional | [...] | - | Não | - |
| `losses_fees` | INTEGER | Perdas em taxas | [...] | - | Não | - |
| `losses_premature_sale` | INTEGER | Perdas por venda antecipada | [...] | - | Não | - |
| `losses_value` | INTEGER | Valor das perdas | [...] | - | Não | - |
| `relocation_cost` | INTEGER | Custo de realojamento | [...] | - | Não | - |
| `replanting_cost` | INTEGER | Custo de replantação | [...] | - | Não | - |
| `additional_materials` | INTEGER | Custo de materiais adicionais | [...] | - | Não | - |
| `restoration_cost` | INTEGER | Custo de restauro | [...] | - | Não | - |

## Relações

* **Herda de (subtipo de):** [`farm_damage`](farm_damage.md), que por sua vez herda de [`damage`](damage.md). A tabela `damage_provision` é uma extensão especializada da tabela `farm_damage`.
* **Afeta:** [`component`](component.md) (Um ou mais danos afetam um componente ou as suas subclasses)
* **É comunicado por:** [`survey`](survey.md) (Um ou mais danos são comunicados num levantamento)
* **Comunicado em:** [`attachment`](attachment.md) (Um dano é comunicado em um ou mais anexos)
* **Resulta em:** [`economic_loss`](economic_loss.md)

!!! tip "Onde está o resto dos dados?"
    Para encontrar a descrição, as datas, a localização geográfica (`geometry`, `town`, `country`) ou outros detalhes de um dano a provisões, tem de juntar esta tabela ao registo `damage` que partilha o mesmo `id`.

## Consulta de exemplo

Obtenha uma lista de todos os danos a provisões, incluindo descrições, municípios e coordenadas espaciais, juntando a tabela à respetiva entidade-mãe `damage`:

```sql
SELECT
    dp.*,
    d.*
FROM 
    damage_provision dp JOIN damage d ON dp.id = d.id;
```
