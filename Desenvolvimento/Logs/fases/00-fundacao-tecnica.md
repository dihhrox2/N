# Fase 00 — Fundação técnica

## Entrega local — 2026-09-11

Implementados projeto único, JSON versão 1, validação estrutural e referencial, RNG Mulberry32 e diagnóstico HTML/PixiJS. TypeScript estrito, Vite, Zod, Vitest e ESLint estão configurados; versões exatas e lockfile estão presentes.

Passaram 14 testes headless, lint, tipos e build. O navegador local confirmou os dados, a amostra PixiJS e a repetição da seed. O gate local desta entrega está atendido; isso não representa validação mobile, combate ou produção.

Os tópicos seguintes preservam o planejamento original. Stack e formato de dados, citados como abertos ao final, foram resolvidos na entrega: TypeScript/PixiJS e JSON com Zod. Consulte o README para comandos e exercícios.

## Objetivo e gate

Criar a base previsível do projeto antes de features complexas: repositório, stack, convenções, dados, RNG, testes e ferramentas. A fase termina quando um comando sobe o projeto, outro executa testes e um personagem de teste pode ser carregado e validado sem depender da interface.

## Dependências, escopo e limites

Parte das decisões de projeto e do MVP local. Inclui domínios separados para engine, conteúdo/dados, aplicação web e testes; dados externos declarativos; IDs estáveis; versionamento de schema; RNG centralizado com seed manual; lint, type-check, testes unitários e CI/local. Não inclui login, banco remoto, servidor, economia, ranking, monetização ou arte final.

## Requisitos e fluxos

- A engine não depende de DOM, rede ou framework visual; regras não ficam em componentes.
- Conteúdo é carregado, validado por schema e referenciado apenas por IDs válidos; falhas impedem a inicialização e indicam arquivo/ID.
- Toda aleatoriedade passa por um serviço de RNG; a seed usada fica registrada e não há `random` disperso nas regras.
- O ambiente instala dependências, executa desenvolvimento, abre diagnóstico simples e roda testes sem passos manuais.

## Marcos, validação e métricas

| Marco | Saída verificável |
| --- | --- |
| Estrutura | Projeto sobe localmente e gera build de produção. |
| Schemas | Fixtures válidas e inválidas produzem diagnóstico legível. |
| RNG/testes | A mesma seed reproduz a mesma sequência. |
| Qualidade | Lint, type-check e testes passam em um comando previsível. |

Testar schemas, IDs duplicados/quebrados, serialização de fixtures e instalação limpa. Acompanhar apenas tempo de instalação/build, cobertura de schema/RNG e tamanho de dependências como diagnóstico.

## Riscos, decisões abertas e entregáveis

Evitar abstrações prematuras, conteúdo hardcoded e stack que prenda a regra à UI. Permanecem abertos o framework/empacotamento e o formato final dos dados. Entregáveis: repositório configurado, README operacional, schemas/fixtures, RNG seeded, suíte básica e página de diagnóstico.
