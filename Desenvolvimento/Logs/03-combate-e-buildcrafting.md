# Combate e buildcrafting

## Estrutura de batalha confirmada

Limite atual aprovado: 100 turnos individuais concluídos; vence maior HP restante absoluto, com empate em igualdade. Derrota por HP zero encerra antes de qualquer comparação pelo limite. Campo `battle.maxTurns` externo permite balanceamento posterior.

Iniciativa: sorteio único ponderado por `1 + índice de iniciativa`, seguido de alternância fixa. Mesmo índice implica 50% de chance inicial. Helper implementado e integrado ao contrato de RNG compartilhado; não representa ainda batalha completa.

- Formato principal 1x1, com turnos alternados.
- Uma ação principal por turno; skills, buffs/debuffs e consumível podem atuar como free actions quando sua regra permitir.
- Tempo de decisão desejado: 15 a 20 segundos; ao expirar, o jogador passa o turno.
- Vitória normal ao derrotar o adversário. Se houver limite de turnos, vence quem tiver mais vida; o limite exato está em teste.
- Não há movimentação tática relevante ou distância de ataque: a apresentação é lateral, em 2D.
- Dados públicos permanecem visíveis; parte da build inimiga fica oculta antes e durante a luta.
- A batalha prevê Combat Log e Chat; esses elementos não são requisito do MVP local.

## Ações básicas

Esquiva ativa aprovada: consome ação principal, dá +25 pontos percentuais de esquiva até o início do próximo turno próprio. Bônus em `activeDodge.bonus`; soma à esquiva passiva antes de aplicar limites de acerto, sem sorteio adicional. Stun impede uso. Helpers de ativação/expiração existem; coordenador deve passar o estado correto ao ataque. Não há invulnerabilidade garantida ou proteção contra DoTs.

### Atualização de permissões — 2026-09-12

Fluxo de Stun confirmado: sem ação legal, passagem automática imediata; com limpeza disponível, turno aberto para escolher usar a limpeza ou passar. Interface permanece visível/inspecionável, mas ações ilegais continuam bloqueadas. Intenção estratégica: menos tempo de planejamento no próprio turno quando não há resposta ao Stun. Passagem não cancela efeitos periódicos ou contagem de cooldown. O coordenador de turno ainda deve executar essas etapas.

Uma ação que consome o turno o encerra automaticamente após sua resolução; não há confirmação adicional de passar. Consumíveis são ações livres permitidas somente no próprio turno, antes da ação que o encerra. Stun bloqueia **todas** as ações, inclusive livres e poção de cura. Exceção: definição explícita de item/skill capaz de remover Stun. Isso substitui a descrição anterior de bloqueio apenas da ação principal; DoTs continuam normalmente.

Helpers em `src/core/action-window.ts` validam dono, janela aberta e Stun; `useConsumableInWindow` usa essa validação, com poção sem exceção de limpeza. `finishAction` fecha a janela após ação principal. São funções isoladas: não agendam próximo turno ou ticks. Definição de permissão vem da regra da ação, não de input livre do jogador. A existência da exceção não adiciona automaticamente item/skill de limpeza nem define o fluxo de decisão do turno atordoado.

Consumíveis são ações livres por decisão de Diego: não consomem a ação principal. Poção de teste cura 30 HP, sem crítico, limitada ao máximo e sem ressurreição. `consumableEffect.actionType` é `free`; `useConsumable` retorna `consumesMainAction: false` e `used: true`. O chamador deve preservar uso único por batalha. Com HP cheio, o uso atualmente consome o item sem recuperação. Não remove status nem consome RNG. Ainda não há execução por turnos ou botão de poção. Momento permitido de uso e interação com Stun ainda precisam ser definidos.

### Atordoamento (Stun) — regra inicial aprovada

Impede a próxima ação principal do alvo. Reaplicar antes do consumo não acumula ações perdidas. Danos periódicos continuam sendo resolvidos no fim do turno; não remover sangramento nem pular seus ticks. Nenhuma arma ou habilidade aplica Stun automaticamente nesta etapa, e nenhuma chance de ativação foi definida.

