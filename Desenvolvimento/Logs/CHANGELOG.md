# Histórico de alterações

## 2026-09-13 — Navegação do replay da matriz

- Reutilizado replay por posição para navegar comandos da amostra verificada, com estado de recursos e efeitos.
- Troca de amostra e nova execução limpam seleção e desabilitam navegação anterior.
- Mantidos verificação prévia, snapshot de configuração e limites de posição; sem mudanças de combate ou validação visual presumida.

## 2026-09-13 — Replay das amostras da matriz

- Seletor identifica confronto, seed e duração de cada luta concluída, inclusive em matriz parcial.
- Replay usa builds/configuração do snapshot e verifica resumo antes de exibir histórico; chave não confunde seeds iguais de pares diferentes.
- Testados replay existente e rejeição de par/seed ausentes. Novo lote limpa resultados visuais anteriores.
- Sem importação externa, mudança de combate ou validação visual presumida.

## 2026-09-13 — Exportação da matriz

- JSON com configuração, builds por confronto, resumos/comandos, estado parcial e contagens totais.
- CSV por luta identifica confronto e mantém cabeçalho único; pares sem lutas continuam explícitos no JSON.
- Testados isolamento dos resultados e exportação parcial; botões desabilitados durante execução e sem resultados.
- Sem mudança de combate, importador externo ou validação manual dos downloads presumida.

## 2026-09-13 — Matriz incremental de confrontos

- Runner executa quatro pares com mesmo intervalo de seeds; identidade da amostra é confronto + seed.
- Painel dedicado inicia 400 lutas, informa resumo por par e permite cancelamento entre lutas preservando parciais.
- Teste de matriz pequena verifica os quatro pares, seeds, replay e isolamento do cenário. Não equivale a benchmark visual de 400 lutas.
- Regras e balanceamento inalterados; exportação própria da matriz permanece futura.

## 2026-09-13 — Confrontos entre builds existentes

- Seleção dos quatro pares espada/cajado, incluindo espelhos e ordem invertida, com IA nos dois lados.
- Instâncias independentes preservam IDs A/B; confronto identificado no resumo, comparação e exportações.
- Testados os quatro pares com simulação e replay. Seleção só aplica ao próximo lote; sem mudança na batalha manual.
- Nova interface ainda não validada visualmente; não constitui matriz automática ou aprovação de equilíbrio.

## 2026-09-13 — Conferência do resumo de replay

- Replay reexecutado e resumo comparado antes da navegação; divergência informa campos e bloqueia apresentação como partida original.
- Testados caso válido, duração alterada, comando inválido e ausência de mutação.
- Verificação limitada ao resumo interno, sem autenticação externa ou alegação de igualdade de todos os eventos. Nova interação visual ainda pendente.

## 2026-09-13 — Replay por posição

- Navegação de comandos no laboratório com estado de HP/mana/efeitos e histórico até a posição selecionada.
- Posição zero preserva iniciativa; passo de comando inclui reações e etapas automáticas. Novo lote limpa a seleção de replay.
- Testados início, primeiro comando, equivalência do resultado final, limites de posição e ausência de mutação.
- Sem importação externa, mudança de combate ou validação visual presumida.

## 2026-09-13 — Lote de 100 lutas verificado

- Teste de integração executa seeds 42–141 com builds reais, verifica conclusão, limite, unicidade de seeds e ausência de mutação.
- Replay dos extremos de duração conferido com o resumo original.
- Execução sem navegador; não extrapolar desempenho para 10.000 lutas ou interpretar resultados como aprovação de equilíbrio.

## 2026-09-13 — Medição de execução do laboratório

- Painel mostra tempo e velocidade média observada; conclusão/cancelamento congela a medição.
- JSON inclui seção `execution` separada de comandos e resultados; relógio não altera RNG ou replay.
- Testados cálculo, ausência de amostra e entradas inválidas. Sem benchmark de escala ou validação visual presumidos.

## 2026-09-13 — Comparação de lotes na sessão

