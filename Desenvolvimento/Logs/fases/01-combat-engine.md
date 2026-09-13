# Fase 01 — Combat Engine

## Estado da implementação

### Revisão consolidada — 2026-09-12

Consumível deixou de ser placeholder de efeito: poção cura 30 HP sem crítico e devolve estado de uso único. Schema e testes integrados. Ainda definir categoria de ação e integrar ao estado da batalha na Fase 2.

Ultimate integrada ao catálogo e ao uso atômico com custo aprovado 20, cooldown e recarga. Diagnóstico lista perfil sem equipar; não agenda turnos. Pendência de consumível permanece: item ainda é placeholder sem efeito definido.

Ultimate de teste implementada isoladamente com efeito direto massivo aprovado e multiplicador provisório 3×. Schema/perfil e resolvedor existem; vínculo ao catálogo/build e condição de uso ainda não. Fase permanece parcial.

Catálogo de passivas e referência opcional de build integrados. `src/core/build.ts` resolve dependências sem alterar o catálogo; a fixture normal permanece sem passiva. Ultimate ainda precisa de definição de efeito antes da implementação. Não há atribuição automática ou sistema completo de loadout.

Primeira passiva isolada implementada: 5 HP após crítico direto próprio. JSON/schema e testes de gatilhos indevidos, HP máximo e não encadeamento. Ainda não há vínculo de passivas em builds ou coordenador genérico; modelos de Ultimate seguem pendentes.

Identidade uniforme de eventos adicionada em `src/core/events.ts`: versão, sequência local, tipo, ator, alvo, fonte e snapshot de resultado. Demonstração usa nos ataques/ticks e cura da arma. Poison/Stun são suportados pelo contrato, mas continuam sem agendamento de turno. A origem de sangramento é preservada pela demonstração; um estado completo de batalha com origem de todos os status ainda não existe.

Atualização posterior à revisão: catálogo mínimo de habilidades entregue, com uma habilidade de cura referenciada pelo cajado. IDs, referências, versões e efeito são validados. O modelo ainda não contempla Ultimate/passiva, loadout, custos ou cooldowns; a próxima recomendação abaixo descreve o passo que deu origem a esta entrega.

Fase 1 **parcial**, sem aprovação do gate completo. A ação básica reproduzível existe, mas o escopo da especificação inclui modelos e efeitos que ainda não estão completos. A contagem de testes não substitui esses requisitos.

| Área | Evidência atual | Pendência |
| --- | --- | --- |
| Atributos e balanceamento externo | `src/core/attributes.ts`, JSON e testes de atributos | Modificadores de equipamentos/passivas ainda não compõem os derivados. |
| Ataque, defesa e crítico | `src/core/attack.ts`, testes de ataque e probabilidades | Resolução genérica de skills e efeitos de fonte. |
| Armas | Adaga, machado, cajado validados em JSON e testes | Perfis provisórios, não equilíbrio validado. |
| Cura | `src/core/healing.ts` e testes | Fonte do cajado ainda não é habilidade com ID/loadout. |
| Status | Bleed integrado ao crítico; Poison e Stun isolados | Modelo comum de origem/identidade dos efeitos e gatilhos declarativos ainda não existe. |
| Logs e replay | Formatadores e teste de sequência compartilhada | Eventos ainda não possuem identidade uniforme de ator/alvo/fonte. |
| Skills, Ultimate e passiva | Não há módulos ou catálogo correspondentes | Modelos, referências e validação; testes de gatilhos indevidos de passivas. |
| Consumível | Item placeholder validado | Efeito de uso ainda não implementado. |

**Próxima implementação recomendada:** catálogo mínimo de habilidades com IDs e referências em armas. Começar representando a cura já existente do cajado, sem criar nova mecânica. Depois definir gatilhos/passivas e eventos comuns. Valores e regras ainda não decididos não devem ser inferidos como aprovados.

**Reservado à Fase 2:** alternância, iniciativa, consumo de recursos, contagem de cooldown, consumo único de itens, agendamento/ordem dos ticks, consumo de Stun e encerramento da batalha. Modelar um campo de custo não equivale a implementar a economia de turnos. Ausência desses mecanismos não justifica antecipar a Fase 2 nem omitir os modelos da Fase 1.

### Notas históricas de implementação

Os parágrafos abaixo registram estados anteriores. Para situação atual, usar a tabela acima; os objetivos e escopo originais permanecem nas seções seguintes.

Formatadores legíveis cobrem agora ataque, bleed, poison, consumo de Stun e cura. Veneno/Stun permanecem isolados; seus textos estão testados e preparados para integração futura. Nenhuma nova regra de combate nesta atualização.

Veneno isolado implementado e testado: coeficiente 5%, duração 5, renovação com maior potência, defesa percentual e expiração. Nenhuma fonte atribuída e nenhuma integração de turno; não há nova interação visual.

Stun isolado implementado com aplicação, consulta e consumo de uma ação principal, sem acúmulo. Teste confirma continuidade de bleed após ação bloqueada. Não atribuído a armas; integração de turno permanece na Fase 2. Demais pendências da Fase 1 continuam abertas.

