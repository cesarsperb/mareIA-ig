Componente 6 do DAK — *Decision-support logic*. Fonte estruturada: `l2/6-decision-logic.csv`.
Implementada no L3 como `Library` (CQL) + `PlanDefinition`.

> A plataforma **apoia** a decisão por **protocolo auditável** (RF-PS05) e por **IA com XAI**
> (RF-PS06); o profissional mantém autonomia clínica.

### DT-1 · Classificação de risco ESAS (DMN)

Soma dos 6 domínios (0–10 cada) → `soma_esas`. **REVISAR ADR-0004** — as faixas do DAK vão até 70,
mas o máximo aritmético com 6 domínios é 60.

| Entrada: soma_esas | Saída: nivel_risco | Ação do sistema |
|---|---|---|
| 0 – 30 | **Baixo** | Exibir confirmação de envio. Sem alerta. |
| 31 – 50 | **Moderado** | Exibir confirmação. Registrar para tendência. |
| 51 – 70 | **Alto** | Exibir orientação ao cuidador. Criar alerta. Notificar profissional vinculado. |

### DT-2 · Classificação Zarit (DMN)

| Entrada: pontuacao_zarit | Saída: classificacao | Ação do sistema |
|---|---|---|
| 0 – 20 | **Leve** | Exibir resultado. Registrar histórico. Sem notificação. |
| 21 – 40 | **Moderada** | Exibir resultado. Registrar histórico. Sem notificação. |
| 41 – 88 | **Severa** | Exibir resultado ao cuidador. Notificar profissional vinculado. |

### DT-3 · Alertas ativos (RA)

| Regra | Condição de disparo | Ação do sistema |
|---|---|---|
| RA-01 | soma_esas > 50 | Criar alerta **ESAS_ALTO** + notificar profissional + mensagem ao cuidador |
| RA-02 | zarit ≥ 41 | Criar alerta **ZARIT_SEVERA** + notificar profissional |
| RA-03 | dias_sem_registro > janela_esperada | Sinalizar queda de adesão no painel do Gestor (**ADESAO_BAIXA**) |
| RA-04 | alerta.status = Aberto (sem resolução) | Manter visível no painel do Gestor como "requer atenção" |
| RA-05 | nivel_risco = Alto | Exibir mensagem bidirecional: cuidador + profissional |

### DT-4 · Lógica de agendamento

| Evento | Frequência padrão | Condição de ajuste | Responsável |
|---|---|---|---|
| Registro ESAS | Diário | 2×/dia se risco Alto recente | Profissional de saúde |
| Escala Zarit | Mensal | Semanal se Severa na última avaliação | Profissional de saúde |
| Notificação de adesão | Semanal (Gestor) | Alerta imediato se taxa < 80% em 7 dias | Sistema automático |
| Dashboard Gestor | A cada hora (view materializada) | Tempo real para alertas abertos | Sistema automático |

> Agendamento segue o padrão DMN e será implementado como `ServiceRequest.occurrence[x]`;
> frequência padrão configurada pelo profissional no cadastro do vínculo clínico.

*Fonte: DAK FamilIAr_Ativa, Componentes 6 (§6.1–6.3) e 7.*
