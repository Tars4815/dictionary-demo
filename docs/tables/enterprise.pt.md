# Tabela: `enterprise`

!!! warning "Tradução assistida por IA"
    Esta página foi traduzida com a assistência de inteligência artificial e pode conter erros. A versão em inglês é a referência. Os nomes das tabelas e dos atributos são idênticos em todas as línguas porque correspondem aos da implementação PostgreSQL.

**Descrição (PT):** Esta é a entidade-mãe central (superclasse) da base de dados. Armazena os atributos universais de alto nível, como a identificação, a localização geográfica e os dados administrativos, de todos os principais ativos físicos ou empresariais. Os tipos específicos de empresas (como [edifícios](building.md), [empresas comerciais](business.md), [explorações agrícolas](farm.md) ou [sistemas de rede](network_system.md)) armazenam os seus dados especializados em subtabelas separadas que partilham o mesmo ID. A propriedade não é armazenada aqui: está registada na tabela de ligação [`enterprise_owner`](enterprise_owner.md).

## Estrutura das colunas

| Coluna | Tipo de dados | Definição | Exemplo de valor | Restrição? | Geometria? | Comentários |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Identificador único da empresa | `3` | PK | Não | Funciona como ID universal para todas as tabelas de subtipos |
| `type` | VARCHAR(255) | Coluna discriminadora que define o tipo específico de empresa | `BUILDING` | NOT NULL | Não | Valores atualmente presentes nos dados: 'BUILDING', 'FARM', 'TRANSPORT', 'TELECOMMUNICATION' |
| `name` | VARCHAR(255) | Nome oficial ou denominação da empresa | `Main Headquarters` |  | Não |  |
| `management_type` | VARCHAR(255) | Tipo de gestão ou de administração da empresa | `PUBLIC` |  | Não | e.g., 'PUBLIC', 'PRIVATE', 'MIXED' |
| `vat` | VARCHAR(255) | Número de IVA da empresa | `IT00000000000` |  | Não |  |
| `description` | VARCHAR(255) | Descrição em texto livre da empresa | `Regional hospital` |  | Não |  |
| `country` | VARCHAR(255) | País onde a empresa se situa | `Italy` |  | Não |  |
| `state` | VARCHAR(255) | Estado ou região onde a empresa se situa | `Lazio` |  | Não |  |
| `county` | VARCHAR(255) | Condado ou província onde a empresa se situa | `Rome` |  | Não |  |
| `town` | VARCHAR(255) | Município onde a empresa se situa | `Rome` |  | Não |  |
| `hamlet` | VARCHAR(255) | Lugar ou localidade onde a empresa se situa | `Trastevere` |  | Não |  |
| `road` | VARCHAR(255) | Rua onde a empresa se situa | `Via Appia` |  | Não |  |
| `house_number` | VARCHAR(255) | Número de porta da empresa | `10` |  | Não |  |
| `postcode` | VARCHAR(255) | Código postal da empresa | `00100` |  | Não |  |
| `geometry` | GEOMETRY | Representação espacial da empresa | `POINT(12.49 41.89)` |  | Sim | EPSG:4326. Pode ser um ponto ou um polígono, consoante a escala |
| `coordinates_inferred` | BOOLEAN | Indica se as coordenadas da empresa foram inferidas em vez de medidas diretamente | [...] |  | Não |  |

## Relações

Dado que `enterprise` é o eixo central do esquema, tem numerosas relações:

* **Tem subtipos (herança):** As tabelas seguintes herdam de `enterprise` e partilham o seu `id`:
    * [`building`](building.md)
    * [`business`](business.md)
    * [`farm`](farm.md)
    * [`network_system`](network_system.md)
* **É detida por:** [`owner`](owner.md). Uma empresa pode ter vários proprietários e um proprietário pode deter várias empresas. Esta relação muitos-para-muitos é assegurada pela tabela de ligação [`enterprise_owner`](enterprise_owner.md).
* **Tem muitos:** [`component`](component.md) (Uma empresa é composta por vários subcomponentes, como maquinaria, culturas ou redes elétricas)
* **Tem muitos:** [`survey`](survey.md) (Uma empresa pode ser objeto de vários danos ou levantamentos de avaliação ao longo do tempo)

## Consulta de exemplo

Obtenha uma lista de todas as empresas situadas num município específico, mostrando o seu nome, a sua classificação específica (tipo) e as suas coordenadas:

```sql
SELECT 
    id, 
    name, 
    type, 
    ST_AsText(geometry) as coordinates 
FROM 
    enterprise 
WHERE 
    town = 'Rome'
ORDER BY 
    type ASC;
```

Obtenha os proprietários de cada empresa através da tabela de ligação:

```sql
SELECT 
    e.id, 
    e.name, 
    o.full_name 
FROM 
    enterprise e
JOIN 
    enterprise_owner eo ON eo.enterprise_id = e.id
JOIN 
    owner o ON o.id = eo.owner_id;
```
