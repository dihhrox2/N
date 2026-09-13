# Backlog e roadmap

## Estado consolidado — 2026-09-13

Trabalho atual: infraestrutura da Fase 04, com protótipo local jogável. Consulte [estado atual](00-estado-atual.md) para capacidades e evidências. Balanceamento adiado, sem aprovação implícita dos gates. Fases 05–13 não iniciadas.

## Prioridades técnicas

- Validar visualmente recursos recentes do laboratório/matriz e replay.
- Medir escalas maiores; apenas lote de 100 lutas headless confirmado.
- Revisar lacunas de conteúdo/modelos das Fases 01/02 e requisitos ainda pendentes da Fase 04.
- Alinhar ampliação de conteúdo ou sistemas com Diego; não presumir progressão, backend ou publicação.
- Obter URL do repositório documental para eventual envio. Pasta atual sem Git/remote.

## Ideia futura preservada

LUK aumentar chance de triggers de armas/itens/skills, além do crítico: hipótese de Diego, sem implementação. Definir elegibilidade, fórmula, caps e evitar contagem dupla em efeitos já garantidos no crítico.

## Leitura do roadmap

As fases e gates abaixo são orientação de escopo e sequência, não comprovação de entrega. A infraestrutura atual não declara gameplay ou balanceamento aprovados. As decisões abertas devem ser lidas com as atualizações consolidadas.

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
| Definir builds fixas e cenários de playtest | 3 | Recorte implementado | Espada/sangramento e cajado/cura; cenários ampliados ainda futuros. |
| Definir roteiro e registro de feedback | 3 | Roteiro documentado | Ferramentas e métricas implementadas; avaliação de equilíbrio adiada. |
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

Notas de implementação anteriores preservadas no [arquivo histórico](historico/BACKLOG-antes-consolidacao-2026-09-13.md).
