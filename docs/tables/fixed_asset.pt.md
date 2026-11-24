# Tabela: `fixed_asset`

!!! info "Nome diferente na interface web (GUI)"
    No backend PostgreSQL, esta tabela chama-se `fixed_asset`, como indicado no título da página. Na interface da aplicação web aparece como **Elements**. Todos os aliases estão na [tabela de correspondência](../backend-to-gui.md).

!!! warning "Tradução assistida por IA"
    Esta página foi traduzida com a assistência de inteligência artificial e pode conter erros. A versão em inglês é a referência. Os nomes das tabelas e dos atributos são idênticos em todas as línguas porque correspondem aos da implementação PostgreSQL.

**Descrição (PT):** Esta tabela representa os componentes do tipo ativo imobilizado. Na arquitetura de herança da base de dados, funciona como subtipo direto da tabela [`component`](component.md). Não armazena colunas descritivas redundantes: em vez disso, utiliza uma chave primária partilhada para herdar todos os atributos de alto nível (como nome, localização, tipo de gestão e geometria) do seu registo principal `component`.

## Estrutura das colunas

| Coluna | Tipo de dados | Definição | Exemplo de valor | Restrição? | Geometria? | Comentários |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Identificador único do componente do tipo ativo imobilizado | `42` | PK, FK | Não | Chave primária que funciona também como chave estrangeira a referenciar `component.id` |

## Relações

* **Herda de (subtipo de):** [`component`](component.md). A tabela `fixed_asset` é uma extensão especializada da tabela `component`.
* **Tem subtipos (herança):** As tabelas seguintes herdam de `fixed_asset` e partilham o seu `id`:
    * [`infrastructure`](infrastructure.md)
    * [`land`](land.md)
    * [`machinery`](machinery.md)
    * [`material`](material.md)
* **Pertence a:** [`enterprise`](enterprise.md) (Um subtipo de componente está associado a uma única empresa)
* **Tem muitos:** `damage` (Um subtipo de componente pode sofrer vários danos ao longo do tempo)

!!! tip "Onde está o resto dos dados?"
    Para encontrar o nome, a localização geográfica (`geometry`, `town`, `country`) ou os detalhes de propriedade de um registo fixed_asset, tem de juntar esta tabela ao registo `component` que partilha o mesmo `id`.

## Consulta de exemplo

Obtenha uma lista de todos os ativos imobilizados, incluindo nomes, municípios e coordenadas espaciais, juntando a tabela à respetiva entidade-mãe `enterprise`:

```sql
SELECT 
    fa.id, 
    c.name, 
    c.town, 
    ST_AsText(c.geometry) as coordinates 
FROM 
    fixed_asset
JOIN 
    component c ON fa.id = c.id
WHERE 
    c.component_kind  = 'FIXED_ASSET';
```