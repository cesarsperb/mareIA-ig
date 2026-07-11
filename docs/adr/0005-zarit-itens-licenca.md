# ADR-0005 — Itens da Escala Zarit (ZBI-22): copyright e placeholders

- **Status:** PROPOSTO — aguarda definição de licenciamento pela equipe do projeto
- **Bloqueia:** Questionnaire Zarit completo no L3 (texto dos itens)

## Contexto
O DAK (§5.2) especifica a Escala Zarit com **22 itens (0–4 cada; total 0–88)** e classificação
0–20 Leve / 21–40 Moderada / 41–88 Severa (§6.2), mas **não transcreve o texto dos itens**.
O Zarit Burden Interview (ZBI-22, Zarit, Reever & Bach-Peterson) é um instrumento protegido por
direitos autorais; suas traduções validadas para o PT-BR também têm titularidade própria.

## Questões abertas (não decidir sozinho)
1. Definir a **versão/tradução** do ZBI-22 a ser usada (validação brasileira) e obter a
   **licença de uso** correspondente.
2. Confirmar se a pontuação por item é 0–4 no formato Likert da versão licenciada.
3. Avaliar código LOINC para o escore total do ZBI (há códigos LOINC para instrumentos de
   sobrecarga do cuidador; conferir aplicabilidade) — hoje usa código local
   `familiarativa-obs-code#zarit-total-score`.

## Decisão provisória
O `Questionnaire/familiarativa-zarit` usa **placeholders** ("Item N da Escala Zarit…") com
`status: draft` e nota de copyright, preservando linkIds (`z01..z22`), tipos e limites (0–4).
O texto oficial só entra no repositório mediante licença. A lógica de pontuação/classificação
(L2 §6.2) não depende do texto dos itens e está codificada normalmente.
