# Fase 05 — Progressão local

## Objetivo e gate

Adicionar crescimento offline/local: XP, nível sem teto artificial, atributos, árvore de classe, biblioteca, inventário e drops determinísticos. O gate é o loop compreensível combater, receber XP/item, evoluir, alterar build e combater novamente sem rede.

## Escopo e requisitos

Inclui um ponto de atributo por nível, Noob no nível 1, classe-base no 10 e Classes II/III nos 30/60 configuráveis, escolhas exclusivas/irreversíveis, duas skills/Ultimate/passiva por classe, quatro slots livres, inventário por personagem, 20–30 slots configuráveis, stacks de consumível, item por ID+raridade sem rolls, BOE e drops por família de inimigo. Não inclui Gold/economia, AH, conta online, VIP/respec real ou Ranked.

Persistir histórico de XP e mudança importante, usar comandos de classe com confirmação e versionar schema do save local. O item recebido pode ser inspecionado, equipado e vinculado; depois de vinculado não transfere entre personagens.

## Validação, riscos e entregáveis

Testar múltiplos níveis, ponto único após reload, classe irreversível, stats idênticos por raridade, BOE, stacks e inventário cheio. Medir tempo para marcos, atributos por nível, distribuição de raridade e pressão de inventário. Permanecem abertos curva de XP, quantidade de stats por raridade e overflow local. Entregáveis: módulo de progressão, árvore inicial, inventário/BOE, tabelas de drop/raridade e save/load local.
