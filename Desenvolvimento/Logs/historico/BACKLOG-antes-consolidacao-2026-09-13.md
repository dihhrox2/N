# Backlog histórico — antes da consolidação

Transcrição preservada; não usar como status atual.

```markdown
# Backlog e roadmap

## Construção priorizada — 2026-09-12

Por decisão de Diego, balanceamento fica adiado sem bloquear construção e sem ser considerado aprovado. Seletor da build humana implementado: espada ou cajado, com IA no lado oposto e reinício explícito na troca. Não abre montagem livre. Próximas verificações funcionais incluem troca de lado, cura contra espada e reinício com seed; novo seletor ainda não validado visualmente.

## Resumo validado; avaliação qualitativa pendente — 2026-09-12

Diego validou o resumo. [Roteiro de avaliação](02-mvp-e-playtests.md) atualizado para comparar decisões e registrar percepção sem alterar parâmetros. Próxima decisão depende do feedback sobre recompensa do bloqueio, identidade das builds e RNG, não de nova confirmação de funcionamento. G1–G3 não foram aprovados automaticamente.

## Comparação validada e métricas — 2026-09-12

Diego validou a composição espada/cajado. Resumo observacional agora acompanha o painel; não atribui autoria de DoT ausente dos dados, contabiliza HP perdido pelo alvo. Próxima avaliação de gameplay: identificar se bloqueio compensa a ação, se a cura cria escolhas e se o sangramento exerce pressão perceptível. Validação funcional não responde automaticamente a essas perguntas.

## Builds de comparação aprovadas — 2026-09-12

Diego aprovou espada/sangramento contra cajado/cura. Painel conectado aos arquivos reais por `createPlaytestBuilds`, com atributos iguais da fixture, poção e Ultimate preservadas. Sem passiva nova equipada. Próximo passo é playtest comparativo de decisões, cura, pressão do sangramento e clareza dos resultados; nenhum vencedor foi declarado balanceado.

## Revisão do gate e validação do histórico — 2026-09-12

Diego validou o histórico legível. Revisão consolidada registrada na [Fase 02](fases/02-turn-engine.md): núcleo e painel funcionais, com 231 testes na última execução, mas sem aprovação automática de balanceamento ou conclusão integral da fase. A decisão imediata é escolher as builds fixas para comparação humana; o painel atual espelha a fixture. Testes sintéticos não substituem essa escolha.

## Validação da IA e legibilidade — 2026-09-12

Diego validou o painel com IA. Histórico aprimorado para explicar resultados sem JSON técnico; testes de apresentação adicionados. Aprovação funcional não equivale a aprovação de balanceamento ou ao fechamento automático do gate. Próximo passo: revisar cobertura e lacunas do gate com evidência atual; apresentação nova ainda não validada visualmente.

## IA local conectada — 2026-09-12

IA simples implementada e ligada ao painel, com mesmas ações/validações do humano e sem antecipar RNG. Limiar provisório de sobrevivência: 50% HP; poção, cura equipada, Ultimate pronta e ataque, nessa ordem condicional. Sem política defensiva sofisticada. Painel manual validado por Diego; próximo item é playtest da interação com IA e revisão do gate, sem inferir equilíbrio dos confrontos.

## Painel guiado conectado — 2026-09-12

Interface de batalha local adicionada sem remover diagnósticos: Diego controla ambos os lados, com fixture fixa e Ultimate de teste. Próximas verificações: inspeção visual, playtest manual e revisão de lacunas do gate. IA local ainda não implementada; painel guiado não substitui o MVP contra IA.

## Linha do tempo integrada — 2026-09-12

Consolidada visão cronológica de iniciativa, abertura, ações/reações, fim de turno e resultado, preservada no replay. Sem novo painel de UI. Próximos itens: revisar lacunas do gate da Fase 2 e conectar a interface ao motor; autoria detalhada dos DoTs não deve ser presumida a partir dos registros atuais.

## Duelo integrado verificado — 2026-09-12

Ampliada cobertura com duas builds sintéticas distintas em dez seeds, roteiro misto e replay integral. Invariantes de HP, mana, recarga, janelas e RNG conferidas a cada comando. 225 testes, lint, tipos e build passaram. Sem conclusão de balanceamento ou alteração de presets reais.

Próximos itens técnicos: consolidar log de ações e etapas de turno, revisar gate da Fase 2 e conectar interface para playtest. Não confundir os cenários automatizados com IA local implementada ou aprovação de gameplay.

## Passiva conectada — 2026-09-12

Concluída integração da passiva opcional de cura por crítico próprio ao despachante, com eventos identificados e replay. Testes cobrem execução única, HP máximo, ordem antes do DoT e ausência de gatilho por cura/DoT. Próximos itens: cenários de builds variadas, log de batalha consolidado e interface. Referências abaixo à integração pendente de passivas descrevem estado anterior.

## Comandos integrados — 2026-09-12

Entregue despacho local de ataque, block, dodge, passar, poção, cura equipada e Ultimate, com recursos, RNG contínuo, defesas temporárias e replay de comandos. Verificados 212 testes, lint, tipos e build. Interface não alterada.

Próximos itens técnicos: integrar passivas, ampliar os cenários de batalha entre builds e conectar o diagnóstico ao motor. O gate completo da Fase 2 continua aberto. Não há ação de limpeza de Stun no conteúdo atual; não inventar uma para habilitar o caminho futuro. As próximas seções são registros anteriores, não reabrem decisões já confirmadas.

## Estado consolidado — 2026-09-12

Ciclo de participantes implementado e testado: iniciativa, alternância, passagem automática por Stun, DoTs/recursos de fim de turno e limite de 100 turnos. Mantém escolha aberta quando há limpeza disponível. Recebe ações já resolvidas, sem despacho de comandos ou ligação com a tela.

Próximo trabalho técnico: integrar comandos válidos, recursos, efeitos defensivos e RNG compartilhado ao ciclo; depois verificar replay de duas builds completas e conectar a interface. Não depende de reabrir decisões já confirmadas. As notas anteriores abaixo registram a sequência histórica: iniciativa, custo/recarga da cura, esquiva ativa, limite/empate e fluxo de Stun já foram definidos. Fases 1 e 2 permanecem em desenvolvimento.

## Atualização — Fase 1 iniciada

Limite/resultado definidos e avaliador implementado: 100 turnos individuais, maior HP absoluto, empate em igualdade e prioridade à derrota. Restante da integração de batalha não deve ser confundido com helpers já testados.

Esquiva ativa implementada com bônus 25pp, ação principal e expiração no próximo início próprio. Próxima decisão necessária ao encerramento de batalha: limite total de turnos e empate exato ao alcançar esse limite.

Cura do cajado com uso validado: mana 10, ação principal, CD 2 sem desconto no turno atual. Próxima regra ainda aberta para ações básicas: benefício exato da esquiva ativa, distinto da esquiva passiva.

Iniciativa aprovada/implementada isoladamente: sorteio único ponderado, seguido de alternância. Para conectar habilidades ao ciclo, falta definir custo e recarga da cura do cajado, atualmente demonstração sem custo.

Fim de turno isolado implementado na ordem aprovada: DoTs, morte, mana e cooldowns. Ainda falta definir iniciativa para conectar o fluxo entre participantes; não há batalha completa.

DoTs resolvidos em ordem central configurável: bleed → poison; morte interrompe a sequência. Extensão futura exige registro, posição e testes. Integração completa com demais etapas de fim de turno continua pendente.

Fluxo sob Stun definido e helper testado: sem ação legal passa imediatamente; com limpeza disponível aguarda decisão. Intenção estratégica de passagem rápida registrada. Próxima decisão para integração: ordem de múltiplos DoTs no fim do turno e interrupção por morte.

Confirmados: fim automático após ação principal, consumíveis antes dela no próprio turno e Stun bloqueando todas as ações salvo limpeza explícita. Permissões isoladas implementadas. Falta definir fluxo de turno sob Stun quando houver opção de limpeza; nenhuma nova habilidade de limpeza foi criada.

Consumíveis definidos como ação livre, sem consumir ação principal. Uso único mantido. Próxima decisão: janela de uso no turno e interação com Stun.

Poção de cura 30 implementada com uso único, sem crítico. Próxima decisão: consome ação principal ou pertence à categoria de free action; nenhuma regra de economia de ações presumida.

Ultimate: mana 20 aprovada, uso validado e catálogo integrados. Próxima decisão para completar o recorte de consumível: efeito da poção de teste (ainda placeholder). Turn Engine não iniciado.

Recarga pós-Ultimate aprovada/implementada isoladamente: 4 turnos, sem desconto no turno do uso. Próxima decisão: custo de mana da Ultimate. Disponibilidade ainda não integrada ao resolvedor/Turn Engine.

Ultimate começa com CD 4 e libera no quinto turno próprio, contagem isolada implementada. Ainda decidir recarga após uso e mana; coordenação pertence à Fase 2.

Ultimate: efeito massivo definido e implementado isoladamente. Falta decisão sobre liberação/recarga para modelar condição de uso; integração ao catálogo/build segue pendente.

Catálogo de passivas e resolução de build integrados/testados, mantendo a fixture sem passiva. Decisão solicitada a Diego: efeito da primeira Ultimate de teste. Valores numéricos poderão ser provisórios; mecanismo não será presumido sem decisão.

Passiva de recuperação crítica isolada entregue e testada, sem atribuição. Próximas pendências: vínculo/validação de passivas em builds e modelo de Ultimate. O coordenador futuro deve evitar processamento duplicado do mesmo evento.

Envelope de eventos identificado implementado para resultados atuais, integrado ao diagnóstico de ataque/bleed e cura do cajado. Próximas pendências: modelos e gatilhos de passivas/Ultimate; estado integrado e turnos seguem separados. Notas abaixo são anteriores.

Catálogo mínimo de habilidades implementado: cura do cajado por ID e JSON próprio, preservando valores. Próximas pendências: modelos de passivas/Ultimate, gatilhos e identidade uniforme de eventos. Notas de revisão abaixo antecedem esta entrega.

**Revisão consolidada em 2026-09-12:** ver [matriz de implementação da Fase 1](fases/01-combat-engine.md). Próximo passo: catálogo mínimo de habilidades, começando pela cura existente do cajado e sua referência por ID. Depois: gatilhos/passivas e identidade uniforme de eventos. Ação básica, cura e três status não equivalem ao escopo completo. Fase 2 não iniciada.

### Notas anteriores

Registro legível ampliado para veneno, Stun e cura. Integração de efeitos no Turn Engine e sistema de habilidades continuam pendentes; não confundir formatação pronta com execução de turno pronta.

Veneno isolado entregue com valores aprovados provisórios. Ainda definir fonte/gatilho e ordem de múltiplos efeitos no Turn Engine; implementação não conclui a Fase 1.

Stun isolado entregue: uma ação principal bloqueada, sem acumular na reaplicação e sem interromper DoTs. Falta integração com Turn Engine na Fase 2; gatilhos em armas/skills, resistências e interação com free actions não foram definidos.

Diego confirmou o teste das três armas. Adicionada verificação determinística de frequências de acerto/crítico, sem ajuste de balanceamento.

## Ideias futuras para análise

| Ideia | Fase de análise | Responsável | Estado |
| --- | --- | --- | --- |
| LUK ampliar chance de ativação de efeitos de armas, itens e habilidades, além de crítico | 4 — Balance Lab | Diego | Hipótese, não implementada; definir elegibilidade, fórmula, caps e evitar contagem dupla nos efeitos já garantidos por crítico. |

### Histórico de avanços da Fase 1

Fixtures de adaga, machado e cajado entregues com identidades iniciais aprovadas e seletor diagnóstico. Valores provisórios; ainda faltam integração de habilidades, custos e demais status. Fase 1 não declarada completa.

Validação de estados de sangramento e limites numéricos reforçada antes do RNG. Não altera balanceamento nem adiciona novo status; demais efeitos e identidades de armas permanecem pendentes.

RNG compartilhado entre ações implementado e sequência integrada testada, com contagem de sorteios nos logs. Não implementa turnos. Diego confirmou a demonstração de cura anterior; ainda faltam demais status e perfis de armas.

Cura isolada entregue com crítico e limite de HP. Falta integrá-la a fontes de cura definitivas/skills; demais efeitos e perfis de armas continuam em aberto. Fase 1 ainda parcial.

Registro legível de ataque e sangramento entregue, com dados técnicos preservados. Diego confirmou manualmente o sangramento da entrega anterior. Próximos itens de Fase 1: cura, demais status e identidades de armas; não avançar ao Turn Engine como se a fase estivesse completa.

Atualização de sangramento: valores provisórios definidos e implementados (10% do poder, três aplicações, crítico como gatilho, renovação sem acúmulo com maior potência). Diagnóstico avança ticks manualmente. Controle de turnos e demais efeitos seguem pendentes. As notas seguintes registram estados anteriores.

DoTs: redução percentual por defesa implementada isoladamente, escala inicial 50, piso 1, sem bloqueio. Escala com poder dos atributos é a direção do sangramento; coeficiente, gatilho, duração, tick e reaplicação ainda precisam de confirmação. Não há status persistente ou turnos implementados.

Perfil numérico da espada externalizado no JSON e validado, preservando os resultados anteriores. Diego confirmou o teste manual do ataque independente. Próximo marco: definir as identidades e gatilhos de efeitos das armas, antes de implementar status.

Atualização mais recente: ataque independente e log estruturado implementados, com seed, acerto, variação, crítico por fonte, bloqueio, defesa e HP. Demonstração usa valores provisórios de 95–105% e 1,5×. Faltam perfis de armas/skills, efeitos e validação do gate; os parágrafos seguintes registram etapas anteriores.

Bloqueio atualizado: base 30%, bônus de STR com retorno decrescente e limite total 60%. Implementada a redução final isolada (bloqueio antes da defesa fixa, mínimo 1 no acerto, zero no erro). Integração ao ataque e controle da duração da ação seguem pendentes; não há batalha implementada.

Concluído o primeiro cálculo de atributos: pesos externos, curvas de bloqueio/esquiva/precisão/crítico e acerto por confronto. Valores provisórios aprovados por Diego. O gate da Fase 1 continua aberto: falta resolver ataque com dano, defesa, crítico, efeitos e log. Os estados abaixo da Fase 0 descrevem a entrega anterior.

## Estado da execução — 2026-09-11

Fase 0 entregue localmente: diagnóstico, schemas e referências JSON, RNG seeded, testes, lint, tipos e build. Motor definido como PixiJS; TypeScript estrito e JSON com Zod confirmados. Nenhuma fase de combate está implementada. Android/iOS continuam sem verificação.

## Como usar este documento

O roadmap define ordem de redução de risco, não datas. Cada fase só avança após seu gate; uma reprovação leva à revisão da fase atual, não à antecipação de sistemas futuros. Diego é responsável pelas decisões e aprovações.

## Roadmap sequencial

| Fase | Objetivo | Gate de saída | Dependência |
| --- | --- | --- | --- |
| 0. Fundação técnica | Definir repositório, stack, convenções, dados fora da lógica, IDs, versionamento, testes e seeds. | Projeto executa localmente, testes básicos rodam e dados de personagem de teste são validados. | Nenhuma. |
| 1. Combat Engine | Modelar personagem, atributos, derivados, equipamento, skills, status e cálculos de ação. | Um teste automatizado resolve uma ação e produz log reproduzível. | Fase 0. |
| 2. Turn Engine | Fechar ordem, turno, recursos, cooldowns, condições de vitória e resolução por turno. | Duas builds completas simulam combate determinístico, com log explicável. | Fase 1. |
| 3. Sandbox MVP | Disponibilizar UI funcional para luta contra IA, log, painel de resultado e depuração. | Pessoas externas avaliam decisões de combate como interessantes e compreensíveis. | Fase 2. |
| 4. Balance Lab | Simular em lote, controlar seeds, depurar e gerar métricas de combate. | Nenhuma arma ou classe domina sem explicação intencional; RNG e balanceamento são reproduzíveis. | Fase 3. |
| 5. Progressão local | Adicionar XP, níveis, árvore de classe, drops e inventário em ambiente local. | Loop de progressão offline/teste funcional. | Fase 4. |
| 6. Economia local | Simular Gold, durabilidade, NPC, bind, banco e Auction House local. | Economia simulável sem multiplayer. | Fase 5. |
| 7. Multiplayer PvP | Adicionar conta, persistência, serviço autoritativo, filas e matchmaking. | Dois jogadores em navegadores distintos concluem PvP 1x1 com estado consistente e resultado validado pelo servidor. | Fase 6. |
| 8. Ranking e social | Adicionar rating, perfil, histórico, amigos, chat e Hub inicial. | Alpha social jogável. | Fase 7. |
| 9. PvE e loop diário | Adicionar energia, missões, inimigos, bosses, autoplay e desafios. | Loop diário completo. | Fase 8. |
| 10. Mercado entre jogadores | Operar Auction House, trade, taxas, logs e proteções contra abuso. | Economia entre jogadores funcional. | Fase 9. |
| 11. Monetização segura | Adicionar VIP de conveniência, slots, cosméticos e regras de zero P2W. | Monetização sem alterar teto de poder. | Fase 10. |
| 12. Arte, áudio e polish | Substituir placeholders, produzir UX final, VFX, áudio e otimizações. | Beta apresentável e otimizado. | Fase 11. |
| 13. Hardening e lançamento | Segurança, anti-cheat, observabilidade, QA, moderação e soft launch. | Candidato a lançamento. | Fase 12. |

## Caminho atual: validação do MVP

### Especificações detalhadas disponíveis

| Fase | Documento |
| --- | --- |
| 0 | [Fundação técnica](fases/00-fundacao-tecnica.md) |
| 1 | [Combat Engine](fases/01-combat-engine.md) |
| 2 | [Turn Engine](fases/02-turn-engine.md) |
| 4 | [Balance Lab](fases/04-balance-lab.md) |
| 5 | [Progressão local](fases/05-progressao-local.md) |
| 6 | [Economia local](fases/06-economia-local.md) |
| 7 | [Multiplayer PvP](fases/07-multiplayer-pvp.md) |
| 8 | [Ranking e social](fases/08-ranking-e-social.md) |
| 9 | [PvE e loop diário](fases/09-pve-loop-diario.md) |
| 10 | [Mercado entre jogadores](fases/10-mercado-entre-jogadores.md) |
| 11 | [Monetização segura](fases/11-monetizacao-segura.md) |
| 12 | [Arte, áudio e polish](fases/12-arte-audio-e-polish.md) |
| 13 | [Hardening e lançamento](fases/13-hardening-e-lancamento.md) |

A Fase 03 não possui documento detalhado e fica omitida intencionalmente.

As fases 0 a 4 são o caminho de validação. Não iniciar a fase 5 ou qualquer sistema online, social, econômico, comercial ou artístico final antes de evidência positiva de combate e buildcrafting.

O primeiro playtest da Fase 3 usa builds fixas contra IA local determinística. A tela para criar personagem, distribuir atributos e montar builds livremente é uma expansão posterior do Sandbox; ela não substitui esse primeiro recorte de teste.

## Gates de decisão

| Gate | Pergunta que precisa ser respondida | Se a resposta for não |
| --- | --- | --- |
| G1. Combate | O jogador entende as regras e sente que suas decisões importam? | Iterar fórmulas, ações, mana, block, dodge e design de skills. |
| G2. Buildcrafting | Duas builds realmente jogam de forma diferente? | Reforçar a identidade de armas, passivas e skills. |
| G3. RNG | Críticos e dodge são empolgantes sem parecer injustos? | Ajustar frequência, telegraph, caps e efeitos. |
| G4. Progressão | Subir nível e escolher classe aumenta possibilidades sem esmagar o PvP? | Revisar curva de atributos, rating e recompensas. |
| G5. Economia | Gold entra e sai do sistema de forma sustentável? | Revisar sinks, drops, taxas e durabilidade. |
| G6. Multiplayer | Serviço autoritativo e reconexão são robustos? | Não liberar Ranked ou mercado. |
| G7. Monetização | F2P alcança o mesmo teto de poder e recursos? | Reprojetar o benefício pago antes de vender. |

## Decisões abertas por fase

### Fases 0 a 4 — P0

| Item | Fase | Status | Contexto |
| --- | --- | --- | --- |
| Escolher motor web | 0 | Concluído | PixiJS confirmado e amostra local verificada; regras independentes. |
| Definir fórmulas de diminishing returns, hit, dodge, crítico e block | 1 | Balancear | Necessário para legibilidade, risco e G1/G3. |
| Definir limite máximo de turnos | 2 | Definido provisoriamente | 100 turnos individuais; maior HP absoluto vence e igualdade empata. Implementado e testado. |
| Definir builds fixas e cenários de playtest | 3 | Aberto | Necessário para comparar decisões e diversão no MVP. |
| Definir roteiro e registro de feedback | 3 | Aberto | Necessário para transformar playtests em evidência. |
| Definir critério de crítico ignorar parte da defesa | 1 | Aberto | Decisão específica da mecânica de crítico. |

### Fases 5 a 10 — pós-MVP

| Item | Fase | Status | Contexto |
| --- | --- | --- | --- |
| Itens únicos/lendários que alteram regras | 5 | Aberto | Manter raridade determinística sem quebrar identidades. |
| Taxa de desgaste e custo de reparo | 6 | Teste | Durabilidade é posterior ao MVP. |
| Tabela exclusiva de drops PvP | 7 | Explorar | Separar quando economia e recompensas entrarem no escopo online. |
| Regras de derank proposital e smurfing | 7 | Aberto | Requisito de PvP online/ranked. |
| Escala e instanciamento do Hub | 8 | Técnico | Não deve atrasar o combate inicial. |
| Política de mercado paralelo | 10 | Aberto | Exige regras e proteções futuras. |

### Fases 11 a 13 — futuro

| Item | Fase | Status | Contexto |
| --- | --- | --- | --- |
| Tentativas extras de PvE via VIP | 11 | Revisar | Deve respeitar zero P2W e G7. |
| Classificação indicativa formal | 12 | Aberto | Produto direcionado a adultos; classificação não definida. |
| Lore, classes, locais, inimigos e identidade final | 12 | Criativo | Não bloqueia o MVP técnico. |
| Empacotamento para mobile além do browser | 12 | Técnico | Fora do alvo inicial PC web. |
| Hardcore e perda de equipamento | Futuro | Futuro | Regras de entrada, risco e recompensa permanecem sem fase definida. |

## Ordem de trabalho recomendada

Criar etapas pequenas com critério de aceite testável. Começar por modelos de dados e motor de combate sem UI, exigir testes unitários antes de novas features, manter conteúdo em arquivos separados da lógica e introduzir UI somente após as regras estarem cobertas por testes. O Sandbox continua sendo o ambiente permanente para validar cada skill, item ou classe nova.
```