Implementação isolada em `src/core/stun.ts`: aplicação, consulta sem consumo e consumo explícito. Estado ausente é `null`; estado ativo bloqueia exatamente uma ação principal. O futuro Turn Engine deve consumir uma única vez na oportunidade da ação e respeitar o resultado, continuando a resolução do fim do turno. Consultas da UI não devem consumir o efeito. Não define interação com free actions, imunidade ou resistência; essas decisões continuam abertas. Não há integração com o turno ou nova interação na tela nesta entrega.

| Ação | Papel estratégico |
| --- | --- |
| Ataque básico | Depende da arma e deve equivaler a uma decisão real; pode aplicar efeitos, gerar recurso ou interagir com passivas. |
| Bloquear | Ação ativa que reduz parte do dano recebido até o próximo turno do usuário. |
| Esquivar | Ação ativa mais arriscada, com chance elevada de evitar completamente uma ofensiva. |
| Skill | Usa uma das habilidades equipadas; pode consumir mana, ter cooldown, ser free action ou exigir condição. |
| Consumível | Um item por build, normalmente de uso único por batalha. |
| Passar | Encerra o turno sem ação ofensiva e preserva recursos. |

## Build e progressão de personagem

Uma build combina atributos, classe, arma, armadura, acessório, skills, passiva e consumível. O personagem nasce sem classe; no nível 10 escolhe uma entre três classes-base reconhecíveis, com orientação para dano bruto, agilidade/destreza ou magia/intelecto. A escolha de classe é irreversível e desbloqueia ferramentas, não atributos.

Cada classe adiciona duas skills, uma Ultimate e uma passiva à biblioteca do personagem. O loadout de combate usa quatro slots de skill inteiramente livres, incluindo skills da arma. O jogador pode equipar nenhuma ou várias Ultimates; a economia de recursos deve limitar escolhas extremas.

## Atributos e matemática provisória

### Configuração inicial aprovada — início da Fase 1

Os valores abaixo são provisórios para testes, sem validação de equilíbrio. A fonte executável é `src/content/balance/attributes.json`, validada por Zod. A implementação preserva decimais; o arredondamento do dano aplicado será definido no resolvedor de ataques.

| Atributo | Peso inicial |
| --- | --- |
| STR | +1 poder e +1 índice de bloqueio |
| VIT | +10 HP e +0,5 defesa passiva |
| AGI | +1 índice de esquiva e +1 índice de iniciativa |
| DEX | +1 poder e +1 índice de precisão |
| INT | +1 poder, +2 mana máxima e +0,5 regeneração de mana por turno |
| LUK | +1 índice de crítico |

Bases: HP 100, mana 30, regeneração 3, defesa 0 e poder 0. Poder dos atributos = STR × pesoSTR + DEX × pesoDEX + INT × pesoINT. Todos os pesos ofensivos começam em 1; DEX 0,8 ou 0,7 são possibilidades futuras, não ajustes já aplicados.

Benefício percentual = limite × índice / (índice + curva), exceto Bloquear: redução = base + (limite total − base) × índice / (índice + curva). A base aprovada é 0,30. Percentuais são frações de 0 a 1 no código.

| Benefício | Limite | Curva |
| --- | --- | --- |
| Redução ao usar Bloquear | 0,60 | 30 |
| Esquiva passiva | 0,35 | 50 |
| Bônus de precisão | 0,08 | 50 |
| Chance de crítico | 0,50 | 50 |

Chance de acerto = 0,90 + bônus DEX do atacante − esquiva do defensor, limitada entre 0,10 e 0,98. É uma única chance de acerto; não executar um segundo sorteio de esquiva passiva, pois isso contaria o mesmo benefício duas vezes.

Bloquear garante 30% sem STR; 30 STR geram 45%; 60 STR, 50%. O limite total é 60%, com retorno decrescente. Essa redução só é aplicada pela ação Bloquear, que consome a ação principal. O índice de iniciativa ainda não define um sorteio. Esquiva ativa, poder da arma, modificadores de habilidades e resistência a status permanecem pendentes.

O painel de derivados mostra somente atributos. O ataque independente soma o poder da arma de teste; não existe consumo de mana, cura ou turno implementado.

### Ataque independente — implementação parcial

