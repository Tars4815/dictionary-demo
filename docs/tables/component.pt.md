# Tabela: `component`

!!! info "Nome diferente na interface web (GUI)"
    No backend PostgreSQL, esta tabela chama-se `component`, como indicado no título da página. Na interface da aplicação web aparece como **Elements & production (all subclasses)**. Todos os aliases estão na [tabela de correspondência](../backend-to-gui.md).

!!! warning "Tradução assistida por IA"
    Esta página foi traduzida com a assistência de inteligência artificial e pode conter erros. A versão em inglês é a referência. Os nomes das tabelas e dos atributos são idênticos em todas as línguas porque correspondem aos da implementação PostgreSQL.

**Descrição (PT):** Esta tabela armazena os atributos universais de alto nível, como a identificação e a localização geográfica, de todos os principais componentes físicos ou empresariais. Os tipos específicos de componentes (como [corpos adicionados](added_block.md), [bens artísticos](artistic_good.md) ou outros) armazenam os seus dados especializados em subtabelas separadas que partilham o mesmo ID.

## Estrutura das colunas

| Coluna | Tipo de dados | Definição | Exemplo de valor | Restrição? | Geometria? | Comentários |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Identificador único do componente | `3` | PK | Não | Funciona como ID universal para todas as tabelas de subtipos |
| `component_kind` | VARCHAR | Coluna discriminadora que identifica o subtipo específico do componente | `BUILDING_COMPONENT` | NOT NULL | Não | Contém o tipo mais específico. Valores atualmente presentes nos dados: 'BUILDING_COMPONENT', 'TRANSPORT_COMPONENT', 'TRANSPORT_SERVICE', 'ADDED_BLOCK', 'CROP' |
| `enterprise_id` | BIGINT | Identificador da empresa a que o componente pertence | `42` | FK | Não | Aponta para o id da entidade [enterprise](enterprise.md) |
| `insured` | BOOLEAN | Indica se o componente está coberto por um seguro | `True` | - | Não | - |
| `name` | VARCHAR | Nome ou denominação do componente | `Warehouse A` | - | Não | - |
| `country` | VARCHAR | País onde o componente se situa | `Italy` | - | Não | - |
| `state` | VARCHAR | Estado ou região onde o componente se situa | `Lazio` | - | Não | - |
| `county` | VARCHAR | Condado ou província onde o componente se situa | `Rome` | - | Não | - |
| `town` | VARCHAR | Município onde o componente se situa | `Rome` | - | Não | - |
| `hamlet` | VARCHAR | Lugar ou localidade onde o componente se situa | `Trastevere` | - | Não | - |
| `road` | VARCHAR | Rua onde o componente se situa | `Via Appia` | - | Não | - |
| `house_number` | VARCHAR | Número de porta do componente | `10` | - | Não | - |
| `postcode` | VARCHAR | Código postal do componente | `00100` | - | Não | - |
| `details` | VARCHAR | Detalhes adicionais da morada do componente | `Building B, second floor` | - | Não | - |
| `geometry` | GEOMETRY | Representação espacial da entidade componente | [...] | - | Sim | - |
| `coordinates_inferred` | BOOLEAN | Indica se as coordenadas do componente foram inferidas em vez de medidas diretamente | [...] | - | Não | - |
| `cultural_heritage` | BOOLEAN | Indica se o componente é um bem do património cultural | [...] | - | Não | - |

## Relações

Dado que `component` é uma das entidades centrais do esquema, tem numerosas relações:

* **Tem subtipos (herança):** As tabelas seguintes herdam de `component` e partilham o seu `id`:
    * [`added_block`](added_block.md)
    * [`artistic_good`](artistic_good.md)
    * [`agriculture_product`](agriculture_product.md), que tem os seus próprios subtipos [`crop`](crop.md) e [`stored`](stored.md)
    * [`building_component`](building_component.md)
    * [`building_functionality`](building_functionality.md)
    * [`business_operations`](business_operations.md)
    * [`electrical_network_component`](electrical_network_component.md)
    * [`fixed_asset`](fixed_asset.md), que tem os seus próprios subtipos [`infrastructure`](infrastructure.md), [`land`](land.md), [`machinery`](machinery.md) e [`material`](material.md)
    * [`livestock`](livestock.md)
    * [`network_service`](network_service.md)
    * [`product`](product.md)
    * [`provision`](provision.md)
    * [`staff`](staff.md)
    * [`tlc_network_component`](tlc_network_component.md)
    * [`transport_network_component`](transport_network_component.md)
* **Pertence a:** [`enterprise`](enterprise.md) (Um componente está associado a uma única empresa)
* **Tem muitos:** [`damage`](damage.md) (Um componente pode sofrer vários danos ao longo do tempo)
