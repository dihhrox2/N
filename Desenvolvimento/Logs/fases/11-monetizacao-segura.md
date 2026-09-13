# Fase 11 — Monetização segura

## Objetivo e gate

Adicionar receita apenas por conveniência e estética, mantendo zero P2W. O gate exige que F2P dedicado alcance o mesmo teto de poder/recursos que pagante; dinheiro compra tempo, conveniência ou visual, nunca probabilidade de vencer.

## Escopo e regras

Inclui VIP por assinatura, entitlements server-side, presets/rerolls/capacidade operacional, skip de PvE já vencido manualmente, respec periódico VIP ou alternativa cara em Gold, slots/expansões e cosméticos BOA/possível revenda aprovada. Não inclui venda de stats, equipamento poderoso, energia extra que aumente máximo diário, chance de drop/crit paga, lootbox paga ou Battle Pass obrigatório.

## Validação e entregáveis

Cada benefício passa por verificação: aumenta poder máximo, recursos máximos ou chance de vencer? Se sim, reprojetar. Pagamento/webhook é idempotente, entitlement não depende de flag de cliente e refund/chargeback preserva consistência. Testar comparação F2P/VIP, custo/resultado de skip, expansão até mesmo máximo e cosmético sem efeito de batalha. Abertos: revenda, preço/período VIP e rerolls. Entregáveis: assinaturas, conveniências, loja cosmética, respec e checklist zero P2W.