- Preservado resumo do último lote não vazio ao iniciar nova execução válida.
- Exibidas diferenças de taxas e duração média, com seeds, tamanhos e status, incluindo parciais; ausência de dados não vira zero.
- Testado cálculo sem mutação. Sem persistência, comparação entre versões, inferência estatística ou alteração de combate.
- Nova apresentação ainda não validada visualmente; não presumida aprovação das métricas anteriores.

## 2026-09-12 — Distribuição e taxas do laboratório

- Diego validou a exportação CSV.
- Adicionados taxas com empates no denominador, mediana, P90 e total de lutas encerradas pelo limite, incluindo resultados parciais.
- Testados casos conhecidos, amostra unitária/vazia e duração inválida. Resumo recalculado a cada dez lutas e no término.
- Nenhuma regra de combate alterada; nova apresentação e desempenho em escala não declarados validados.

## 2026-09-12 — Exportação tabular do laboratório

- Registrada validação de Diego para o painel de simulações, sem inferir volume testado.
- Adicionado CSV por luta com estado do lote, contagens, seeds, resultado e política; JSON de replay preservado.
- Testados conteúdo parcial, empate, escape, proteção de fórmulas e rejeição de partida incompleta.
- Corrigido início inválido que alterava metadados do lote anterior antes da validação. Sem mudanças de balanceamento.

## 2026-09-12 — Painel do laboratório

- Lotes com progresso/cancelamento entre lutas, resultados agregados e extremos por seed.
- Exportação JSON com estado completo/parcial, configuração, builds e comandos; replay local de seed concluída.
- Agregação testada com amostra artificial, lote vazio e rejeição de partida incompleta.
- Interface e desempenho em milhares de lutas ainda sem validação; parâmetros de combate preservados.

## 2026-09-12 — Infraestrutura de simulação

- Diego validou a explicação do HP após iniciativa/ataque automático e pediu a próxima etapa.
- Iniciado runner sem interface: duelo automatizado e lote incremental com seeds sequenciais, resumo e comandos reproduzíveis.
- Verificadas equivalência com replay e entradas inválidas; sem alteração de parâmetros, painel novo ou desempenho declarado para milhares de lutas.

## 2026-09-12 — Informação de ações

- Registrada validação de Diego para o seletor de build.
- Mostrados custos, recargas, economia de ações e motivo de indisponibilidade em texto visível associado ao botão.
- Testes conferem leitura dos dados e ausência de mutação; nenhuma mudança de regras, IA ou balanceamento.
- Nova disposição visual ainda não validada manualmente.

## 2026-09-12 — Escolha da build controlada

- Adicionado seletor espada/cajado; IA assume o lado oposto e modo manual permanece disponível.
- Troca reinicia a partida; seed inválida impede reinício e restaura seletores do estado ativo. Identificação de você/IA/manual exibida por participante.
- Testado controle humano dos dois lados sem trocar equipamentos ou habilidades. Validação visual do seletor ainda pendente.
- Diego determinou adiar balanceamento e seguir a construção. Não implica aprovação de equilíbrio ou dos gates qualitativos.

## 2026-09-12 — Resumo validado e rodada qualitativa

- Diego confirmou a apresentação do resumo do playtest.
- Organizado roteiro comparativo em MVP e playtests, preservando parâmetros e separando validação funcional de julgamento de gameplay.
- Próxima entrada necessária: percepção de recompensa do bloqueio. Sem aprovação presumida de G1–G3 ou mudança de regras.

## 2026-09-12 — Resumo de playtest

- Diego validou a comparação espada/sangramento contra cajado/cura.
- Adicionadas métricas observadas por participante, sem alterar regras ou RNG: ataques, cura efetiva, dano direto, perda por DoTs, defesas e primeira Ultimate no turno global.
- Resumo parcial/final ligado ao painel, sem persistência. Testes conferem contagem, invariantes e ausência de mutação.
- Nova apresentação ainda sem validação visual; não declara equilíbrio aprovado.

