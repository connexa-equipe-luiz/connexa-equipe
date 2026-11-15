# ADR-001 — Arquitetura e Stack Tecnológica do Connexa

- **Situação:** proposta
- **Data:** 2026-11-15
- **Participantes:** Luiz Felipe Knudsen Rodrigues e demais integrantes da equipe (incluir os nomes após confirmação)

## Contexto

O projeto Connexa será desenvolvido na disciplina de Engenharia de Software, utilizando práticas de desenvolvimento ágil, versionamento de código, testes automatizados e integração contínua.

Considerando o prazo acadêmico, o tamanho reduzido da equipe e a necessidade de organizar as funcionalidades, é importante adotar uma arquitetura que facilite a manutenção, a integração e a evolução do sistema.

A solução precisa permitir o desenvolvimento de funcionalidades independentes, mantendo limites claros entre os módulos e garantindo a qualidade do código.

## Decisão

Adotamos uma arquitetura de **monolito modular com aplicação SPA (Single Page Application)**, utilizando as seguintes tecnologias:

- **Back-end:** .NET 10, C# e ASP.NET Core Minimal APIs.
- **Front-end:** React 19 com TypeScript.
- **Banco de dados:** PostgreSQL 17.
- **Persistência:** Entity Framework Core com Npgsql e migrações.
- **Testes:** MSTest, WebApplicationFactory, Vitest e Testing Library.
- **Integração contínua:** GitHub Actions.
- **Organização do trabalho:** GitHub e Azure Boards.

O back-end será dividido em projetos independentes por módulo de negócio, com um schema de banco de dados por módulo.

A autenticação será simulada durante a Sprint 1, utilizando a interface `IUsuarioAtual`, permitindo a implementação de autenticação real futuramente.

## Alternativas consideradas

| Alternativa | Por que não foi escolhida |
|---|---|
| Arquitetura de microsserviços | Exige maior complexidade de infraestrutura, comunicação e implantação, não sendo necessária para o porte atual do projeto. |
| Monolito tradicional dividido apenas em camadas | Não estabelece limites suficientemente rígidos entre os diferentes módulos de negócio. |
| Banco de dados compartilhado sem separação por schemas | Dificulta o isolamento dos dados e o controle das responsabilidades de cada módulo. |

## Consequências

- **Positivas:**
  - Organização das funcionalidades por módulos.
  - Facilidade de manutenção e evolução do sistema.
  - Menor complexidade de implantação em comparação aos microsserviços.
  - Separação das responsabilidades entre os módulos.
  - Maior segurança nas alterações do banco por meio de migrações.
  - Verificação automática da qualidade por testes e integração contínua.

- **Negativas:**
  - Necessidade de respeitar rigorosamente as fronteiras entre os módulos.
  - Maior atenção à organização dos projetos e suas dependências.
  - Implantação conjunta dos módulos do back-end.
  - Necessidade de manter testes automatizados e migrações atualizados.

- **Como verificar:**
  - Executar `./verificar` antes de enviar alterações ao GitHub.
  - Conferir a compilação e os testes automatizados do back-end.
  - Validar os limites entre módulos por meio do NetArchTest.
  - Executar os testes, o lint e o build do front-end.
  - Conferir os três checks do GitHub Actions.
  - Exigir revisão e aprovação dos Pull Requests antes da integração à branch `main`.
