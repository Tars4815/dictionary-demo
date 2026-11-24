# Tabela: `farm`

!!! info "Nome diferente na interface web (GUI)"
    No backend PostgreSQL, esta tabela chama-se `farm`, como indicado no título da página. Na interface da aplicação web aparece como **Economic Activities - Farm**. Todos os aliases estão na [tabela de correspondência](../backend-to-gui.md).

!!! warning "Tradução assistida por IA"
    Esta página foi traduzida com a assistência de inteligência artificial e pode conter erros. A versão em inglês é a referência. Os nomes das tabelas e dos atributos são idênticos em todas as línguas porque correspondem aos da implementação PostgreSQL.

**Descrição (PT):** Esta tabela representa as empresas agrícolas. Na arquitetura de herança da base de dados, funciona como subtipo direto da tabela [`enterprise`](enterprise.md). Não armazena colunas descritivas redundantes: em vez disso, utiliza uma chave primária partilhada para herdar todos os atributos de alto nível (como nome, localização, tipo de gestão e geometria) do seu registo principal `enterprise`.

## Estrutura das colunas

| Coluna | Tipo de dados | Definição | Exemplo de valor | Restrição? | Geometria? | Comentários |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Identificador único da exploração agrícola | `42` | PK, FK | Não | Chave primária que funciona também como chave estrangeira a referenciar `enterprise.id` |

## Relações

* **Herda de (subtipo de):** [`enterprise`](enterprise.md). A tabela `farm` é uma extensão especializada da tabela `enterprise`.
* **Contém:** Embora não esteja ligada diretamente através de `farm_id`, uma exploração agrícola possui ativos agrícolas através da coluna `enterprise_id` da tabela `component`. Estes componentes incluem frequentemente subtipos agrícolas especializados, tais como:
    * [`agriculture_product`](agriculture_product.md) e os seus subtipos [`crop`](crop.md) e [`stored`](stored.md)
    * [`livestock`](livestock.md)
    * [`fixed_asset`](fixed_asset.md) e os seus subtipos (p. ex. [`machinery`](machinery.md), como tratores)

!!! tip "Onde está o resto dos dados?"
    Para encontrar o nome, a localização geográfica (`geometry`, `town`, `country`) ou outros detalhes de uma exploração agrícola, tem de juntar esta tabela ao registo `enterprise` que partilha o mesmo `id`.

## Consulta de exemplo

Obtenha uma lista de todas as explorações agrícolas, incluindo nomes, municípios e coordenadas espaciais, juntando a tabela à respetiva entidade-mãe `enterprise`:

```sql
SELECT 
    f.id, 
    e.name, 
    e.town, 
    ST_AsText(e.geometry) as coordinates 
FROM 
    farm f
JOIN 
    enterprise e ON f.id = e.id
WHERE 
    e.type = 'FARM';
```