## 2026-09-12 — Builds fixas de comparação

- Diego aprovou espada com sangramento contra cajado com cura.
- Painel usa as duas armas e habilidades reais do catálogo; atributos iguais, sem alterar JSON do personagem.
- Testados isolamento do catálogo, referências e replay de duelos em três seeds. Sem ajuste de balanceamento ou validação visual da nova composição.

## 2026-09-12 — Histórico validado e revisão de gate

- Diego confirmou a apresentação legível do histórico.
- Revisada evidência da Fase 02 e separados funcionamento técnico, validação manual e avaliação de gameplay.
- Corrigida pendência desatualizada do limite de turnos no backlog; decisão já aprovada preservada.
- Identificada escolha das builds fixas de playtest como próxima decisão. Sem alterar regras, criar conteúdo ou declarar conclusão integral de fase.

## 2026-09-12 — IA validada e histórico legível

- Diego confirmou validação manual da interação com IA local.
- Histórico passa a explicar dano/HP perdido, cura, passiva, sangramento, encerramento, mana, recargas e resultado; detalhes técnicos preservados.
- Tipado o registro do ciclo e adicionados testes de apresentação sem navegador, incluindo morte por DoT e poção livre.
- Sem mudança de regras ou balanceamento. Apresentação visual nova ainda pendente de validação.

## 2026-09-12 — IA local determinística

- Política simples sem sorteios próprios: sobrevivência até 50% HP, Ultimate disponível e ataque. Executa pelo mesmo despachante do jogador.
- Painel responde automaticamente com jogador_b; modo manual preservado por opção que reinicia a batalha.
- Testados prioridade, ação livre seguida de principal, recursos/recarga, turno correto e replay de duelo automatizado.
- Diego confirmou o painel manual anterior. Playtest da nova IA pendente; sem declaração de balanceamento ou gate aprovado.

## 2026-09-12 — Painel de batalha guiada

- Interface conectada ao motor com controle manual dos dois lados, seed/reinício, recursos, recargas, efeitos e histórico técnico.
- Builds fixas derivadas da fixture, com Ultimate de teste explicitamente adicionada ao diagnóstico; sem alteração do JSON original.
- Disponibilidade consultada por simulação pura do comando; regras permanecem no núcleo. Sem IA, persistência ou multiplayer.
- Diagnósticos anteriores preservados. Validação visual/manual pendente; não declara gate de playtest aprovado.

## 2026-09-12 — Linha do tempo consolidada

- Adicionado registro de abertura de turno e visão cronológica de ciclo, ações, reações e resultado.
- Ações livres preservam o mesmo turno; rejeições não geram registros; resultado aparece uma vez.
- Replay inclui a linha do tempo; logs anteriores preservados. Sem nova interface ou conclusão de fase.

## 2026-09-12 — Duelo de builds distintas e invariantes

- Dez cenários por seed com espada/sangramento/passiva contra cajado/cura, incluindo block, dodge, Ultimate e consumível livre.
- Conferidos recursos, janela ativa única, cursor de RNG e reprodução completa por comandos.
- 225 testes, lint, tipos e build aprovados. Builds restritas aos testes, sem mudança visual, novo balanceamento ou conclusão de fase.

## 2026-09-12 — Passiva no fluxo de batalha

- Integrada passiva opcional de cura por crítico direto próprio, incluindo Ultimate, sem RNG adicional ou recursão.
- Eventos identificados de ataque, cura e passiva, preservados no replay local.
- Testadas ordem antes do DoT, ausência de gatilho por cura/DoT, limite de HP e reprodução de batalha com passivas.
- Fixture normal e interface permanecem inalteradas; gate completo da Fase 2 ainda aberto.

## 2026-09-12 — Ações conectadas ao ciclo