Ataque e cura aceitam agora um `RandomStream` opcional compartilhado, criado por `createRandomStream`. Sem ele, as demonstrações continuam reiniciando a seed. Com ele, ataque consome três sorteios e cura um; ticks não consomem RNG. Logs registram `rollStart` (quantidade já consumida antes da ação) e `rollEnd` (quantidade depois). Entradas de HP/status não são modificadas, mas o estado do gerador avança intencionalmente. Replay exige mesma seed, dados, versão das regras e ordem de ações, não apenas a seed isolada. Ainda não há agendamento de turnos.

O perfil provisório da espada é carregado de `src/content/espada_teste.json`, no objeto `attack`, com multiplicador crítico e variação mínima/máxima. A validação exige perfil em armas, multiplicador >= 1 e variações não negativas em ordem crescente. Nenhum efeito especial foi inferido; a identidade final das armas continua aberta. O formato local foi ampliado sem migração de saves, pois não existe persistência nesta etapa.

`src/core/attack.ts` recebe derivados validados, fonte de ataque, HP atual, indicação de bloqueio e seed. Retorna um novo resultado sem modificar entradas. Ordem: acerto → poder dos atributos + poder da fonte → variação → crítico → bloqueio → defesa → arredondamento/mínimo → HP restante.

A demonstração usa variação 95–105% e multiplicador crítico 1,5 como hipóteses provisórias, não decisões definitivas. Esses parâmetros pertencem à fonte recebida pela função. São feitos três sorteios em ordem fixa (acerto, variação, crítico), inclusive em erro; erro não aplica crítico nem dano. O log preserva sorteios e etapas, dano calculado e HP efetivamente perdido, sem permitir HP negativo.

Cada execução independente reinicia o RNG e o HP para comparação. A futura batalha precisará de um fluxo compartilhado de RNG, não reiniciar a mesma seed a cada turno. O primeiro efeito on-crit é sangramento; ainda não há batalha completa ou sistema de turnos.

### Redução final aprovada

Depois do eventual crítico, aplicar bloqueio ativo antes da defesa fixa. Arredondar para o inteiro mais próximo apenas ao final e garantir mínimo de 1 de dano quando o ataque acertar. Erro ou esquiva bem-sucedida causam zero. Exemplo: dano 40, bloqueio 30% e defesa 10 resultam em 18 de dano, contra 30 sem bloquear.

A função pura `src/core/damage.ts` implementa apenas essa etapa, recebendo dano e resultado do acerto prontos. Não sorteia crítico, não controla a duração do bloqueio e não modifica HP. A compensação pelo turno gasto ainda precisa ser avaliada em playtests; a ordem matemática não garante equilíbrio por si só.

| Atributo | Influência esperada |
| --- | --- |
| STR / Força | Poder ofensivo, bloqueio e derivados; armas não dependem exclusivamente de STR. |
| VIT / Vitalidade | HP direto, defesa e resistência a status. |
| AGI / Agilidade | Dodge, iniciativa e possíveis interações de velocidade. |
| DEX / Destreza | Precisão e derivados técnicos. |
| INT / Intelecto | Mana, regeneração de mana e eficiência de efeitos mágicos. |
| LUK / Sorte | Chance de crítico e builds focadas em crítico. |

Há um ponto de atributo por nível, sem limite inicial. Dano tem variação pequena; defesa e valor de proteção são separados. Percentuais relevantes usam diminishing returns, e hit/dodge têm limites mínimo e máximo para evitar 0% e 100% absolutos. Fórmulas exatas seguem abertas.

## Danos por tempo (DoTs) — redução inicial aprovada

Fim de turno confirmado e implementado isoladamente: DoTs → verificar morte → regenerar mana → reduzir cooldowns. Se morrer, não regenerar nem reduzir cooldowns. Regeneração limitada à mana máxima, preservando frações. Aplica-se também à passagem automática por Stun.

Ordem conjunta aprovada: sangramento antes de veneno, interrompendo na morte. Configuração `dot.order` e registro central em `src/core/periodic-effects.ts` permitem extensão futura explícita. A ordem de entrada dos estados não altera a sequência de resolução. Essa regra substitui a pendência de ordem citada em notas anteriores.

DoTs, incluindo sangramento, ignoram a ação Bloquear. O golpe inicial que aplica o efeito continua sujeito ao bloqueio. Defesa passiva reduz cada aplicação periódica percentualmente, não por subtração fixa:

`dano final = max(1, arredondar(dano periódico original × escala / (escala + defesa)))`