Primeiras identidades aprovadas implementadas em JSON: adaga com bleed no crítico, machado com multiplicador 2× e cajado com fonte de cura 20/1,5×. Poder 1 e variação 95–105% iguais para comparação inicial; não são valores balanceados. Seletor técnico permite testar sem alterar o personagem. Cura da arma é uma fonte independente, não um sistema completo de skills/custos/cooldowns. Demais status e marcos permanecem pendentes.

Validação de estado reforçada: efeito ativo exige aplicações inteiras positivas e dano finito; dados inválidos de efeito e overflow potencial são rejeitados antes de consumir RNG. Cobertura automatizada ampliada, sem concluir os demais marcos de Fase 1.

Integração headless validada em teste: ataque → tick de sangramento → cura → ataque, transferindo HP/status e compartilhando RNG. Demonstrações isoladas preservadas. Não constitui batalha ou Turn Engine; demais entregáveis da Fase 1 continuam pendentes.

Cura independente implementada: crítico seeded, limite de HP, excedente e ausência de ressurreição. Parâmetros provisórios em JSON; diagnóstico separado de ataque e status. Skills, custos, demais efeitos e identidades de armas continuam pendentes.

Registro legível implementado para ataque e sangramento, com JSON técnico preservado em painel expansível. O formatador é testado sem navegador e distingue erro, crítico, aplicação/renovação, expiração e morte. Diego confirmou manualmente a demonstração de sangramento anterior. O gate completo continua pendente de demais efeitos, cura e perfis de armas.

Sangramento inicial implementado: crítico aplica status, três ticks manuais, renovação sem acúmulo, snapshot do poder e defesa percentual atual. Testes cobrem expiração e morte. Não há Turn Engine, skills ou outros status. As notas anteriores abaixo são históricas.

Atualização: Diego confirmou o teste manual do ataque independente. O perfil numérico da espada agora vem do JSON validado, com testes de equivalência aos valores anteriores. Identidades das três armas e efeitos ainda não foram definidos nem implementados.

Iniciada parcialmente: pesos em JSON, schema de balanceamento, derivados de atributos e chance de acerto por confronto implementados com testes Node. O diagnóstico exibe os derivados. O gate de ataque completo ainda não foi atendido.

Os parâmetros aprovados estão em [Combate e buildcrafting](../03-combate-e-buildcrafting.md). Um ataque independente já resolve acerto, variação, crítico por fonte, bloqueio, defesa e HP, com log estruturado e seed. O diagnóstico permite comparar com/sem bloqueio. Perfis definitivos de armas, skills, status e efeitos continuam pendentes; o gate completo não foi aprovado.

## Objetivo e gate

Transformar decisões de combate em uma engine pura, calculável e reproduzível. Um teste automatizado deve executar “A ataca B”, resolver hit/dodge, dano/crítico, defesa e status, e gerar log estruturado com a seed fixa.

## Dependências, escopo e limites

Depende da Fase 00, atributos provisórios e dados de armas/skills. Inclui Character, Attributes, DerivedStats, EquipmentLoadout, arma/armadura/acessório/consumível, skills, Ultimate, passiva, StatusEffect, dano parametrizável, caps/diminishing returns, cura, efeitos on-hit/on-crit e CombatEvent/CombatLog. Não inclui turnos completos, mana por turno, UI, IA, XP, Gold ou persistência.

## Regras e fluxos

- Estado mutável de batalha é separado do template persistente; derivados vêm de atributos, equipamentos e passiva ativa.
- O pipeline resolve precisão contra dodge, variação seeded, defesa com piso configurável, crítico conforme fonte e efeitos em ordem documentada.
- Crítico pertence à fonte de ataque e pode disparar efeitos conectáveis; status têm ID, duração, stacks, origem e refresh definido.
- Logs nascem de eventos estruturados e registram seed, rolls, valores antes/depois e efeitos.

## Marcos e validação

| Marco | Saída verificável |
| --- | --- |
| Entidades | Builds válidas montadas em teste. |
| Ataque | Ataque básico determinístico por seed. |
| Efeitos | Adaga, machado e cajado ganham identidades via dados. |
| Logs | Cada cálculo é auditável. |

Cobrir defesa maior que dano, HP quase zero, chances mínima/máxima, seed repetida, distribuição estatística, diminishing returns, Bleed/Poison, Stun, cura crítica e passivas fora de eventos indevidos. Medir dano por fonte, taxas de hit/dodge/crit e eventos por ação.

## Riscos, abertos e entregáveis

Mitigar fórmulas opacas, crítico hardcoded, ordem inconsistente e returns confusos com etapas pequenas, hooks declarativos e testes de prioridade. Dano mínimo de 1 no acerto e bloqueio após crítico/antes da defesa estão definidos; caps são provisórios para balanceamento. Cura, três fixtures de armas e formatadores estão implementados no recorte descrito na revisão consolidada. Pendências de modelos, gatilhos e eventos estão explicitadas nessa revisão; o Combat Engine completo não foi declarado entregue.