- Integrados ataque, defesa, esquiva, passagem, poção, cura e Ultimate com validação de turno/equipamento, recursos e RNG contínuo.
- Defesas expiram no início próprio; consumível permanece livre e único; ações principais encerram automaticamente.
- Replay local por comandos e teste de batalha de ataques até derrota, além de recursos, recargas e rejeições sem mutação.
- 212 testes, lint, tipos e build aprovados. Sem alteração visual; passivas e gate completo da Fase 2 ainda pendentes.

## 2026-09-12 — Ciclo integrado de participantes

- Conectados iniciativa, alternância, fim de turno, contagem e resultado em módulo sem interface.
- Stun sem opção legal passa automaticamente e processa efeitos; limpeza disponível mantém a escolha aberta.
- Testadas 100 passagens, repetibilidade, morte por ação/DoT e rejeições de encerramento inválido, sem mutação da entrada.
- Ainda recebe ações previamente resolvidas; despacho, defesas temporárias, RNG das ações, replay completo e interface não estão integrados. Nenhuma fase declarada concluída.

## 2026-09-12 — Limite de batalha e empate

- Implementado avaliador de resultado com limite provisório 100, HP absoluto e empate por igualdade, conforme aprovação.
- Derrota por HP zero tem precedência; validação rejeita entradas inválidas.
- Testes cobrem fronteira 99/100, empate, HP fracionário e derrota imediata. Contador de batalha ainda precisa ser conectado ao coordenador de turnos.

## 2026-09-12 — Esquiva ativa

- Bônus aprovado 25pp em JSON, integrado ao acerto único com limites preservados.
- Ativação consome ação principal e respeita permissões; expiração no início do próximo turno próprio.
- Log identifica bônus; testes cobrem chances, consumo de RNG, duração e Stun. Sem nova interação visual ou batalha completa.

## 2026-09-12 — Uso da cura com recursos e ação

- JSON da habilidade inclui 10 mana, ação principal e recarga 2 aprovados.
- Helper coordena permissões, cura crítica, gasto, cooldown e fechamento automático da janela, sem mutação.
- Tentativas inválidas não avançam RNG. Sem substituir a demonstração isolada por uma batalha completa.

## 2026-09-12 — Iniciativa e alternância

- Implementado sorteio único ponderado por 1 + índice, com log e um consumo de RNG compartilhado.
- Alternância posterior sem sorteios, validação de participantes e proteção contra overflow da soma de pesos.
- Testes cobrem igualdade, pesos diferentes, replay, continuidade e entradas inválidas; não há nova interface ou batalha completa.

## 2026-09-12 — Encerramento ordenado do turno

- Coordenada etapa isolada de DoTs, morte, regeneração de mana e cooldowns, sem troca de participante.
- Morte interrompe recursos posteriores; mana limitada ao máximo; preservado CD no turno de uso da Ultimate.
- Flag de processamento evita repetir encerramento no estado retornado; testes cobrem Stun automático e entradas inválidas.
- Nenhuma batalha completa ou nova interface adicionada.

## 2026-09-12 — Resolução ordenada e extensível de DoTs

- Registro central e `dot.order` validado implementados: bleed antes de poison, parada imediata na morte.
- Resolvedor retorna eventos ordenados e estados restantes sem modificar entradas; tipos duplicados/inválidos são rejeitados.
- Documentado procedimento para novas classes de DoT sem criar tipos fictícios ou alterar fórmulas atuais.

## 2026-09-12 — Passagem automática sob Stun

- Implementada decisão isolada de passar imediatamente sem ação legal ou manter janela aberta com limpeza disponível.
- Passagem voluntária permitida ao dono sob Stun; resultado exige resolução de fim de turno, sem cancelar DoTs/cooldowns.
- Documentada intenção estratégica de reduzir o tempo de planejamento quando o turno é pulado.
- Sem item de limpeza criado, temporizador ou interface completa; testes exercitam opções sintéticas.

## 2026-09-12 — Fechamento automático e restrições de Stun

