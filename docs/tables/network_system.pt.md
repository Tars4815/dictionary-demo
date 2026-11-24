# Tabela: `network_system`

!!! warning "Tradução assistida por IA"
    Esta página foi traduzida com a assistência de inteligência artificial e pode conter erros. A versão em inglês é a referência. Os nomes das tabelas e dos atributos são idênticos em todas as línguas porque correspondem aos da implementação PostgreSQL.

**Descrição (PT):** Esta tabela representa os sistemas de rede de infraestrutura (p. ex. redes de transporte, elétricas ou de telecomunicações). Na arquitetura de herança da base de dados, funciona como subtipo direto da tabela [`enterprise`](enterprise.md). Não armazena colunas descritivas redundantes: em vez disso, utiliza uma chave primária partilhada para herdar todos os atributos de alto nível (como nome, localização, tipo de gestão e geometria) do seu registo principal `enterprise`.

## Estrutura das colunas

| Coluna | Tipo de dados | Definição | Exemplo de valor | Restrição? | Geometria? | Comentários |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Identificador único do sistema de rede | `8` | PK, FK | Não | Chave primária que funciona também como chave estrangeira a referenciar `enterprise.id` |

## Relações

* **Herda de (subtipo de):** [`enterprise`](enterprise.md). A tabela `network_system` é uma extensão especializada da tabela `enterprise`.
* **Tem subtipos (herança):** As tabelas seguintes herdam de `network_system` (e, através dela, de `enterprise`) e partilham o seu `id`:
    * [`electrical_system`](electrical_system.md)
    * [`tlc_system`](tlc_system.md)
    * [`transport_system`](transport_system.md)
* **Contém:** Embora não esteja ligado diretamente através de `network_system_id`, um sistema de rede possui ativos de infraestrutura através da coluna `enterprise_id` da tabela `component`. Estes componentes incluem frequentemente subtipos especializados, tais como:
    * `transport_network_component`
    * `electrical_network_component`
    * `tlc_network_component`
    * `network_service`

!!! tip "Onde está o resto dos dados?"
    Para encontrar o nome, a localização geográfica (`geometry`, `town`, `country`) ou outros detalhes de um sistema de rede, tem de juntar esta tabela ao registo `enterprise` que partilha o mesmo `id`.

## Consulta de exemplo

Obtenha uma lista de todos os sistemas de rede, incluindo nomes, municípios e coordenadas espaciais, juntando a tabela à respetiva entidade-mãe `enterprise`:

```sql
SELECT 
    n.id, 
    e.name, 
    e.town, 
    e.type,
    ST_AsText(e.geometry) as coordinates 
FROM 
    network_system n
JOIN 
    enterprise e ON n.id = e.id;
```
