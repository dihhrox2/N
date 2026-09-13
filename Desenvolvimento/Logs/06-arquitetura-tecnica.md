# Arquitetura técnica

## Estado e limites

Linha do tempo consolidada (2026-09-12): `CommandBattle.timeline` intercala cópias dos registros do ciclo com ações, eventos derivados e resultado. Sequência é determinística e independente de relógio. Logs separados continuam disponíveis, mas consumidores não precisam tentar ordenar essas listas a posteriori. Detalhes de DoTs/mana/recargas permanecem agrupados por encerramento; não se inventa autoria de DoT ausente no estado atual.

Passivas integradas (2026-09-12): o despachante emite eventos de ataque e cura, avalia a passiva opcional do atacante uma vez por ataque e registra a cura passiva sem novo despacho. Eventos possuem sequência reproduzível; etapas do ciclo permanecem em log separado. Essa execução local não protege contra reapresentação externa de snapshots antigos e não constitui API de servidor.

Integração local de comandos (2026-09-12): `battle-commands.ts` recebe loadouts internos já validados, verifica turno/permissões/equipamento e coordena helpers atômicos com `battle-flow.ts`. Clona o estado antes de executar: rejeições não alteram HP, recursos ou cursor de RNG da entrada. O replay local reexecuta comandos com os mesmos loadouts, seed e balanceamento. Não é importador de dados externos nem protocolo seguro de rede. O cursor é reconstruído a partir da seed e quantidade de sorteios, suficiente ao protótipo; não há novo gerador aleatório.

Bloqueio e esquiva expiram na abertura do turno próprio, antes da decisão sob Stun. Poção permanece livre e de uso único; habilidades equipadas e Ultimate usam seus custos e recargas. Passivas ainda não são despachadas. Nenhuma limpeza de Stun existe neste catálogo: o despachante atual não oferece essa ação; o helper de ciclo preserva suporte a opções futuras previamente avaliadas.

A Fase 0 está implementada para PC web local em projeto único: TypeScript estrito, Vite, PixiJS, HTML/CSS, JSON validado por Zod, Vitest e ESLint. Dependências diretas usam versões exatas e package-lock.json. Servidor, banco, conta, persistência e deploy permanecem futuros.

O catálogo versão 1 contém personagem com seis atributos e quatro referências de equipamentos. Itens de teste possuem ID, nome, slot e poder provisório. O carregamento rejeita campos desconhecidos, versões diferentes, IDs duplicados e referências inexistentes ou incompatíveis. Não há interpretação desses valores como fórmulas de combate.

O RNG usa Mulberry32 com seed inteira de 32 bits e estado privado por instância. O intervalo é [0,1); testes verificam um vetor conhecido. A reprodução futura de batalhas também exige mesma versão dos dados, regras e sequência de comandos. O algoritmo não é criptográfico.

## Princípios arquiteturais confirmados

- Regras de combate, IA e jogador devem obedecer às mesmas regras.
- Classes, armas, skills, itens e inimigos devem existir como dados separados da lógica de combate.
- A simulação deve ser determinística quando receber o mesmo estado inicial e a mesma seed de RNG.
- O combate deve oferecer modo de depuração com controle dos dois lados.
- Um sandbox futuro deve permitir escolher builds e executar muitas simulações.
- A velocidade de simulação pode ser acelerada ou instantânea em contexto de teste.

## Interfaces conceituais

| Conceito | Responsabilidade |
| --- | --- |
| Estado da batalha | Representar participantes, recursos, turno, status, eventos e resultado. |
| Dados de build | Representar atributos, classe, equipamentos, skills, passiva e consumível. |
| Resolução de ação | Aplicar uma decisão válida ao estado e produzir eventos legíveis. |
| Fonte de RNG | Receber seed e produzir resultados repetíveis para crítico, hit, dodge e drops. |
| Controlador de participante | Solicitar uma ação de jogador humano, IA ou depuração sob as mesmas regras. |
| Relatório de combate | Expor resultado, duração, críticos, stuns, dano e demais indicadores para análise. |

Essas são fronteiras conceituais para orientar a decisão futura; não constituem contratos de código.

## Decisão de motor web

Diego escolheu PixiJS com regras independentes da renderização. A Fase 0 usa importação dinâmica e uma amostra estática WebGL. Capacitor é uma possibilidade futura para aplicativos mobile, ainda não instalado ou validado. Os critérios preservados para evolução são:

- renderização 2D apropriada para pixel art e interface de combate lateral;
- simplicidade para um jogo por turnos e dados separados da lógica;
- ferramentas de depuração e testes locais;
- compatibilidade com PC web;
- manutenção, documentação e peso de dependências compatíveis com um MVP.

Phaser foi considerado na descoberta; a escolha confirmada é PixiJS.
