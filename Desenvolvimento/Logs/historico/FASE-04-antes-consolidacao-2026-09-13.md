# Registro histórico da Fase 04

Texto preservado; não usar como estado atual.

```markdown
# Fase 04 — Balance Lab

## Início técnico — 2026-09-12

Iniciada infraestrutura de simulação, sem ajuste de balanceamento por decisão de Diego. `src/core/simulation.ts` executa duelo com IA dos dois lados e retorna resumo e comandos; gerador de lote avança seeds sequenciais sem repetição ou wrap silencioso. Cada resultado pode ser reproduzido pelo replay existente com os mesmos dados/regras. Cenário copiado no início da iteração; não há persistência.

Testados lote pequeno, equivalência com execução individual/replay e rejeição de intervalos inválidos. Limite de entrada de 10.000 não significa desempenho validado nessa escala. Faltam painel, cancelamento, agregação, exportação, benchmarks e baselines ampliadas. Não declara gate anterior ou desta fase aprovado; é construção da ferramenta, não avaliação automática de equilíbrio.

## Objetivo e gate

Verificação de escala inicial — 2026-09-13: executado teste de 100 duelos com conteúdo real (seeds 42–141), todos concluídos dentro do limite, sem seeds duplicadas ou mutação das builds. Reproduzidos por comandos os resultados mais curto e mais longo. Teste inclui medição de execução apenas informativa, sem limite de velocidade aprovado. Evidência headless não valida responsividade do navegador ou escala de 1.000/10.000; nenhuma conclusão sobre balanceamento.

Em 2026-09-13, comparação descritiva entre resumo atual e último lote não vazio da sessão: diferenças de taxas em pontos percentuais e média de turnos. Metadados identificam amostras diferentes e execução parcial. Configuração/builds são as mesmas carregadas na página; isso não implementa comparação de versões nem persistência da baseline. Sem aprovação automática de equilíbrio.

Métricas agregadas ampliadas: vitória e empate usam todas as lutas concluídas como denominador, inclusive em lote parcial; contagem por limite não equivale a empate. Mediana par usa média central; P90 usa posto ceil(0,9 × N). Sem intervalos de confiança ou inferência de equilíbrio. Resumo é recalculado a cada dez lutas e no término para reduzir trabalho de apresentação; progresso continua por luta. Não constitui benchmark de escala.

Exportação CSV adicionada em 2026-09-12: uma linha por luta concluída com metadados do lote, inclusive cancelamento/falha. UTF-8 com BOM, ponto e vírgula, escape de aspas e proteção contra interpretação de fórmulas textuais. JSON mantém cenário e comandos. Diego validou o laboratório anterior; essa confirmação não especifica escala de execução nem valida o novo CSV. Pedido de lote inválido preserva resultados e metadados anteriores.

Atualização técnica: painel ligado ao runner incremental com progresso, cancelamento entre lutas, contagem de vitórias/empates, média e extremos de duração. Lote cancelado/falho preserva apenas lutas concluídas; exportação JSON identifica estado parcial, quantidade pedida e contém cenário e comandos. Replay local seleciona seed concluída. Interface/performance em escala ainda não validadas; uma luta em andamento não é interrompida no meio. Não há CSV, importador externo, matriz ampliada ou comparação entre versões nesta entrega. Balanceamento segue adiado.

Transformar o Sandbox em laboratório que execute milhares de lutas, compare matchups, reproduza seeds problemáticas e exporte análise. O gate exige que bugs de RNG/balanceamento sejam reproduzíveis e que nenhuma arma/classe domine sem explicação deliberada.

## Escopo e requisitos

Inclui builds baseline Tank, Crit, Dodge, Burst, Sustain e variantes; execução x1/acelerada/instantânea; lotes de 100, 1.000 e 10.000; matriz de matchup; métricas agregadas/distribuições; filtro por seed/replay; CSV/JSON; comparação de versões de configuração e painel simples. Não inclui IA por machine learning, telemetria real, economia ou progressão.

O simulador é headless, recebe builds, quantidade e seed-base, permite paralelismo sem perder determinismo e usa IA simples/explícita, separada da engine. Todo outlier retorna seed/replay e a alteração de números ocorre nos dados, não na engine.

## Fluxos, validação e diagnóstico

Selecionar builds e versão, executar matriz, revisar win rates/distribuições, abrir outliers no Sandbox e comparar com baseline. O resultado do batch deve bater com o Sandbox para os mesmos comandos/seed e não duplicar eventos. Testar sanidade com amostra artificial, redução de variância e 10.000 lutas em tempo prático local.

Medir win rate e intervalo quando possível, turnos, dano/cura/críticos/stuns, mana/hit/dodge, uso de skill/Ultimate e timeout/empate. Riscos: IA enviesar resultados, média esconder extremos, otimizar o simulador antes do jogo e logs gigantes. Limite aceitável de win rate e política da IA baseline continuam abertos. Entregáveis: runner, matriz/painel, exportador, biblioteca baseline e replay no Sandbox.
```
