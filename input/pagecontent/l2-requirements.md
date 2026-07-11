Componente 8 do DAK (Componente 9 no documento fonte) — *Functional and non-functional
requirements*. Fonte: `l2/_l1-facts.yaml`. No L3: `CapabilityStatement` (capacidades FHIR) e
`Requirements`.

### Requisitos Funcionais

| Id | Persona | Requisito | Critério de aceitação |
|---|---|---|---|
| RF-PC01 | Cuidador/Paciente | Registrar sintomas via formulário ESAS (6 campos 0–10) | Campos obrigatórios; risco calculado e exibido imediatamente; timestamp imutável |
| RF-PC02 | Cuidador | Responder Escala Zarit (22 itens, 0–4) | 22 itens obrigatórios; pontuação e classificação exibidas; notificação se Severa |
| RF-PC03 | Cuidador/Paciente | Enviar mensagem ao profissional via chat seguro | Mensagem não vazia; canal criptografado; histórico mantido |
| RF-PC04 | Cuidador/Paciente | Acessar módulos educativos por categoria | Acesso registrado em ACESSO_MODULO com timestamp |
| RF-PC05 | Cuidador/Paciente | Consultar direitos e rede de apoio (SUS) | Seção disponível offline; contatos de serviços incluídos |
| RF-PS01 | Profissional | Dashboard consolidado de pacientes ativos | Tempo real; filtros por período e risco |
| RF-PS02 | Profissional | Receber e resolver alertas clínicos | Alerta automático; status rastreável; observação clínica registrada |
| RF-PS03 | Profissional | Gráficos de tendência de sintomas (14 dias) | Por paciente e por domínio ESAS |
| RF-PS04 | Profissional | Responder mensagens de cuidadores | Histórico acessível; notificação de nova mensagem |
| RF-PS05 | Profissional | Detecção de risco por protocolo auditável | Regras DMN documentadas; resultado explicável |
| RF-PS06 | Profissional | Predição de risco com IA e XAI | Score de probabilidade; fatores explicados por XAI |
| RF-GT01 | Gestor/SUS | Indicadores epidemiológicos agregados (desidentificados) | IND-01 a IND-07 disponíveis; sem acesso a dados individuais |
| RF-GT02 | Gestor/SUS | Exportar relatório de pacientes em PDF | Filtros por período, profissional e diagnóstico; geração < 30 s |

### Requisitos Não-Funcionais

| Id | Categoria | Requisito |
|---|---|---|
| RNF-01 | Segurança | Criptografia em trânsito (TLS 1.3) e em repouso (AES-256); conformidade **LGPD** |
| RNF-02 | Autenticação | Acesso por perfil com MFA; Row Level Security (RLS) no banco |
| RNF-03 | Responsividade | Mobile (≤ 375px) e web; resposta < 2s para o ESAS |
| RNF-04 | Interoperabilidade | **HL7 FHIR R4**; integração e-SUS APS e **RNDS** via FHIR; LOINC, SNOMED CT, CID-10 |
| RNF-05 | Disponibilidade | SLA 99,5% para coleta; **modo offline** para ESAS com sincronização |
| RNF-06 | Escalabilidade | PostgreSQL com schemas por módulo (auth, clinical, alerts, messaging, education, analytics); crescimento até TRL 7 |
| RNF-07 | Privacidade | Gestor acessa apenas views desidentificadas (schema analytics); dados individuais só ao profissional vinculado |
| RNF-08 | Acessibilidade | WCAG 2.1 AA; fontes ≥ 16px em mobile; contraste ≥ 4.5:1; leitores de tela |

*Fonte: DAK FamilIAr_Ativa, Componente 9 (§9.1–9.2).*