A escala provisória é 50, configurada em `src/content/balance/attributes.json` no campo `dot.defenseScale`, validado como finito e positivo. Exemplo técnico de dano original 10: defesas 0, 10, 50 e 100 resultam em 10, 8, 5 e 3. Arredondar somente ao final. Cada aplicação invocada tem piso 1, inclusive se receber base zero; ausência ou expiração de um efeito não deve invocar uma aplicação.

Implementação isolada em `src/core/dot.ts`: não recebe bloqueio, não usa RNG, não modifica HP nem controla turnos. O diagnóstico mostra exemplos técnicos, não sangramento ativo. Golpes diretos continuam usando defesa fixa.

Sangramento implementado com valores provisórios autorizados: crítico de fonte habilitada aplica 10% do poder dos atributos (sem poder da arma) por três finais de turno do alvo. O valor-base é fixado na aplicação, sem arredondamento antecipado; cada tick usa a defesa atual. Reaplicação renova três aplicações, sem acumular, e conserva o maior valor-base. O dano periódico não sorteia acerto ou crítico, ignora bloqueio e respeita redução percentual e piso 1. Alvo morto não recebe efeito novo nem ticks posteriores. Ignorar defesa passiva continua sendo possibilidade futura, não regra inicial.

`src/core/bleed.ts` retorna novos estados sem alterar os anteriores. `resolveAttack` aceita sangramento existente e registra aplicação/renovação no resultado. A espada de teste recebeu o perfil apenas como demonstração, sem definir a identidade final das armas. A tela reinicia o estado a cada ataque e avança ticks manualmente; a renovação é coberta pelos testes. Exemplo: poder 50 e defesa 50 produzem três ticks de 3, total 9.

## Mana, cura e crítico (regras gerais)

Cura do cajado: custo aprovado 10 mana, ação principal e recarga 2, sem desconto no turno do uso. `useHealingSkill` valida janela própria, Stun, mana, HP e cooldown antes do RNG; retorna cura, mana, recarga e janela encerrada. A demonstração antiga de cura isolada ainda não usa esse coordenador, portanto não comprova consumo de recursos na UI. Elegibilidade por loadout continua responsabilidade do futuro coordenador de batalha.

### Ultimate inicial — impacto massivo

Custo aprovado: 20 de mana, em `manaCost`. `useUltimate` valida dono do cooldown, disponibilidade e mana antes dos sorteios, retorna mana restante e recarga pós-uso sem alterar entradas. Uso executado cobra mana e inicia cooldown mesmo se o golpe errar (regra inicial adotada); tentativas inválidas não consomem RNG ou recursos. `resolveUltimate` permanece como cálculo isolado de dano. Perfil integrado ao catálogo, sem equipar a Ultimate automaticamente. Agendamento dos turnos continua fora desta entrega.

Recarga após uso aprovada: volta a 4, sem desconto no fim do turno do uso. A primeira redução ocorre no fim do próximo turno do dono. Exemplo: disponível/usada no turno próprio 5, continua em 4 no fim dele, diminui nos finais de 6–9 e fica disponível no turno 10. Campo `cooldownAfterUse` no JSON. `restartCooldownAfterUse` deve ser chamado apenas após uso bem-sucedido e pronto; o coordenador deve emitir cada fim de turno uma única vez. Custo de mana continua sem definição. Helpers não aplicam automaticamente esta restrição ao resolvedor de dano.

Cooldown inicial aprovado: começa em 4, reduz uma vez no fim de cada turno do próprio personagem e fica disponível para sua quinta oportunidade de turno. Não reduz no turno adversário. Campo `initialCooldown` no perfil da Ultimate; helpers isolados em `src/core/cooldown.ts`. `resolveUltimate` continua apenas calculando dano: o futuro coordenador deve verificar disponibilidade antes de chamá-lo. Recarga após uso e custo de mana ainda precisam ser definidos. Não há trava separada por número global de turno.

Efeito escolhido por Diego: dano direto massivo. Implementação isolada em `src/core/ultimate.ts`; perfil validado em `src/content/ultimates/impacto_massivo_teste.json`. Multiplicador provisório 3 sobre a soma de poder dos atributos e poder da arma, variação 95–105% e crítico próprio 1,5×. Segue acerto, bloqueio, defesa e piso existentes. Não herda bleed ou multiplicador crítico da arma. Aceita RNG compartilhado e não altera entradas. Não atribuída a personagem/classe; catálogo integrado, condição de liberação, custo e recarga continuam pendentes. Não há nova interface.

