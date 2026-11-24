# Terminologia da interface gráfica do utilizador (GUI)

!!! warning "Tradução assistida por IA"
    Esta página foi traduzida com a assistência de inteligência artificial e pode conter erros. A versão em inglês é a referência. Os nomes das tabelas e dos atributos são idênticos em todas as línguas porque correspondem aos da implementação PostgreSQL.

A [aplicação web do AHEAD](https://ahead-impact.app/lode/) utiliza alias para as entidades envolvidas no preenchimento dos formulários pelos utilizadores. Para facilitar a compreensão das ligações subjacentes à base de dados, esta secção inclui uma tabela que associa os termos da interface gráfica aos nomes das entidades na base de dados PostgreSQL, em apoio da replicabilidade e da transparência do sistema.

---

## Correspondência entre o backend e a aplicação web

| Nome da entidade na base de dados | Alias no sítio web |
| :--- | :--- | 
| `building` | Built environment | 
| `business` | Economic Activities - Business |
| `farm` | Economic Activities - Farm |  
| `electrical_system` | Lifelines - Electrical |
| `transport_system` | Lifelines - Transport |
| `tlc_system` | Lifelines - Telecommunication |
| `owner` | Owner profiles |
| `component` | Elements & production (all subclasses) |
| `added_block` | Added block |
| `building_component` | Principal structure |
| `fixed_asset` | Elements |
| `material` | Stocks - Stored inputs |
| `network_service` | Telecom service/Electrical service/Transport service |
| `transport_network_component` | Transport element |
| `tlc_network_component` | Telecom element |