- Confirmado encerramento automático após ação que consome o turno, com consumíveis antes dela e somente no próprio turno.
- Corrigido escopo de Stun: bloqueia ações livres também, salvo remoção explícita; poção de cura sem exceção.
- Helpers de janela/permissão e uso validado de consumível adicionados e testados, sem máquina de turnos completa.

## 2026-09-12 — Consumíveis como ação livre

- Decisão de Diego: consumíveis não consomem ação principal. JSON/schema e resultado de uso refletem essa regra.
- Uso único da poção mantido. Não foi inferida permissão de uso durante turno adversário ou sob Stun.

## 2026-09-12 — Poção de cura

- Consumível de teste agora possui efeito validado em JSON: cura 30 HP, sem crítico/RNG, limitado ao máximo e sem ressurreição.
- Uso único representado no resultado; repetição com estado usado é rejeitada. Sem integração de turno ou atribuição de categoria de ação.
- Resultado informa recuperação/excedente; item e HP de entrada não são modificados.

## 2026-09-12 — Uso validado e catálogo de Ultimate

- Custo de 20 de mana aprovado e implementado, com verificação de CD/dono e consumo após execução; erro do golpe também consome recursos.
- Tentativa inválida não altera entrada nem avança sorteios. Uso devolve recarga 4 com proteção contra desconto no turno atual.
- Catálogo valida Ultimates/IDs e diagnóstico mostra perfil não equipado. Sem agendamento de turnos ou atribuição automática.
- Testes cobrem mana exata/insuficiente, CD, alvo inválido, erro do golpe e validação do catálogo.

## 2026-09-12 — Recarga após Ultimate

- Recarga pós-uso de 4 em JSON, sem redução no turno do uso; flag consumida somente no fim do turno do dono.
- Testada sequência: primeira disponibilidade no turno próprio 5 e nova disponibilidade no 10 após uso no 5.
- Reinício rejeita cooldown ainda ativo; estado anterior não é alterado. Mana e coordenação de turnos ainda não implementadas.

## 2026-09-12 — Cooldown inicial da Ultimate

- Perfil começa com CD 4; helpers reduzem no fim do turno do dono, liberando na quinta oportunidade própria.
- Testes cobrem contagem, turno adversário, piso zero, consulta sem consumo e validação.
- Sem agendamento de turnos ou recarga pós-uso presumida. Resolvedor de dano continua independente da disponibilidade.

## 2026-09-12 — Ultimate de dano direto

- Implementado efeito escolhido: golpe massivo, com 3× poder total provisório e perfil próprio de crítico/variação em JSON validado.
- Reutiliza resolução de ataque e RNG compartilhado; sem herdar efeitos da arma.
- Testes cobrem poder, crítico, mitigação, erro, HP, reprodução e validação.
- Sem liberação/custo/recarga definidos, atribuição ou UI; esses aspectos não foram presumidos.

## 2026-09-12 — Catálogo de passivas e build

- Catálogo carrega/valida passivas, detecta colisões globais de ID e referências ausentes.
- Personagem aceita passiva opcional; fixture existente não foi alterada nem equipada automaticamente.
- Resolver de build retorna cópia da arma, habilidades disponíveis e passiva. Diagnóstico exibe resumo, sem executar passivas automaticamente.
- Testes cobrem resolução, ausência, duplicação, perfil inválido e independência dos objetos.
- Solicitada decisão de efeito da primeira Ultimate; não implementada nesta atualização.

## 2026-09-12 — Primeira passiva isolada

- JSON/schema da recuperação crítica: 5 HP após crítico direto do dono, limitado ao máximo e sem ressurreição.
- Ignora DoTs, cura crítica e ataques alheios. Cura resultante não usa RNG nem causa crítico; evento próprio não reativa o gatilho.
- Testes cobrem filtros, limite, pureza e prevenção de encadeamento neste recorte. Sem classe/arma atribuída, interface ou coordenador global de passivas.

## 2026-09-12 — Identidade dos eventos

