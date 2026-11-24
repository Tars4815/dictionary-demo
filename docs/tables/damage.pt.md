# Tabela: `damage`

!!! warning "Tradução assistida por IA"
    Esta página foi traduzida com a assistência de inteligência artificial e pode conter erros. A versão em inglês é a referência. Os nomes das tabelas e dos atributos são idênticos em todas as línguas porque correspondem aos da implementação PostgreSQL.

**Descrição (PT):** Esta tabela armazena os atributos universais de alto nível, como a identificação e a localização geográfica, de todos os danos ocorridos na sequência de um evento. Os tipos específicos de danos (como [danos a bens artísticos](damage_artistic_good.md), [danos à funcionalidade dos edifícios](damage_building_functionality.md) ou outros) armazenam os seus dados especializados em subtabelas separadas que partilham o mesmo ID.

## Estrutura das colunas

| Coluna | Tipo de dados | Definição | Exemplo de valor | Restrição? | Geometria? | Comentários |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Identificador único do dano | `3` | PK | Não | Funciona como ID universal para todas as tabelas de subtipos |
| `estimated_value` | BIGINT | [...] | - | - | Não | - |
| `component_id` | BIGINT | [...] | - | FK | Não | Aponta para o id da entidade [component](component.md) |
| `date` | TIMESTAMP | [...] | [...] | - | Não | - |
| `end_date` | TIMESTAMP | [...] | [...] | - | Não | - |
| `start_end` | TIMESTAMP | [...] | [...] | - | Não | - |
| `survey_id` | BIGINT | [...] | [...] | FK | Não | Aponta para o id da entidade [survey](survey.md) |
| `country` | VARCHAR | [...] | [...] | - | Não | - |
| `county` | VARCHAR | [...] | [...] | - | Não | - |
| `description` | VARCHAR | [...] | [...] | - | Não | - |
| `hamlet` | VARCHAR | [...] | [...] | - | Não | - |
| `house_number` | VARCHAR | [...] | [...] | - | Não | - |
| `postcode` | VARCHAR | [...] | [...] | - | Não | - |
| `road` | VARCHAR | [...] | [...] | - | Não | - |
| `state` | VARCHAR | [...] | [...] | - | Não | - |
| `town` | VARCHAR | [...] | [...] | - | Não | - |
| `geometry` | GEOMETRY | Representação espacial da entidade dano | [...] | - | Não | - |
| `coordinates_inferred` | BOOLEAN | [...] | [...] | - | Não | - |
| `sendai_indicator` | VARCHAR | [...] | [...] | - | Não | - |

## Relações

Dado que `damage` é uma das entidades centrais do esquema, tem numerosas relações:

* **Tem subtipos (herança):** As tabelas seguintes herdam de `damage` e partilham o seu `id`:
    * [`damage_artistic_good`](damage_artistic_good.md)
    * [`damage_building_functionality`](damage_building_functionality.md)
    * [`damage_building_not_structural`](damage_building_not_structural.md)
    * [`damage_building_structural`](damage_building_structural.md)
    * [`damage_business_operations`](damage_business_operations.md)
    * [`damage_church_structure`](damage_church_structure.md)
    * [`damage_goods`](damage_goods.md)
    * [`damage_network_component`](damage_network_component.md)
    * [`damage_network_service`](damage_network_service.md)
    * [`damage_people`](damage_people.md)
    * [`damage_product`](damage_product.md)
    * [`damage_vehicles`](damage_vehicles.md)
    * [`damage_whole_structure`](damage_whole_structure.md)
    * [`farm_damage`](farm_damage.md)
* **Afeta:** [`component`](component.md) (Um ou mais danos afetam um componente ou as suas subclasses)
* **É registado por:** [`survey`](survey.md) (Um ou mais danos são comunicados num levantamento)
* **Está documentado em:** [`attachment`](attachment.md) (Um dano é comunicado em um ou mais anexos)
* **Resulta em:** [`economic_loss`](economic_loss.md)