# Fase 13 — Hardening e lançamento

## Objetivo e gate

Preparar operação real: carga, anti-cheat, segurança, observabilidade, backups, moderação, QA e soft launch. O gate é um jogo operável com problemas detectáveis/reversíveis, economia auditável, moderação disponível e infraestrutura capaz de suportar a carga planejada.

## Escopo e regras

Inclui testes de carga de matchmaking/battle server/Hub/chat/AH/auth, revisão server-side, rate limits, proteção antiabuso, scans de dependência, logs/métricas/traces/alertas, backups/restore/RPO/RTO, rollback, GM/moderação, política de fraude/RMT/chargeback, QA browser/mobile, acessibilidade mínima, feature flags/kill switches e soft launch com dashboards. Não inclui escala global garantida no dia 1, guildas/cases pesados, moderação totalmente automática ou uptime sem dados.

Observabilidade correlaciona request/battle/transação, mantém dados sensíveis fora dos logs e dispara alertas acionáveis. Ações GM são auditadas e não alteram ativos sem trilha. Em incidente econômico, alerta, kill switch, investigação de ledger, identificação de contas, correção, reversão segura e monitoramento são sequenciais. Soft launch começa por cohort limitada e só expande com gates operacionais.

## Validação e entregáveis

Testar carga concorrente, restart de battle service, falha/restore de banco, retry de pagamento, abuso de endpoints/replay/tampering/spam, permissões GM e QA de navegadores/dispositivos. Medir uptime/erros, P95/P99, fila/matchmaking, crashes, reconexão, Gold criado/destruído, moderação e retenção. Abertos: CCU, regiões, RMT e SLA interno. Entregáveis: security review, load test, dashboards/alertas, runbooks, backups/restore, GM/moderação, matriz QA e relatório de soft launch.
