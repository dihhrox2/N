# Fase 10 — Mercado entre jogadores

## Objetivo e gate

Abrir economia social com Auction House e trade auditáveis. O gate exige circulação de itens/Gold com integridade, atomicidade e rastreabilidade suficientes para operar economia real.

## Escopo e regras

Inclui AH com busca/filtros, criação/cancelamento/compra de listing, taxa, limites por conta, trade item/Gold com dupla confirmação, BOE/BOA, ledger, escrow/ownership, proteção contra duplicação/race condition, detecção inicial de wash trading e ferramentas administrativas. Não inclui RMT oficial, leilão complexo, crafting ou guild bank.

## Validação e entregáveis

Servidor é fonte de verdade para owner, bind e localização; item tem estado locked durante listing/trade. Compra debita comprador, credita vendedor menos taxa e transfere item atomicamente. Qualquer alteração reinicia confirmações de trade; logs têm IDs e trilha de auditoria. Testar compra concorrente, cancelamento, reconnect, commit repetido, saldo insuficiente, taxa, overflow e payload manipulado. Abertos: política RMT, cosmético BOA e expiração. Entregáveis: AH, trade, escrow/ownership, ledger, painel admin e antiabuso.
