# MVP e playtests

## Recorte confirmado

O MVP é uma experiência local para PC web: o participante enfrenta uma IA determinística em duelo 1x1 por turnos. As builds disponíveis são fixas e preparadas para teste; o objetivo não é validar progressão, economia ou interface final.

| Inclui | Não inclui |
| --- | --- |
| Duelo 1x1, turnos alternados e uma ação principal por turno | PvP online, matchmaking ou chat |
| IA local determinística | Conta, salvamento entre sessões ou backend |
| Builds fixas contrastantes | Criação livre, classe permanente ou inventário |
| Feedback de ações, dano, crítico e status | Arte final, Hub, narrativa ou monetização |

## Fluxo de playtest

1. Apresentar a build fixa do participante e a build da IA.
2. Explicar as ações e os dados visíveis antes da primeira decisão.
3. Jogar um duelo completo contra a IA.
4. Registrar a compreensão do participante, as decisões tomadas e os momentos de impacto.
5. Coletar feedback estruturado ao término; repetir com outra build quando útil.

## IA e reprodutibilidade

A IA deve seguir as mesmas regras do jogador. O combate precisa poder ser repetido sob condições idênticas, incluindo a seed de RNG quando ela existir. Isso permite comparar escolhas e investigar resultados sem atribuí-los a variação não reproduzível.

## Critérios de avaliação

### Rodada comparativa atual — 2026-09-12

Diego validou funcionalmente painel, IA, histórico, composição espada/sangramento contra cajado/cura e resumo de métricas. Isso não registra ainda aprovação de diversão, equilíbrio ou valor estratégico.

Roteiro sugerido sem mudança de parâmetros:

1. Jogar com espada contra a IA do cajado e anotar seed e resultado antes de reiniciar, pois não há persistência.
2. Repetir a mesma seed variando uma decisão: atacar ou bloquear antes de um ataque adversário. A mudança de comandos pode alterar a posição dos sorteios; mesma seed sozinha não garante os mesmos acertos.
3. Avaliar se o turno gasto em defesa pareceu recompensado, considerando também os DoTs que ignoram bloqueio.
4. Observar se a cura adversária exige mudar a estratégia e se a pressão do sangramento é perceptível. Para experimentar a cura diretamente, desativar a IA e controlar o cajado manualmente.
5. Registrar impressão de crítico/esquiva e uma decisão que foi difícil ou que pareceu óbvia demais.

Feedback ainda pendente: valor percebido do bloqueio (prioridade pela decisão de Diego de recompensar a ação defensiva), identidade das builds e percepção de justiça do RNG. Não ajustar pesos nem aprovar G1–G3 apenas pela ausência de bugs. Não há número obrigatório de partidas ou meta de vitória inventada nesta rodada.

Um playtest é informativo quando responde, no mínimo:

- O participante entendeu quais ações estavam disponíveis e seus custos/efeitos?
- A escolha a cada turno teve valor estratégico percebido?
- Dano, bloqueio, dodge, crítico e status pareceram compreensíveis?
- O crítico gerou impacto satisfatório sem invalidar outras builds?
- O participante quer experimentar outra combinação ou revanche?

Não há meta numérica de aprovação definida nesta etapa. Diego decide quando a evidência qualitativa é suficiente para ampliar o MVP.