- Adicionado contrato tipado de evento com ator, alvo, fonte, sequência e snapshot do resultado, sem datas ou IDs aleatórios.
- Ataques e ticks formam lista técnica; cura da arma tem evento próprio. Fórmulas preservadas.
- A sequência é local à demonstração e não identifica globalmente batalhas. O helper recebe resultados internos, não é importador de replay externo nem valida referências de catálogo.
- 129 testes aprovados; nova estrutura visual dos dados técnicos ainda sem conferência no navegador.

## 2026-09-12 — Catálogo mínimo de habilidades

- Cura do cajado extraída para `src/content/skills/cura_cajado_teste.json`; arma referencia ID em `skills`.
- Validação detecta habilidade ausente, ID duplicado, referência repetida, versão e efeito inválidos.
- Interface resolve nome e efeito via catálogo. Valores e resultado da cura preservados; demo genérica continua independente.
- Sem migração de saves (não existe persistência), mana, cooldown ou loadout. Nova apresentação ainda sem conferência visual.

## 2026-09-12 — Revisão de pendências da Fase 1

- Consolidada matriz de implementação, distinguindo estado atual das notas históricas.
- Corrigida descrição que ainda tratava cura e fixtures de armas como ausentes.
- Identificadas pendências concretas: catálogo/modelos de habilidades, Ultimate/passiva, gatilhos, consumível e identidade de eventos.
- Próximo recorte recomendado: representar a cura existente do cajado como habilidade referenciada por ID, sem nova mecânica.
- Nenhum código ou regra alterado nesta revisão; gate completo permanece aberto. Última verificação executada na entrega anterior: 117 testes, tipos, lint e build aprovados.

## 2026-09-12 — Registro de efeitos e cura

- Formatadores em português cobrem veneno, consumo de atordoamento e cura, sem alterar regras.
- Registro distingue expiração/morte, ação bloqueada e ausência de atordoamento; não afirma que ticks foram executados pelo consumo de Stun.
- Cura genérica e do cajado usam o mesmo formatador, incluindo sorteio, recuperação e excedente.
- 117 testes aprovados. Veneno/Stun continuam sem interface ou integração de turnos; texto de cura atualizado sem nova conferência visual.

## 2026-09-12 — Veneno isolado

- Implementado Poison com cinco aplicações de 5% do poder, snapshot e renovação sem acúmulo, preservando maior potência.
- Defesa percentual atual, piso 1, sem bloqueio ou sorteios; expiração e morte encerram o efeito.
- Parâmetros externos validados em JSON. Testes cobrem duração, renovação, defesa, morte e entradas inválidas.
- Nenhuma arma, interface ou integração de turno adicionada.

## 2026-09-12 — Atordoamento isolado

- Implementada regra aprovada de uma ação principal bloqueada, sem acúmulo de reaplicações.
- Separadas consulta e consumo para evitar remover o efeito ao apenas consultar seu estado.
- Testes cobrem consumo único, reaplicação, pureza, estados inválidos e continuidade do sangramento.
- Sem arma atribuída, chance de ativação, nova interface ou Turn Engine. Nenhuma mudança na hipótese futura de LUK.

## 2026-09-12 — Hipótese de LUK e verificação de probabilidades

- Registrado teste manual das armas informado por Diego.
- Registrada ideia futura: LUK aumentar chance de efeitos de armas/itens/habilidades. Sem implementar bônus ou sorteio adicional; análise prevista no Balance Lab.
- Adicionados três testes de 20 mil ataques com seed fixa, comparando frequências de acerto e crítico com as probabilidades calculadas, tolerância de 2 pontos percentuais.
- Verificada relação atual de sangramento garantido no crítico elegível. Testes de sanidade não comprovam equilíbrio entre builds nem substituem playtests.

## 2026-09-12 — Três identidades iniciais de armas

