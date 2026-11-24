# Tabela: `business`

!!! info "Nome diferente na interface web (GUI)"
    No backend PostgreSQL, esta tabela chama-se `business`, como indicado no título da página. Na interface da aplicação web aparece como **Economic Activities - Business**. Todos os aliases estão na [tabela de correspondência](../backend-to-gui.md).

!!! warning "Tradução assistida por IA"
    Esta página foi traduzida com a assistência de inteligência artificial e pode conter erros. A versão em inglês é a referência. Os nomes das tabelas e dos atributos são idênticos em todas as línguas porque correspondem aos da implementação PostgreSQL.

**Descrição (PT):** Esta tabela representa as empresas comerciais. Na arquitetura de herança da base de dados, funciona como subtipo direto da tabela [`enterprise`](enterprise.md). Não armazena colunas descritivas redundantes: em vez disso, utiliza uma chave primária partilhada para herdar todos os atributos de alto nível (como nome, localização, tipo de gestão e geometria) do seu registo principal `enterprise`.

## Estrutura das colunas

| Coluna | Tipo de dados | Definição | Exemplo de valor | Restrição? | Geometria? | Comentários |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Identificador único do registo da empresa comercial | `8` | PK, FK | Não | Chave primária que funciona também como chave estrangeira a referenciar `enterprise.id` |
| `share_capital` | BIGINT | Valor monetário total dos fundos da sociedade | [...] | - | Não | [...] |
| `nace_section` | VARCHAR | Classificação de nível superior da principal atividade económica da empresa comercial, de acordo com a norma NACE | [...] | - | Não | [...] |

## Relações

* **Herda de (subtipo de):** [`enterprise`](enterprise.md). A tabela `business` é uma extensão especializada da tabela `enterprise`.
* **Contém:** Embora não esteja ligado diretamente através de `business_id`, um sistema de rede possui ativos de infraestrutura através da coluna `enterprise_id` da tabela `component`. Estes componentes incluem frequentemente subtipos especializados, tais como:
    * `business_operations`

!!! tip "Onde está o resto dos dados?"
    Para encontrar o nome, a localização geográfica (`geometry`, `town`, `country`) ou os detalhes de propriedade de um sistema de rede, tem de juntar esta tabela ao registo `enterprise` que partilha o mesmo `id`.

## Consulta de exemplo

Obtenha uma lista de todos os registos de empresas comerciais, incluindo nomes, municípios e coordenadas espaciais, juntando a tabela à respetiva entidade-mãe `enterprise`:

```sql
SELECT 
    b.id, 
    e.name, 
    e.town, 
    ST_AsText(e.geometry) as coordinates 
FROM 
    business b
JOIN 
    enterprise e ON b.id = e.id
WHERE 
    e.type = 'BUSINESS';
```