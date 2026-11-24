# Tabela: `owner`

!!! info "Nome diferente na interface web (GUI)"
    No backend PostgreSQL, esta tabela chama-se `owner`, como indicado no título da página. Na interface da aplicação web aparece como **Owner profiles**. Todos os aliases estão na [tabela de correspondência](../backend-to-gui.md).

!!! warning "Tradução assistida por IA"
    Esta página foi traduzida com a assistência de inteligência artificial e pode conter erros. A versão em inglês é a referência. Os nomes das tabelas e dos atributos são idênticos em todas as línguas porque correspondem aos da implementação PostgreSQL.

**Descrição (PT):** Esta entidade armazena os atributos universais de alto nível, como a identificação e os contactos, dos registos de proprietários.

## Estrutura das colunas

| Coluna | Tipo de dados | Definição | Exemplo de valor | Restrição? | Geometria? | Comentários |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Identificador único do proprietário | `3` | PK | Não | - |
| `email` | VARCHAR | Endereço de e-mail do proprietário | `example@mail.com` | - | Não | - |
| `fiscal_code` | VARCHAR | Número fiscal do proprietário | `AB0123CDEF` | - | Não | O limite de carateres e a configuração podem variar de país para país |
| `full_name` | VARCHAR | Nome completo do proprietário | `John Doe` | - | Não | - |
| `phone` | VARCHAR | Número de telefone e indicativo internacional do proprietário | `+390123456789` | - | Não | - |

## Relações

* **Possui:** [`enterprise`](enterprise.md) (Um proprietário possui uma empresa). Esta relação muitos-para-muitos é assegurada pela tabela de ligação [`enterprise_owner`](enterprise_owner.md).

## Consulta de exemplo

Obtenha uma lista de todos os proprietários, mostrando o seu nome e os seus contactos específicos:

```sql
SELECT *
FROM 
    owner o
ORDER BY 
    o.full_name ASC;
```

