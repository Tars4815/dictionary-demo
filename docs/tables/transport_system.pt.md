# Tabela: `transport_system`

!!! info "Nome diferente na interface web (GUI)"
    No backend PostgreSQL, esta tabela chama-se `transport_system`, como indicado no título da página. Na interface da aplicação web aparece como **Lifelines - Transport**. Todos os aliases estão na [tabela de correspondência](../backend-to-gui.md).

!!! warning "Tradução assistida por IA"
    Esta página foi traduzida com a assistência de inteligência artificial e pode conter erros. A versão em inglês é a referência. Os nomes das tabelas e dos atributos são idênticos em todas as línguas porque correspondem aos da implementação PostgreSQL.

**Descrição (PT):** Esta tabela representa os sistemas de rede de transporte. Na arquitetura de herança da base de dados, funciona como subtipo direto da tabela [`network_system`](network_system.md). Não armazena colunas descritivas redundantes: em vez disso, utiliza uma chave primária partilhada para herdar todos os atributos de alto nível (como nome, localização, tipo de gestão e geometria) do seu registo principal `network_system`, que por sua vez é filho de um registo [`enterprise`](enterprise.md).

## Estrutura das colunas

| Coluna | Tipo de dados | Definição | Exemplo de valor | Restrição? | Geometria? | Comentários |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Identificador único do sistema de rede de transporte | `8` | PK, FK | Não | Chave primária que funciona também como chave estrangeira a referenciar `network_system.id` e `enterprise.id` |

## Relações

* **Herda de (subtipo de):** [`network_system`](network_system.md). A tabela `electrical_system` é uma extensão especializada da tabela `network_system`.
* **Contém:** Embora não esteja ligado diretamente através de `transport_system_id`, um sistema de transporte possui ativos de infraestrutura através da coluna `enterprise_id` da tabela `component`. Estes componentes incluem frequentemente subtipos especializados, tais como:
    * `transport_network_component`

!!! tip "Onde está o resto dos dados?"
    Para encontrar o nome, a localização geográfica (`geometry`, `town`, `country`) ou os detalhes de propriedade de um sistema de rede, tem de juntar esta tabela ao registo `enterprise` que partilha o mesmo `id`.

## Consulta de exemplo

Obtenha uma lista de todos os sistemas elétricos, incluindo nomes, municípios e coordenadas espaciais, juntando a tabela à respetiva entidade-mãe `network_system` - `enterprise`:

```sql
SELECT 
    tr.id, 
    e.name, 
    e.town, 
    ST_AsText(e.geometry) as coordinates 
FROM 
    transport_system tr
JOIN 
    enterprise e ON tr.id = e.id
WHERE 
    e.type = 'TRANSPORT';