# Estado atual de desenvolvimento

Atualização: 2026-09-13. Responsável por decisões: Diego.

## Resumo executivo

Projeto N possui protótipo local de combate 1x1 contra IA e ferramentas de laboratório. A construção avançou para a infraestrutura da Fase 04; isso não declara todas as fases anteriores integralmente concluídas. Balanceamento foi adiado explicitamente e não bloqueia a construção técnica, mas não está aprovado.

## Situação por etapa

| Etapa | Entregue no recorte atual | Pendente / limite |
| --- | --- | --- |
| 00 — Fundação | TypeScript estrito, Vite, PixiJS, JSON/Zod, RNG, testes e diagnóstico | Mobile não validado |
| 01 — Combate | Ataque, precisão/crítico, defesa, bleed/poison, Stun, cura, passiva, Ultimate e eventos | Escopo original de entidades/gatilhos não integral; origem de DoT ausente |
| 02 — Turnos | Iniciativa, alternância, ação livre/principal, recursos, recargas, encerramento, vitória e replay | Sem lifesteal; limpeza de Stun não equipada; sem sistema separado de carga de Ultimate |
| Sandbox | Builds fixas espada/cajado, escolha humana, IA, modo manual, histórico e métricas | Sem editor livre, arte final ou timer de decisão |
| 04 — Balance Lab | Lotes, quatro confrontos, matriz, agregação, exportações e replay | Sem baselines Tank/Crit/Dodge/Burst/Sustain, comparação entre versões ou importador externo; escala maior pendente |
| 05–13 | Especificações documentais | Não implementadas |

O Sandbox existe como recorte funcional; não foi criado documento da Fase 03.

## Mecânicas em uso

- STR/DEX/INT contribuem para poder; demais pesos e curvas continuam provisórios no JSON.
- Ataque direto: precisão, variação, crítico, bloqueio, defesa e arredondamento; acerto causa no mínimo 1, erro causa 0.
- Bloqueio possui base 30% e melhora com STR; esquiva ativa adiciona 25 pontos percentuais antes dos limites de acerto. Ambos gastam a ação e expiram no início próprio.
- DoTs ignoram bloqueio e sofrem mitigação percentual pela defesa; resolução bleed → poison, interrompida na morte.
- Sangramento da espada é aplicado no crítico; veneno e Stun têm regras testadas, mas não fontes equipadas no painel.
- Ação principal fecha o turno automaticamente. Poção de cura é livre, de uso único e usada antes da principal.
- Stun impede ações salvo limpeza explicitamente definida. Sem opção legal, passa automaticamente; caminho de escolha existe no ciclo, sem item/skill de limpeza no catálogo.
- Cura do cajado: 10 mana, recarga 2. Ultimate de dano direto: 20 mana, começa em recarga 4 e usa recarga 4 após execução. O turno de uso não desconta essa recarga.
- Passiva opcional de cura por crítico direto próprio está integrada; fixture normal não a equipa.
- Limite provisório: 100 turnos individuais. HP zero encerra imediatamente; no limite vence maior HP absoluto, com empate em igualdade.
- IA: até 50% HP prioriza poção e cura legal; depois Ultimate disponível ou ataque. Sem sorteios próprios ou previsão do RNG.

## Laboratório e reprodutibilidade

Lote individual oferece 100/1.000/10.000 lutas e escolha de quatro pares. Matriz usa 100 por par, 400 totais, seeds 42–141. Cancelamento ocorre entre lutas; resultados parciais são identificados.

Métricas incluem vitórias/empates, média, mediana, P90, extremos e limite de turnos. Tempo/velocidade são observações da execução, não parte do estado determinístico. Comparação entre lotes é temporária e não compara versões de configuração.

JSON guarda cenário, comandos e resultados; CSV serve para análise, não replay. Não há importação de arquivos, persistência automática ou serviço externo. Recarregar perde o estado da sessão.

Replay exige mesmos dados, regras, seed e comandos. Navegação por posição avança comandos, não necessariamente turnos. Conferência automática compara resumos; não autentica arquivos nem prova igualdade de todo evento intermediário.

## Evidências e validação

- Verificação atual: 257 testes em 37 arquivos, lint, tipos e build aprovados; verificação repetida na consolidação documental.
- Lote headless de 100 lutas reais, seeds 42–141, concluído; extremos reproduzidos por comandos.
- Testes incluem pares distintos/espelhados, matriz pequena, recursos, limites, replay, exportações e resultados parciais.
- Diego confirmou sucessivamente o painel, IA, histórico legível, composição espada/cajado, resumo, seletor de build, laboratório e CSV nas versões então apresentadas.
- Confirmações não especificam execução de 10.000 lutas. Funcionalidade aprovada não significa equilíbrio aprovado.
- Recursos posteriores, especialmente matriz, exportações/replay da matriz, comparação, métricas e navegação recentes, não receberam confirmação visual explícita nesta consolidação.
- Não há benchmark confirmado de 1.000/10.000 lutas ou matriz completa no navegador, nem teste de compatibilidade mobile.

## Fora da implementação atual

Progressão, XP, classes completas, economia local/social, inventário persistente, contas, banco, backend, multiplayer, ranking/social, PvE diário, mercado, monetização, arte/áudio finais e lançamento.

A futura autoridade de combate/dados será do servidor; o protótipo no navegador não oferece proteção anticheat. Escolha do banco segue futura. PixiJS não equivale a port mobile validado.

## Próximos trabalhos e decisões

1. Verificar interface e responsividade das ferramentas recentes e medir execução em escala.
2. Consolidar cobertura/limites técnicos das fases 01, 02 e 04 sem marcar gates retroativamente.
3. Definir com Diego a próxima ampliação de conteúdo/sistemas antes de assumir classes, progressão ou novos serviços.
4. Manter balanceamento adiado; ideias como LUK aumentar chance de triggers continuam hipóteses, não implementação.
5. Para publicar a documentação: obter URL e confirmar o destino documental. Não enviar código, dependências, dist ou dados pessoais por inferência.

## Fontes e precedência

Esta página consolida código/testes verificados e decisões desta conversa. Os documentos temáticos mantêm especificações e, onde indicado, notas históricas. Para situação de implementação, esta página prevalece sobre parágrafos antigos. Para histórico cronológico, consultar [CHANGELOG](CHANGELOG.md). Para escopo futuro e fontes por fase, consultar [backlog](07-backlog.md).