- Adaga: bleed no crítico; machado: crítico 2×; cajado: cura independente 20 com crítico 1,5×. Valores provisórios em JSON, sem restrições de atributos.
- Preservada espada de teste. Seletor limpa a demonstração ao trocar arma, sem persistência ou alteração do personagem.
- Catálogo valida fonte de cura opcional da arma; painel do personagem lista somente equipamentos referenciados.
- Testes comparam as identidades usando os mesmos sorteios. Nova interação ainda sem conferência visual; não implementa sistema completo de skills.

## 2026-09-12 — Validação do estado em execução

- Sangramento ativo rejeita duração zero, negativa ou fracionária e dano-base inválido; efeito expirado deve ser representado por null.
- Ataque valida perfil de sangramento antes do sorteio, mesmo quando não haverá crítico.
- Ataque e cura rejeitam dano/cura potencial fora do limite numérico antes de avançar o RNG.
- 89 testes aprovados, incluindo preservação da sequência após rejeição. Sem nova mecânica ou interface; balanceamento inalterado.

## 2026-09-12 — Encadeamento reproduzível de ações

- Registrada conferência manual da cura por Diego, referente à entrega anterior.
- Ataque e cura aceitam RNG compartilhado opcional; uso independente preservado.
- Logs incluem posição inicial/final na sequência de sorteios. Teste integra ataque, tick, cura e novo ataque com HP/status transferidos.
- 78 testes aprovados, incluindo replay, isolamento dos geradores, equivalência anterior e seed incompatível.
- Sem nova interação visual, batalha completa ou Turn Engine.

## 2026-09-12 — Cura independente

- Adicionada cura pura com crítico reproduzível, arredondamento final, limite de HP e registro do excedente; não ressuscita.
- Base 20 e crítico 1,5× são valores provisórios no JSON, não balanceamento validado nem definição de skill.
- Diagnóstico separado reinicia com metade do HP, sem alterar ataque/status ou consumir mana.
- Testes cobrem cura normal/crítica, repetição, excedente, HP cheio/zero e entradas inválidas. Nova interface ainda sem conferência visual.

## 2026-09-11 — Registro legível do combate

- Registrada a confirmação manual do sangramento por Diego, referente à entrega anterior.
- Adicionado formatador em pt-BR sem dependência de navegador: acerto, crítico, bloqueio, defesa, HP, aplicação/renovação e expiração/morte por sangramento.
- Resultado de ataque identifica renovação explicitamente; nenhuma fórmula de dano foi alterada.
- JSON técnico preservado em painel expansível da demonstração.
- 66 testes aprovados; nova apresentação ainda sem conferência visual. A Fase 1 permanece parcial.

## 2026-09-11 — Sangramento provisório

- Perfil opcional em armas, habilitado na espada de teste: 10% do poder dos atributos e duração 3.
- Crítico aplica/renova mantendo maior potência; tick usa defesa atual, ignora bloqueio, não sorteia acerto/crítico e expira após três aplicações ou morte.
- Funções não alteram entradas; log registra status e ticks. Diagnóstico possui avanço manual, sem implementar Turn Engine.
- Seed 27 identificada para crítico na fixture original. Testes cobrem gatilhos, renovação, snapshot, expiração e HP; não equivale a balanceamento validado.

## 2026-09-11 — Defesa percentual contra DoTs

- Implementada redução periódica por `escala / (escala + defesa)`, escala provisória 50 em JSON validado, arredondamento final e piso 1.
- Bloqueio não participa da função. Ataques diretos permanecem inalterados.
- Diagnóstico mostra exemplos técnicos de redução, sem aplicar sangramento ou avançar turnos.
- Testes cobrem valores de referência, piso, independência de bloqueio, parâmetros inválidos e pureza. Duração, coeficiente e ciclo de vida do sangramento continuam pendentes.

## 2026-09-11 — Perfil da arma separado da interface

- Diego informou ter testado o ataque independente da entrega anterior; registro de validação manual pelo usuário, não de nova inspeção automatizada no navegador.
- Movidos multiplicador crítico e faixa de variação para o JSON da espada, preservando 1,5× e 95–105% como valores provisórios.
- Validação exige perfil de ataque em armas e identifica campos inválidos. Interface passa a mostrar e usar o perfil carregado.
- 43 testes aprovados, incluindo equivalência de resultados e alteração do multiplicador por fonte. Nenhuma identidade de arma, status ou turno foi inventado.

