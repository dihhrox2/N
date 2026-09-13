# Fase 07 — Multiplayer PvP

## Objetivo e gate

Levar o combate para rede com servidor autoritativo. Dois jogadores em dispositivos/navegadores distintos devem concluir 1x1 consistente, com reconexão funcional e resultado decidido exclusivamente pelo servidor.

## Escopo e regras

Inclui conta/autenticação básica, persistência de personagem/build/inventário/Gold/classes, battle server autoritativo, protocolo versionado de comandos/eventos, Casual/Ranked, matchmaking por rating, lifecycle de sala, reconexão, timeout, idempotência e logs técnicos. Não inclui Hub social completo, AH real, trade, VIP/pagamentos, guildas ou Hardcore.

O cliente envia apenas intenções; servidor mantém BattleState canônico, valida turno/recursos/cooldown/ownership, resolve RNG e persiste resultado uma vez. Comandos têm ID único, sequência/turn index e eventos suficientes para animação/log. Reconexão usa snapshot validado dentro de janela configurável.

## Validação e entregáveis

Testar ação fora do turno, skill sem mana, comando duplicado, payload adulterado, perda/retorno de rede, refresh, múltiplas abas e crash entre fim/persistência. Medir fila, latência comando-evento, reconexão, abandono, validações e duração server-side. Abertos: janela de reconexão, amplitude do matchmaking e tecnologia real-time. Entregáveis: auth, persistência, battle server, protocolo, filas e logs.

