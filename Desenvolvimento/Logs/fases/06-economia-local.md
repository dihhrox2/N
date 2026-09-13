# Fase 06 — Economia local

## Objetivo e gate

Validar Gold, durabilidade, NPCs e Auction House simulada antes de qualquer comércio real. O gate exige que Gold entre e saia de forma mensurável/sustentável em simulações e que sinks façam sentido sem dinheiro real.

## Escopo e regras

Inclui carteira de Gold por personagem, recompensas locais PvE/PvP, compra/venda NPC, serviços, consumíveis, durabilidade/reparo, expansões por Gold, mock de AH, taxa/slots e relatório de fontes/sinks. Não inclui trade, contas, transferência real de Gold, cosméticos pagos, VIP ou fraude de produção.

Todo crédito/débito registra categoria, motivo e identificador; saldo não fica negativo e nenhuma UI altera saldo diretamente. Desgaste é configurável e item não zera sem estado quebrado/reparo. NPC evita arbitragem infinita; o mock de AH valida UX/economia, sem concorrência real.

## Fluxos, validação e entregáveis

O ciclo recebe item, equipa/guarda/vende/anuncia, aplica BOE, desgasta em batalha e repara com Gold. Transações validam saldo/regra, registram ledger e retornam motivo. Testar saldo negativo, arbitragem NPC, taxa, reparo e simulações casual/regular/hardcore. Medir Gold/hora, fontes/sinks, saldo, gastos e itens vendidos. Abertos: taxa/desgaste, taxa de AH e preço de NPC. Entregáveis: carteira/ledger, NPC, durabilidade, mock de AH e relatório econômico.

