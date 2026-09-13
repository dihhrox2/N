# README histórico — antes da consolidação

Transcrição preservada. Não descreve o estado atual. Links dentro do bloco são históricos.

```markdown
# Projeto N

Base documental interna para um RPG PvP 1x1 por turnos, em pixel art dark fantasy.

## Estado atual

Replay da matriz também possui **Anterior**, **Próxima ação** e **Ir ao resultado**, exibindo HP/mana/efeitos. Abre na posição zero após conferir o resumo completo. Trocar a amostra ou iniciar nova matriz limpa a navegação para não misturar históricos. Sem alteração das regras; nova navegação ainda sem validação visual.

Matriz permite selecionar uma luta concluída por confronto + seed e abrir seu histórico após conferir o resumo reproduzido. Lotes parciais listam somente amostras existentes; novo lote limpa a seleção. Usa cenário guardado na execução, sem importar arquivos. Histórico completo; navegação passo a passo permanece no laboratório individual.

Matriz exporta JSON e CSV após conclusão, cancelamento ou falha com ao menos uma luta concluída. JSON guarda os quatro pares, incluindo os não executados, cenário, comandos e contagens; CSV traz apenas lutas concluídas com confronto identificado e contagens por par. Arquivos são baixados explicitamente; não há salvamento automático ou importação. Nova exportação ainda não validada manualmente.

Painel **Matriz dos confrontos**: executa 100 lutas por par (400 totais), sempre seeds 42–141, com progresso e cancelamento entre lutas. Resultados parciais mostram quantidade efetivamente concluída; taxas são da primeira build do par. Sem exportação própria da matriz nesta etapa; o laboratório individual mantém JSON/CSV e replay. Execução completa da matriz no navegador ainda não validada.

Laboratório permite escolher espada × cajado, cajado × espada e confrontos espelhados. A seleção aplica ao executar novo lote, sem alterar replay/exportação do lote já concluído. JSON/CSV identificam confronto; comparação anterior mostra posições A/B, não presume a mesma arma. Sem novas builds, regras ou balanceamento.

Antes de abrir replay, o laboratório reexecuta os comandos e compara todas as métricas do resumo com o lote. Divergências ou comandos inválidos bloqueiam a navegação e mostram o campo/erro. A checagem é interna: não autentica arquivo externo nem prova igualdade de eventos intermediários ausentes do resumo.

Replay do laboratório agora abre na posição inicial, com **Anterior**, **Próxima ação** e **Ir ao resultado**. Mostra HP, mana e efeitos no ponto selecionado. Cada passo é um comando, não um turno: consumíveis livres e efeitos automáticos mantêm sua resolução original. Não altera o lote nem a batalha jogável; navegação visual ainda não validada.

Verificação automatizada de escala inicial: lote de 100 lutas (seeds 42–141) concluído com as builds reais; extremos de duração reproduzidos por comandos. Teste sem navegador, sem comprovar desempenho em 1.000/10.000 ou responsividade visual.

Laboratório mede tempo decorrido e lutas por segundo, incluindo esperas/atualizações da página. Ao concluir ou cancelar, a medição fica fixa e é exportada em `execution` no JSON, separada do resultado determinístico. Não representa benchmark validado de 10.000 lutas; abas em segundo plano podem distorcer velocidade observada.

Comparação entre lotes na sessão: iniciar outro lote preserva o resumo anterior não vazio e mostra diferenças de vitória/empate em pontos percentuais e de duração média. Identifica seeds, tamanhos e estado parcial/concluído. Recarregar a página perde essa referência; não compara versões de configuração nem conclui melhoria de equilíbrio.

Resumo do laboratório ampliado: taxas de vitória/empate sobre todas as lutas concluídas, mediana, P90 de duração e contagem de encerramentos pelo limite. P90 usa posto mais próximo; mediana par é a média dos dois valores centrais. Amostra vazia mostra ausência de medida. Diego validou o CSV anterior; métricas novas ainda sem conferência visual.

Laboratório validado por Diego. Nova opção **Baixar CSV para planilha**: uma linha por luta concluída, com seed, turnos, vencedor, motivo e estado completo/parcial do lote. Separador ponto e vírgula e UTF-8 com BOM. JSON continua sendo o pacote completo de cenário/comandos; CSV não serve para replay. Exportação CSV ainda não validada manualmente em planilha; não há benchmark confirmado de 10.000 lutas.

**Laboratório de simulações** disponível ao fim da página: lotes de 100/1.000/10.000, progresso e cancelamento entre lutas. Resultados parciais ficam em memória; JSON inclui builds, configuração, política identificada e comandos. Consulte uma seed concluída para reproduzir seu histórico. Comece com 100: desempenho em 10.000 ainda não validado. Não há importação de arquivos nem persistência automática.

Infraestrutura do laboratório iniciada em `src/core/simulation.ts`: execução automática de duelos e lotes reproduzíveis com resumo/comandos. Ainda sem controles de lote na tela. Balanceamento continua adiado; a ferramenta não aprova equilíbrio nem conclui os gates.

Ações agora mostram custo, recarga, consumo de turno e motivo de indisponibilidade abaixo do botão. Custos vêm dos dados equipados, sem fórmulas novas. Diego validou o seletor de build; esta apresentação das ações ainda requer conferência visual.

Escolha **Sua build** no painel: espada/sangramento ou cajado/cura. A IA assume o outro lado; trocar escolha ou modo reinicia a partida e descarta o histórico atual. IDs continuam ligados às mesmas builds (a = espada, b = cajado), preservando a iniciativa por seed. Sem editor de personagem. Balanceamento fica adiado por decisão de Diego, não considerado aprovado nem bloqueador da construção.

Comparação espada/cajado validada manualmente por Diego. Novo **Resumo do playtest** mostra turnos concluídos, acertos/críticos, HP retirados diretamente, cura efetiva, HP perdidos para DoTs, defesas usadas e primeira Ultimate por turno global. Valores parciais durante a batalha; não são parecer de balanceamento. Não há salvamento e reiniciar descarta o resumo anterior.

Playtest comparativo aprovado: jogador_a usa espada com sangramento; jogador_b usa cajado com cura. Atributos iguais da fixture para isolar arma/habilidade, sem novos pesos. IA controla o cajado; desative-a para testar manualmente a cura. Poção e Ultimate continuam disponíveis aos dois. Compare decisões e legibilidade, não apenas quem vence; mesma seed e comandos reproduzem o confronto.

Diego validou a interação com IA local. O histórico agora apresenta vida perdida, cura efetiva, sangramento, mana recuperada, recargas e resultado em português, sem exigir consulta ao JSON técnico. Essa apresentação nova ainda não recebeu validação visual; regras e prioridades da IA não foram alteradas.

IA local disponível no painel **Batalha local**: jogador_a é humano e jogador_b responde automaticamente, inclusive se ganhar a iniciativa. Desmarcar IA reinicia em modo manual. Política provisória: até 50% HP, poção disponível e depois cura equipada; senão Ultimate pronta com mana ou ataque. Sem previsão de sorteios, IA avançada ou balanceamento validado. O painel manual anterior foi validado por Diego; a interação nova com IA ainda requer playtest.

Novo painel **Batalha local guiada**, ao fim da página: controle os dois lados com builds fixas da fixture e Ultimate de teste. Mostra HP, mana, efeitos, recargas, ações e histórico cronológico. Use poção antes da ação principal; reinicie com a mesma seed para repetir suas decisões. Não é IA ou multiplayer. Diagnósticos anteriores preservados. Verificação visual/manual deste painel ainda pendente.

Registro cronológico integrado: `CommandBattle.timeline` reúne iniciativa, abertura, ações com reações, encerramento e resultado. Poção e ação principal ficam no mesmo turno; ações rejeitadas não entram no histórico. Os detalhes de DoTs, mana e recargas ficam no registro de fim de turno. Ainda é estrutura interna, sem painel visual novo.

Verificação ampliada: dez seeds de duelos entre builds sintéticas distintas, combinando defesa, cura, Ultimate, poção e ataques, chegam ao resultado e reproduzem estado e registros por comandos. São cenários automatizados, não presets aprovados nem evidência de balanceamento. Total atual: 225 testes aprovados; a tela continua independente do motor de batalha.

Passiva conectada ao motor (2026-09-12): loadouts internos aceitam passiva opcional. Crítico de ataque direto próprio, incluindo Ultimate, aciona a cura configurada uma vez, antes do fim de turno e sem RNG extra. Cura e DoTs não acionam esse gatilho. A fixture normal continua sem passiva e a interface não foi alterada.

Atualização mais recente: `src/core/battle-commands.ts` conecta ataque, bloqueio, esquiva, passagem, poção, cura equipada e Ultimate ao ciclo. Comandos válidos atualizam HP, recursos, efeitos e RNG; ações principais encerram o turno automaticamente. Testes executam batalhas de ataques até a derrota e repetem o resultado pelos mesmos comandos. A interface ainda é o diagnóstico independente; passivas e o gate completo da Fase 2 permanecem pendentes.

Atualização de 2026-09-12: o núcleo possui um ciclo de participantes testável sem navegador (`src/core/battle-flow.ts`), conectando iniciativa, alternância, Stun automático, fim de turno e limite de batalha. Ele recebe ações já resolvidas; ainda não despacha comandos de combate nem está conectado à tela. A demonstração abaixo continua independente. As Fases 1 e 2 não estão declaradas concluídas.

A Fase 0 possui implementação local: diagnóstico de personagem, validação JSON e RNG reproduzível. A Fase 1 resolve ataque independente e sangramento por crítico, com aplicação, renovação e expiração testadas. Ainda não há sistema completo de turnos ou skills. Persistência, backend, multiplayer e arte final continuam futuros.

Na seção **Ataque de teste**, use a seed 42 e clique em **Resolver ataque**. Repita para conferir o mesmo resultado; depois ative Bloquear e compare. Cada execução reinicia o HP. Variação de 95–105% e crítico de 1,5× são parâmetros provisórios da demonstração, não balanceamento aprovado. O poder da arma de teste é somado apenas no ataque.

Os pesos provisórios ficam em `src/content/balance/attributes.json`. O diagnóstico valida esse arquivo e mostra poder, HP, defesa, mana e percentuais calculados. Equipamentos ainda não contribuem para esses derivados. Alterar um peso muda o resultado sem reescrever a fórmula.

## Executar e aprender

O catálogo carrega passivas de `src/content/passives/`. A build aceita uma referência opcional `passive`, validada pelo ID; a fixture normal continua sem passiva. `resolveBuild` resolve arma, habilidades disponíveis e passiva sem modificar dados. Não é um editor nem o loadout completo de quatro skills. Passivas não são executadas automaticamente pela demonstração.

Os dados técnicos do ataque agora são uma lista de eventos identificados: ator, alvo, arma/habilidade e sequência. Cada resultado fica em `result`. O cajado possui painel técnico próprio para o evento de cura. IDs `diagnostic_attacker` e `diagnostic_defender` distinguem as duas instâncias de teste, mesmo usando o mesmo personagem-base.

A cura do cajado agora é a habilidade `cura_cajado_teste`, definida em `src/content/skills/cura_cajado_teste.json`. O cajado guarda apenas seu ID em `skills`. Alterar a cura deve ser feito no arquivo da habilidade; valores permanecem 20 e crítico 1,5×. Sem custo/cooldown ou loadout de skills nesta etapa.

Escolha uma arma em **Arma da demonstração**: adaga aplica sangramento no crítico; machado usa crítico 2×; cajado habilita cura-base 20. Todos têm poder provisório 1 e variação 95–105%. Use seed 27 com atributos originais para comparar críticos. Trocar arma limpa HP/status/log da demonstração, sem editar o JSON do personagem. Cura do cajado é independente, ainda sem mana/cooldown ou sistema completo de skills. A espada original permanece disponível.

O núcleo também suporta RNG compartilhado entre ações. Um teste encadeia ataque, sangramento, cura e novo ataque, transferindo HP e status. A tela continua com demonstrações independentes; esta preparação não implementa turnos. Para repetir a sequência inteira, é preciso a mesma seed, conteúdo e ordem de ações.

**Cura de teste independente** usa a seed informada e começa com metade do HP máximo a cada execução. Base provisória 20 e multiplicador crítico 1,5 ficam em `healingDemo` no JSON de balanceamento. A chance vem de LUK. Não altera a demonstração de ataque, não remove sangramento nem consome mana.

O registro de ataque e sangramento agora explica os cálculos em português. Abra **Ver dados técnicos do combate** para consultar os resultados completos. A apresentação é separada das regras: mudar o texto não altera dano, sorteios ou status.

O diagnóstico também mostra exemplos de redução de DoTs pela defesa. `dot.defenseScale`, no JSON de balanceamento, começa em 50: defesa 50 reduz pela metade o dano antes do arredondamento. Bloqueio não protege contra DoTs.

Para testar sangramento com a fixture original (atributos 5), use seed **27**, resolva o ataque e clique três vezes em **Avançar fim de turno do alvo**. O botão fica indisponível ao expirar o efeito ou morrer o alvo. Cada novo ataque reinicia HP e status; não é uma batalha completa. A espada possui `attack.bleed` provisório: coeficiente 0,1 e duração 3. A renovação é verificada em testes isolados, não pela sequência de ataques dessa tela.

O perfil provisório da espada fica em `src/content/espada_teste.json`: `attack.critMultiplier`, `attack.variationMin` e `attack.variationMax`. A interface lê esses campos validados, sem definir regras de arma. Exercício opcional: altere as duas variações para `1`, salve e repita uma seed; a variação será exatamente 100%. Depois restaure `0.95` e `1.05`.

No terminal, dentro desta pasta, use Node 24.16.0 e npm 11.13.0:

```powershell
npm ci
npm run dev
```

Abra o endereço mostrado pelo Vite (normalmente http://127.0.0.1:5173). Se o diagnóstico já estiver aberto, não inicie outro servidor na mesma porta. Ctrl+C encerra o servidor no terminal.

- `npm run typecheck`: verifica tipos TypeScript.
- `npm run lint`: verifica padrões do código e dependências proibidas no núcleo.
- `npm run test`: executa os testes uma vez; `npm run test:watch` acompanha alterações.
- `npm run build`: verifica tipos e gera a pasta descartável `dist/`.
- `npm run check`: executa lint, testes e build em sequência.
- `npm run preview`: serve o build já gerado para conferência local.

O arquivo de lock registra a árvore exata instalada. `npm ci` reinstala essa árvore; não altere versões para corrigir um erro sem investigar a causa.

## Onde fica cada parte

- `src/core/`: RNG puro, executável sem navegador.
- `src/data/`: schemas Zod e validação de referências, sem interface.
- `src/content/`: JSONs válidos de teste, com números provisórios.
- `src/ui/`: diagnóstico HTML/CSS e amostra estática do PixiJS.
- `tests/`: testes Node e fixtures inválidas isoladas.

## Dois exercícios

1. Abra `src/content/character.json`, altere apenas `name`, salve e observe a tela. Essa é uma alteração de conteúdo; a lógica não precisou mudar.
2. No mesmo arquivo, troque temporariamente o número de `STR` pelo texto `"forte"`. Observe o diagnóstico com arquivo e campo. Restaure o número e execute `npm run check` para voltar ao estado válido. Não cometa o erro proposital como conteúdo normal.

Seed é o ponto inicial de uma sequência pseudoaleatória. Na tela, gere duas vezes com 42: os resultados devem coincidir. Esse gerador não é criptográfico e não oferece segurança contra hacks; na fase online a autoridade será o servidor.

## Verificação da entrega

Em 2026-09-11 passaram 14 testes em Node, lint, tipos e build. No navegador local foram confirmados personagem/equipamentos, renderização PixiJS e repetição da seed. Compatibilidade Android/iOS e distribuição mobile ainda não foram testadas.

## Documentação interna

- [Brief do projeto](documentacao/interno/01-project-brief.md)
- [MVP e playtests](documentacao/interno/02-mvp-e-playtests.md)
- [Combate e buildcrafting](documentacao/interno/03-combate-e-buildcrafting.md)
- [Progressão, itens e economia](documentacao/interno/04-progressao-itens-e-economia.md)
- [UX, direção visual e assets](documentacao/interno/05-ux-direcao-visual-e-assets.md)
- [Arquitetura técnica](documentacao/interno/06-arquitetura-tecnica.md)
- [Backlog](documentacao/interno/07-backlog.md)
- [Histórico de alterações](documentacao/interno/CHANGELOG.md)

## Fases detalhadas

As especificações de desenvolvimento disponíveis ficam em [documentacao/interno/fases/](documentacao/interno/fases/). A Fase 03 não possui documento e foi intencionalmente omitida por enquanto.

## Convenções

Os documentos distinguem três estados: **confirmado** (decisão tomada), **provisório** (direção atual sujeita a validação) e **aberto** (sem decisão). O responsável por decisões de produto, design e priorização é Diego.
```
