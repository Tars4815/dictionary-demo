# Tabela: `damage_staff`

!!! warning "Tradução assistida por IA"
    Esta página foi traduzida com a assistência de inteligência artificial e pode conter erros. A versão em inglês é a referência. Os nomes das tabelas e dos atributos são idênticos em todas as línguas porque correspondem aos da implementação PostgreSQL.

**Descrição (PT):** Esta tabela representa os danos comunicados no pessoal das explorações agrícolas. Na arquitetura de herança da base de dados, funciona como subtipo direto da tabela [`farm_damage`](farm_damage.md), que é ela própria um subtipo de [`damage`](damage.md). Não armazena colunas descritivas redundantes: em vez disso, utiliza uma chave primária partilhada para herdar todos os atributos de alto nível (como descrição, datas, localização e geometria) do seu registo principal `damage`.

## Estrutura das colunas

| Coluna | Tipo de dados | Definição | Exemplo de valor | Restrição? | Geometria? | Comentários |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Identificador único do dano ao pessoal de uma exploração agrícola | `42` | PK, FK | Não | Chave primária que funciona também como chave estrangeira a referenciar `farm_damage.id` (e, por sua vez, `damage.id`) |
| `duration_of_absence` | INTEGER | Duração da ausência do pessoal | [...] | - | Não | - |
| `number_of_absent` | INTEGER | Número de membros do pessoal ausentes | [...] | - | Não | - |
| `number_of_dead` | INTEGER | Número de membros do pessoal mortos | [...] | - | Não | - |
| `number_of_injured` | INTEGER | Número de membros do pessoal feridos | [...] | - | Não | - |
| `further_details` | VARCHAR | Mais detalhes sobre o dano ao pessoal | [...] | - | Não | - |
| `reason_of_absence` | VARCHAR | Motivo da ausência | [...] | - | Não | - |
| `number_of_missing` | INTEGER | Número de membros do pessoal desaparecidos | [...] | - | Não | - |

## Relações

* **Herda de (subtipo de):** [`farm_damage`](farm_damage.md), que por sua vez herda de [`damage`](damage.md). A tabela `damage_staff` é uma extensão especializada da tabela `farm_damage`.
* **Afeta:** [`component`](component.md) (Um ou mais danos afetam um componente ou as suas subclasses)
* **É comunicado por:** [`survey`](survey.md) (Um ou mais danos são comunicados num levantamento)
* **Comunicado em:** [`attachment`](attachment.md) (Um dano é comunicado em um ou mais anexos)
* **Resulta em:** [`economic_loss`](economic_loss.md)

!!! tip "Onde está o resto dos dados?"
    Para encontrar a descrição, as datas, a localização geográfica (`geometry`, `town`, `country`) ou outros detalhes de um dano ao pessoal, tem de juntar esta tabela ao registo `damage` que partilha o mesmo `id`.

## Consulta de exemplo

Obtenha uma lista de todos os danos ao pessoal, incluindo descrições, municípios e coordenadas espaciais, juntando a tabela à respetiva entidade-mãe `damage`:

```sql
SELECT
    ds.*,
    d.*
FROM 
    damage_staff ds JOIN damage d ON ds.id = d.id;
```
