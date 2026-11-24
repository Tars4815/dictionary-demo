# Tabela: `transport_network_component`

!!! info "Nome diferente na interface web (GUI)"
    No backend PostgreSQL, esta tabela chama-se `transport_network_component`, como indicado no título da página. Na interface da aplicação web aparece como **Transport element**. Todos os aliases estão na [tabela de correspondência](../backend-to-gui.md).

!!! warning "Tradução assistida por IA"
    Esta página foi traduzida com a assistência de inteligência artificial e pode conter erros. A versão em inglês é a referência. Os nomes das tabelas e dos atributos são idênticos em todas as línguas porque correspondem aos da implementação PostgreSQL.

**Descrição (PT):** Esta tabela representa os componentes da rede de transporte. Na arquitetura de herança da base de dados, funciona como subtipo direto da tabela [`component`](component.md). Não armazena colunas descritivas redundantes: em vez disso, utiliza uma chave primária partilhada para herdar todos os atributos de alto nível (como nome, localização, tipo de gestão e geometria) do seu registo principal `component`.

## Estrutura das colunas

| Coluna | Tipo de dados | Definição | Exemplo de valor | Restrição? | Geometria? | Comentários |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Identificador único do componente da rede de transporte | `42` | PK, FK | Não | Chave primária que funciona também como chave estrangeira a referenciar `component.id` |
| `is_private` | BOOLEAN | [...] | [...] | - | Não | - |
| `lanes_number` | BIGINT | [...] | [...] | - | Não | - |
| `subtype` | VARCHAR | [...] | [...] | - | Não | Valores possíveis: PRIMARY_ROAD, PROVINCIAL, COUNTRY_SIDE |

## Relações

* **Herda de (subtipo de):** [`component`](component.md). A tabela `transport_network_component` é uma extensão especializada da tabela `component`.
* **Pertence a:** [`enterprise`](enterprise.md) (Um subtipo de componente está associado a uma única empresa)
* **Tem muitos:** `damage` (Um subtipo de componente pode sofrer vários danos ao longo do tempo)

!!! tip "Onde está o resto dos dados?"
    Para encontrar o nome, a localização geográfica (`geometry`, `town`, `country`) ou os detalhes de propriedade de um componente da rede de transporte, tem de juntar esta tabela ao registo `component` que partilha o mesmo `id`.

## Consulta de exemplo

Obtenha uma lista de todos os componentes da rede de transporte, incluindo nomes, municípios e coordenadas espaciais, juntando a tabela à respetiva entidade-mãe `component`:

```sql
 tnc2.id, 
    c.name, 
    c.town, 
    ST_AsText(c.geometry) as coordinates 
FROM 
    transport_network_component tnc2
JOIN 
    component c ON tnc2.id = c.id
```