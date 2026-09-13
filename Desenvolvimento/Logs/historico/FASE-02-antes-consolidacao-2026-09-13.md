# Registro histórico da Fase 02

Texto preservado; não usar como estado atual.

```markdown
# Fase 02 — Turn Engine

## Objetivo e gate

### Revisão consolidada — 2026-09-12

Diego confirmou manualmente o painel de batalha, a interação com IA e o histórico legível, em confirmações sucessivas. Última verificação automatizada: 231 testes, lint, tipos e build aprovados. Não confundir essas confirmações funcionais com aprovação de balanceamento ou dos gates G1–G3.

| Critério | Evidência atual | Limite restante |
| --- | --- | --- |
| Ciclo 1x1, recursos, fim automático e vitória | `battle-flow.ts`, `battle-commands.ts` e testes | Recorte atual, não todo o escopo original de efeitos. |
| Duas builds e reprodução | Duelo sintético espada/cajado em dez seeds, replay de estado e registros | Builds do playtest humano ainda não escolhidas; painel usa duas cópias da fixture. |
| Log explicativo | Linha do tempo e histórico legível validados manualmente | Origem de aplicação não guardada no estado dos DoTs. |
| IA local e ação livre | Mesmas regras do jogador; poção antes da ação; testes e validação manual | Política simples provisória, não evidência de equilíbrio. |
| Stun e veneno | Estados e resolução testados; passagem automática no ciclo | Não há fonte de aplicação equipada no painel nem ação de limpeza no catálogo. |
| Escopo original ampliado | Cura, passiva e Ultimate com mana/CD implementadas | Lifesteal e carga separada de Ultimate não implementados; não presumir exigência imediata contra o recorte aprovado. |

Fase não declarada integralmente concluída. Próxima decisão de Diego: selecionar as builds fixas do primeiro playtest comparativo. A montagem livre permanece posterior. As seções seguintes preservam o histórico das entregas; afirmações antigas de ausência de UI, IA, log consolidado, iniciativa ou limite não descrevem mais o estado atual. Limite e desempate já estão definidos provisoriamente: 100 turnos individuais, HP absoluto e empate em igualdade.

Conectar ações atômicas em partida 1x1 completa, reproduzível e sem UI. O gate exige duas builds completas do início ao fim, reproduzidas por seed e sequência de comandos, com log que explique cada passo.

## Dependências, escopo e limites

Depende da Combat Engine e de valores externos de Skill/Ultimate/Status. Inclui BattleState/TurnState, iniciativa com seed e bônus de agilidade/velocidade, ataque, block, dodge, skill, consumível, passar, mana/regen, cooldowns, carga de Ultimate, stun, duração de status, cura/lifesteal/regen e vitória/desempate. Não inclui timer real/UI, IA sofisticada, rede, ranking, XP ou recompensa.

## Regras e fluxos

### Linha do tempo — 2026-09-12

`CommandBattle.timeline` é a visão cronológica consolidada: iniciativa → abertura → ações e reações → fim de turno → próxima abertura ou resultado. Cada entrada tem sequência estável. A entrada de ação agrupa comando, resultado e eventos derivados; a entrada de fim de turno contém DoTs ordenados, mana, cooldowns e etapas executadas. Não transforma cada tick em evento global com origem de aplicação: essa informação não está no estado atual dos DoTs.

Abertura registra número do turno e expiração das defesas; também aparece para turnos pulados por Stun. Ações livres não geram abertura ou encerramento extra. Resultado é registrado uma vez; comandos rejeitados não alteram registros. Replay compara também a linha do tempo. Logs anteriores permanecem para compatibilidade interna; a interface deve preferir a visão consolidada. Não há importador externo nem painel visual nesta entrega.

### Passiva integrada — 2026-09-12

Loadout interno aceita `passive` opcional. Cada ataque direto executado emite um evento identificado e avalia uma vez a passiva do atacante; Ultimate também é ataque direto. A cura resultante é limitada ao HP máximo e registrada separadamente, sem realimentar o gatilho ou consumir RNG. Resolve após o ataque, antes dos DoTs de fim de turno. Cura crítica, passagem e DoTs não disparam passiva de ataque.

O replay local inclui esses eventos, com sequência estável. Eventos de ataque/cura/passiva estão em `events`; etapas de fim de turno continuam no log do ciclo, sem alegar um log unificado completo. A fixture normal continua sem passiva; loadouts de teste não são novos conteúdos equipados ao jogador. Faltam cenários de builds variadas e integração visual para avaliar o gate completo.

### Comandos conectados — 2026-09-12

`battle-commands.ts` integra ataque, block, dodge, passar, consumível, cura equipada e Ultimate. Ações principais fecham a janela e processam automaticamente o ciclo; poção deixa o turno aberto e registra uso único. Recarga inicial da Ultimate vem do conteúdo; recarga reiniciada não reduz no fim do turno de uso. Defesa ativa expira no próximo início próprio, inclusive sob Stun. RNG continua depois do sorteio de iniciativa e é preservado em ações rejeitadas.

`replayBattleCommands` reproduz comandos locais com os mesmos dados e regras. Testes cobrem uma batalha de ataques até derrota, igualdade do replay, recursos, permissões, recargas e defesas. Ainda não comprova o gate completo: faltam integração de passivas, cenários completos de builds variadas e interface. O histórico de comandos e os logs do ciclo são separados; não há importador/versionamento de replay externo. Notas de integração abaixo descrevem entregas anteriores e suas limitações à época.

### Integração do ciclo — 2026-09-12

`src/core/battle-flow.ts` conecta iniciativa, alternância, contagem de turnos concluídos, encerramento ordenado e resultado. Recebe estados internos após a ação principal/passagem; ações livres não encerram esse ciclo. Sem opção legal sob Stun, encerra automaticamente e resolve DoTs/recursos antes de trocar o participante. Com limpeza disponível, mantém a janela aberta. Opções são previamente avaliadas pelo chamador; nenhuma habilidade de limpeza foi adicionada.

Derrota causada pela ação impede efeitos posteriores; derrota por DoT interrompe recursos e abertura do próximo turno. Batalha encerrada, ator incorreto e janela ainda aberta são rejeitados. O chamador deve reter o estado retornado, pois snapshots antigos não são um mecanismo de proteção contra repetição de comandos.

Testes cobrem 100 passagens alternadas, reprodução do ciclo por seed, Stun dos dois participantes, limpeza disponível e morte. Isso não valida ainda o gate de duas builds completas: faltam despacho de comandos, integração de ataques/skills/consumíveis/passivas, expiração de defesas, continuidade do RNG das ações e replay completo. O contador de RNG deste recorte registra apenas a iniciativa. Interface permanece inalterada.

### Limite e resultado aprovados

Limite provisório de 100 turnos individuais concluídos em `battle.maxTurns`. Cada turno de um participante conta 1; free actions não contam turnos adicionais. Ao fim do centésimo, vence maior HP absoluto restante, sem normalizar pelo HP máximo; valores iguais empatam. Derrota por HP zero encerra imediatamente e tem precedência sobre o limite. Helper `evaluateBattleOutcome` implementa a avaliação; contagem e bloqueio de comandos posteriores cabem ao coordenador. Não há resultado de partidas completas validado apenas por esse helper.

Esquiva ativa: +25pp até início do próximo turno do dono, ação principal, respeita Stun e limites existentes. Helper fecha janela; ataque calcula bônus no mesmo sorteio. A expiração deve ocorrer antes das opções de ação do novo turno.

### Iniciativa aprovada e helper implementado

Sorteio único na abertura com peso `1 + initiativeIndex` (derivado de AGI) para cada participante. Probabilidade de A = pesoA / (pesoA + pesoB); índices iguais dão 50%. `rollInitiative` consome um sorteio do RNG compartilhado e registra pesos, chance, roll e ordem. Depois, `nextParticipant` alterna sem RNG adicional. IDs de instâncias devem ser distintos mesmo com a mesma fixture de personagem. O coordenador ainda precisa verificar vitória e fim de turno antes de alternar.

### Fim de turno implementado isoladamente

`src/core/end-turn.ts`: exige janela encerrada, resolve DoTs na ordem configurada, verifica morte, regenera mana até o máximo e reduz cooldowns do dono. Morte interrompe as etapas restantes. O fim do turno de uso da Ultimate preserva sua recarga, conforme flag existente. Resultado marca `endProcessed`; processar o estado retornado novamente é rejeitado. Entradas não são modificadas. O futuro coordenador deve persistir o resultado, sem reapresentar snapshots antigos como novos turnos.

Mesmo um turno passado automaticamente por Stun executa esse encerramento. Não há troca de jogador, iniciativa ou batalha completa nesta entrega. `endProcessed` deve ser reiniciado apenas ao abrir um novo turno pelo coordenador, não pela UI.

### Ordem de DoTs

Confirmada sequência inicial: bleed → poison, interrompendo imediatamente na morte. `dot.order` no JSON de balanceamento define a prioridade, independentemente da ordem de aplicação/armazenamento dos estados. `resolvePeriodicEffects` valida todos os estados antes de executar, resolve uma aplicação de cada efeito presente, retorna eventos ordenados e estados restantes. Morte remove os efeitos restantes sem executar outro tick.

Para adicionar uma classe de DoT: implementar seu estado/validação/tick, registrá-la em `src/core/periodic-effects.ts` e posicionar seu ID em `dot.order`, com testes. Ordem exige todos os tipos registrados exatamente uma vez; não há prioridade implícita por ordem de objetos. Modificar ordem ou registro modifica a versão lógica necessária ao replay. Não foram criados efeitos futuros fictícios.

### Decisão sob Stun confirmada — 2026-09-12

Se não houver ação legal sob Stun, passar imediatamente, sem espera artificial ou confirmação. Se houver item/skill de remoção realmente disponível (custo, cooldown, uso e alvo válidos), manter o turno aberto para o jogador escolher limpar ou passar. A interface deve continuar visível e inspecionável para permitir análise, sem habilitar execução de ações proibidas. Sem regra nova de timer nesta decisão.

A passagem rápida sem opções tem intenção estratégica explícita de Diego: reduzir o tempo de planejamento durante o turno do atordoado, simulando o efeito de Stun. Isso não significa impedir que o jogador pense ou observe no turno adversário, nem esconder informação pública.

`src/core/stunned-turn.ts` implementa a decisão isolada com opções previamente avaliadas pelo motor. Passar consome Stun e encerra a janela, mas sinaliza que o fim de turno ainda precisa resolver DoTs/cooldowns e vitória. Não executa ticks, não troca jogador e não implementa UI completa. Uma opção de limpeza não é automaticamente criada; fixtures de teste não são habilidades disponíveis no jogo.

Decisões posteriores confirmadas: ação principal encerra automaticamente o turno; consumíveis livres só antes dela, no próprio turno. Stun impede todas as ações exceto item/skill explicitamente capaz de removê-lo; poção de cura bloqueada. DoTs não são interrompidos. Helpers isolados de permissões já existem, mas a máquina de turnos permanece pendente. Fluxo de espera/encerramento quando houver opção de limpar Stun precisa ser definido.

- A máquina usa estados explícitos: pré-batalha, início de turno, free actions, ação principal, resolução, fim e encerramento; comando inválido falha com motivo claro.
- Block e dodge consomem ação principal; dodge é ativo e não garante 100%; free actions têm validação contra loops e consumíveis podem ser configurados como livres.
- Mana e cooldown mudam em momento único documentado; Ultimate combina custo, cooldown e carga; HP menor ou igual a zero encerra imediatamente.
- Um turno aplica início, verifica stun, abre free actions, resolve ação, aplica fim/regen/cooldown, verifica vitória e troca controle.

## Validação, riscos e entregáveis

Evidência de integração em 2026-09-12: `tests/battle-commands.test.ts` executa dez seeds (incluindo extremos de 32 bits) com espadachim sintético, sangramento e passiva contra cajado com cura. Roteiro exercita block, dodge, cura, Ultimate no quinto turno próprio, poção antes da ação e ataques até o resultado. Cada comando verifica limites de HP/mana, recargas não negativas, janela ativa única, limite de turnos e consumo esperado de RNG. Replay compara o estado completo, incluindo registros. Todas as verificações passaram: 225 testes, lint, tipos e build.

Essas builds existem somente nos testes; não são conteúdo aprovado ou simulação de IA. O roteiro não mede equilíbrio, diversão ou decisões humanas. O gate permanece aberto: consolidar logs do ciclo/ações e revisar a cobertura exigida de builds completas antes de declarar a fase concluída. Playtest visual não foi executado nesta verificação.

Testar consumo de stun, expiração de buff, block, consumível único, recursos não negativos, cooldown único, HP máximo, replay e seeds diferentes. Medir turnos por batalha, mana média, bloqueio/dodge e turno da primeira Ultimate. Permanecem abertos turn cap, desempate e timer de UX. Entregáveis: Turn Engine headless, replay, testes de timing, logs completos e fixtures de Ultimate/free action.

> Nota de escopo: o primeiro playtest posterior usa builds fixas. Montagem livre de build é expansão futura e não requisito deste gate.
```