### Passiva de teste — recuperação após crítico direto

Perfil isolado `recuperacao_critica_teste`, em `src/content/passives/`, validado por `src/data/passive.ts`. Crítico direto acertado pelo dono da passiva recupera 5 HP, limitado ao máximo; valor provisório no JSON. Não ativa em ataque normal, ação de outro ator, DoT ou cura crítica. Não ressuscita. A recuperação não usa RNG nem causa crítico.

`src/core/passive.ts` recebe evento identificado e HP do dono e retorna resultado sem modificar entradas. O resultado pode ser registrado como `passive_healing`, tipo inelegível para esse gatilho; não há despacho recursivo. O futuro coordenador deverá processar cada evento uma única vez por passiva: o helper isolado não deduplica chamadas. Não atribuída a classe, arma ou personagem, sem nova interface ou catálogo integrado de passivas. Não representa um sistema genérico de todas as passivas.

### Veneno (Poison) — valores provisórios aprovados

Implementado isoladamente em `src/core/poison.ts`: cinco aplicações no fim dos turnos do alvo, cada uma com base de 5% do poder dos atributos, fixada ao aplicar. Parâmetros em `poison` no JSON de balanceamento. Reaplicar renova cinco aplicações sem acumular, mantendo a maior potência. Usa defesa atual com redução percentual dos DoTs, ignora bloqueio e não sorteia acerto/crítico. Arredondamento final e piso 1 por aplicação; expira após a quinta aplicação ou morte. Nenhuma arma recebeu o efeito; gatilho e integração de turnos seguem pendentes.

Exemplo: poder 100 e defesa 50 resultam em cinco aplicações de 3, total 15. O arredondamento e o piso podem aproximar veneno e sangramento em poderes baixos; diferença de identidade precisa ser validada no balanceamento. Ordem de resolução quando múltiplos DoTs coexistirem ainda não foi definida.

### Ideia futura — LUK e ativação de efeitos

Proposta de Diego para análise, não implementada: além da chance de crítico, LUK poderia aumentar a probabilidade de ativação de efeitos de armas, itens e habilidades. Avaliar no Balance Lab (Fase 4), com decisão de Diego antes de alterar regras ou dados executáveis.

Definir quais efeitos seriam elegíveis, chance-base por fonte, fórmula/peso, limite, retorno decrescente e interação com gatilhos garantidos. Cuidado com benefício duplo: hoje LUK já aumenta indiretamente a frequência de sangramento porque ele é garantido quando um crítico elegível ocorre. Um bônus adicional não deve ser aplicado automaticamente a esse gatilho. Avaliar também ciclos de ativações e efeitos de controle excessivos. Nenhum novo percentual, sorteio ou bônus foi aprovado.

Cura independente implementada em `src/core/healing.ts`: recebe valor da fonte e chance de crítico, sorteia uma vez por seed, multiplica eventual crítico e arredonda ao final. Recuperação é limitada ao HP máximo; resultado distingue cura calculada, recuperação efetiva e excedente. HP zero não é ressuscitado. Valor zero não gera cura mínima. Essas são regras técnicas iniciais, sem skill ou custo de mana.

Demonstração provisória: cura-base 20 e crítico 1,5×, configurados em `healingDemo` no JSON de balanceamento; chance derivada de LUK. Não define escala por atributo para futuras skills. Cada execução começa em metade do HP máximo, independente de ataque/status. Não remove sangramento e não usa defesa ou bloqueio. Sistema de turnos continua futuro.

Mana abastece skills e regenera durante a batalha. HP pode ser recuperado por skills, consumíveis, regeneração, lifesteal e passivas. Ultimates podem usar mana, cooldown e pré-carregamento, e passam a ser disponibilizadas a partir dos turnos 3 ou 4 como meta inicial.

O crítico varia por arma e/ou skill e pode aplicar efeitos como Bleed ou Stun, reforçar o próximo ataque, aumentar cura ou ativar outros efeitos. Skills e armas podem ter modificadores próprios; builds sem crítico precisam ser viáveis. O dano já amplificado por crítico passa pelo bloqueio e pela defesa fixa; modificadores específicos ainda serão definidos.
