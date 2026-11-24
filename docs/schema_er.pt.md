# Visão geral do esquema

!!! warning "Tradução assistida por IA"
    Esta página foi traduzida com a assistência de inteligência artificial e pode conter erros. A versão em inglês é a referência. Os nomes das tabelas e dos atributos são idênticos em todas as línguas porque correspondem aos da implementação PostgreSQL.

O esquema `public` está organizado em três grupos de tabelas:

1. **Empresas**: as unidades detidas e localizadas que podem sofrer danos (edifícios, explorações agrícolas, empresas comerciais, sistemas de rede).
2. **Componentes**: os elementos físicos ou económicos que pertencem a uma empresa (culturas, maquinaria, pessoal, troços de estrada, etc.).
3. **Avaliação**: eventos, levantamentos e os registos de danos que estes originam.

As empresas e os componentes usam ambos a **herança com uma tabela por subtipo**: a tabela de um subtipo partilha a chave primária da tabela-mãe, pelo que uma linha é associada à sua tabela-mãe com `child.id = parent.id`.

O esquema é apresentado em três diagramas para que cada um se mantenha legível.

## 1. Empresas e propriedade

```mermaid
erDiagram
    OWNER ||--o{ ENTERPRISE : "possui"
    ENTERPRISE ||--o| BUILDING : "é um"
    ENTERPRISE ||--o| BUSINESS : "é um"
    ENTERPRISE ||--o| FARM : "é um"
    ENTERPRISE ||--o| NETWORK_SYSTEM : "é um"
    NETWORK_SYSTEM ||--o| ELECTRICAL_SYSTEM : "é um"
    NETWORK_SYSTEM ||--o| TLC_SYSTEM : "é um"
    NETWORK_SYSTEM ||--o| TRANSPORT_SYSTEM : "é um"
    ENTERPRISE ||--o{ COMPONENT : "contém"
    ENTERPRISE ||--o{ SURVEY : "é sujeito a"

```
## 2. Componentes e respetivos subtipos

```mermaid
erDiagram
    ENTERPRISE ||--o{ COMPONENT : "contém"
    COMPONENT ||--o{ DAMAGE : "sofre"

    COMPONENT ||--o| ADDED_BLOCK : "é um"
    COMPONENT ||--o| ARTISTIC_GOOD : "é um"
    COMPONENT ||--o| BUILDING_COMPONENT : "é um"
    COMPONENT ||--o| BUILDING_FUNCTIONALITY : "é um"
    COMPONENT ||--o| BUSINESS_OPERATIONS : "é um"
    COMPONENT ||--o| LIVESTOCK : "é um"
    COMPONENT ||--o| NETWORK_SERVICE : "é um"
    COMPONENT ||--o| PRODUCT : "é um"
    COMPONENT ||--o| PROVISION : "é um"
    COMPONENT ||--o| STAFF : "é um"
    COMPONENT ||--o| ELECTRICAL_NETWORK_COMPONENT : "é um"
    COMPONENT ||--o| TLC_NETWORK_COMPONENT : "é um"
    COMPONENT ||--o| TRANSPORT_NETWORK_COMPONENT : "é um"

    COMPONENT ||--o| AGRICULTURE_PRODUCT : "é um"
    AGRICULTURE_PRODUCT ||--o| CROP : "é um"
    AGRICULTURE_PRODUCT ||--o| STORED : "é um"

    COMPONENT ||--o| FIXED_ASSET : "é um"
    FIXED_ASSET ||--o| INFRASTRUCTURE : "é um"
    FIXED_ASSET ||--o| LAND : "é um"
    FIXED_ASSET ||--o| MACHINERY : "é um"
    FIXED_ASSET ||--o| MATERIAL : "é um"

```
## 3. Interações entre entidades

```mermaid
erDiagram
    EVENT ||--o{ SURVEY : "desencadeia"
    ENTERPRISE ||--o{ SURVEY : "é sujeito a"
    SURVEY ||--o{ DAMAGE : "reporta"
    COMPONENT ||--o{ DAMAGE : "sofre"
    ENTERPRISE ||--o{ COMPONENT : "contém"
    EVENT ||--o{ EVENT : "ligado"
    DAMAGE ||--o{ ECONOMIC_LOSS : "tem"
    OWNER ||--o{ ENTERPRISE_OWNER : "possui"
    ENTERPRISE ||--o{ ENTERPRISE_OWNER : "é possuído por"

```

### Legenda das relações
* `||--o{` : **Um-para-muitos**. *Exemplo: uma empresa contém muitos componentes.*
* `||--||` : **Um-para-um**. *Exemplo: o registo Building é uma extensão direta de um registo Enterprise.*
* `}o--||` : **Muitos-para-um**. *Exemplo: muitas empresas podem pertencer a um único proprietário.*