## 2026-09-11 — Ataque independente reproduzível

- Integrados acerto, variação, crítico por fonte, redução final e HP em função sem mutação das entradas.
- Log estruturado registra seed, três sorteios, etapas de dano e HP antes/depois.
- Diagnóstico inclui ataque contra atributos idênticos, com bloqueio opcional e reinício do HP em cada execução.
- Variação 95–105% e crítico 1,5× são hipóteses da demonstração; não representam aprovação definitiva de balanceamento.
- 35 testes aprovados. Não foram implementados turnos, efeitos, skills ou batalha completa; Fase 1 permanece parcial.

## 2026-09-11 — Bloqueio ativo e redução final

- Implementada base de bloqueio de 30%, bônus decrescente de STR e limite total de 60%, aprovados por Diego.
- Validação impede base negativa ou superior ao limite total.
- Adicionada etapa pura de redução final: bloqueio ativo antes da defesa fixa, arredondamento final e mínimo de 1 no acerto; erro causa zero.
- Diagnóstico utiliza a nova curva; 29 testes aprovados. Não há batalha ou controle de turnos; o gate da Fase 1 permanece aberto.

## 2026-09-11 — Fase 1: atributos parametrizados

- Registrados pesos iniciais aprovados e alternativas futuras para DEX.
- Adicionados configuração JSON validada, derivados puros e cálculo de acerto limitado por confronto.
- Diagnóstico passa a mostrar os valores derivados e erros de configuração.
- Testes cobrem bases, valores fracionários, curvas, caps, pureza e configuração inválida.
- Fase 1 apenas iniciada; nenhuma resolução de ataque ou batalha foi entregue.

## 2026-09-11 — Implementação da Fase 0

- Criados ambiente Vite/TypeScript estrito, PixiJS, Zod, Vitest, ESLint, versões exatas e lockfile.
- Adicionados dados provisórios de personagem e quatro equipamentos, validação de estrutura/IDs/referências e diagnóstico de erros.
- Adicionados RNG seeded independente da UI, amostra gráfica estática e exercícios no README.
- Verificação: 14 testes, lint, tipos e build aprovados; dados, PixiJS e repetição da seed confirmados no navegador local.
- TypeScript 6.0 foi escolhido pela compatibilidade declarada com typescript-eslint; a versão 7 consultada não era compatível.
- Os registros abaixo descrevem estados anteriores. Não há combate, servidor ou validação de dispositivos mobile nesta entrega.

## 2026-09-11

### Atualizado

- Adicionada a documentação detalhada das Fases 00, 01, 02 e 04–13, com objetivos, escopo, validação, riscos, decisões abertas, entregáveis e gates.
- O roadmap no backlog agora referencia as especificações detalhadas disponíveis; a Fase 03 permanece intencionalmente sem documento.
- O backlog passou a incorporar o roadmap de desenvolvimento, com fases sequenciais de fundação técnica até hardening e lançamento.
- Foram incluídos gates G1 a G7 e a associação das decisões abertas às fases correspondentes.
- O primeiro Sandbox foi explicitamente preservado como playtest de builds fixas; montagem livre de build permanece uma expansão posterior.

### Impacto

Nenhuma fase foi implementada. O roadmap é uma orientação de sequência e validação, sem cronograma de datas.

## 2026-09-11

### Adicionado

- Baseline de documentação interna do Projeto N.
- Brief, escopo do MVP, playtests, combate, sistemas futuros, UX, arquitetura conceitual e backlog.
- Registro de decisões confirmadas, provisórias e abertas a partir do documento de decisões do projeto e da conversa de descoberta.

### Impacto

Nenhum código, dependência, asset, integração ou ambiente foi criado ou alterado. O projeto permanece em pré-implementação.
