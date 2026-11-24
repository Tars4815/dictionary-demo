# Diretrizes de contribuição

!!! warning "Tradução assistida por IA"
    Esta página foi traduzida com a assistência de inteligência artificial e pode conter erros. A versão em inglês é a referência. Os nomes das tabelas e dos atributos são idênticos em todas as línguas porque correspondem aos da implementação PostgreSQL.

Obrigado por nos ajudar a manter o dicionário de dados rigoroso e atualizado! 

Uma boa documentação é um trabalho de equipa. Não precisa de ser programador, de saber escrever código nem de conhecer o Git para contribuir para este projeto. Todas as atualizações de conteúdo são geridas através de uma simples folha de cálculo.

---

## O fluxo de trabalho

Atualizar o dicionário requer apenas três passos simples:

1. **Descarregar o modelo:** Obtenha a versão mais recente do modelo Excel do dicionário de dados na nossa pasta partilhada da equipa.
2. **Preencher os dados:** Adicione ou atualize as linhas correspondentes às tabelas e às colunas da base de dados que está a documentar.
3. **Submeter para publicação:** Envie o ficheiro Excel atualizado à equipa técnica. Executaremos um processo automático para converter a sua folha de cálculo nas páginas web que vê aqui.

---

## Como preencher o modelo Excel

Cada folha do ficheiro Excel representa uma única tabela da base de dados. Para cada coluna dessa tabela, indique os seguintes detalhes:

* **Column:** O nome técnico exato do campo na base de dados (p. ex. `user_id`, `geom`, `created_at`).
* **Data type:** O formato dos dados (p. ex. `VARCHAR(255)`, `UUID`, `POINT`, `INTEGER`).
* **Definition (IT) & Definition (EN):** Uma descrição clara, compreensível também por quem não é da área, do que a coluna representa. Preencha tanto a coluna italiana como a inglesa, para apoiar a nossa plataforma bilingue.
* **Example value:** Um exemplo realista dos dados, para ajudar os outros a compreender o formato (p. ex. `john.doe@email.com` ou `POINT(12.49 41.89)`).
* **Constraint?:** Indique eventuais regras da base de dados, como `PK` (chave primária), `FK` (chave estrangeira) ou `NOT NULL`.
* **Geometry?:** Especifique se o campo contém dados espaciais (p. ex. `Yes - EPSG:4326` ou `No`).
* **Comments (IT) & Comments (EN):** Qualquer contexto adicional, lógica de negócio ou aviso sobre a forma de utilizar ou interpretar estes dados.

!!! warning "Mantenha a formatação simples"
    Evite formatações Excel complexas, como células intercaladas, cores de células personalizadas ou várias linhas dentro de uma mesma célula. O texto simples garante a conversão mais fluida para a plataforma web!

---

## Submeter as alterações

Quando o seu ficheiro Excel estiver pronto e revisto:

* Carregue a nova versão na unidade partilhada designada.
* Avise a equipa de administração da base de dados por e-mail ou através do nosso chat interno.
* A equipa processará o ficheiro e as suas alterações ficarão disponíveis no dicionário de dados em poucos minutos!