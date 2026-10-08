# [Projeto] — Plano de risco & segurança de IA

**Organização/projeto:** [nome + 1 linha do que é + URL]
**Tier:** [T1 solo · T2 equipe · T3 enterprise]
**Data:** [DD/mês/AAAA]

---

## 1. Mapa — o que é "o agente"
[1 parágrafo: defina o sistema/agente avaliado. Se não há LLM em runtime, nomeie o sistema autônomo
(ex.: pipeline CI/CD). Liste: o que acessa (APIs/dados/ferramentas/credenciais/deploy), o que decide e
faz sozinho, onde vivem secrets, superfície (inputs/endpoints/conteúdo gerado), como publica.]

## 2. Checklist NIST Cybersecurity Framework

| Categoria | Pergunta | Sim / Não / Não tenho certeza | Observações (ancoradas em fato) |
|---|---|---|---|
| **Identificar** | Sabemos quais sistemas, dados e ferramentas o agente pode acessar? | | |
| | Pensamos em como esse agente se encaixa no ambiente da organização? | | |
| | Consideramos os riscos de dar a esse agente acesso a tarefas confidenciais? | | |
| **Proteger** | Podemos controlar com quem o agente fala e o que ele pode ver ou fazer? | | |
| | As pessoas foram treinadas sobre o que o agente pode e não pode fazer? | | |
| | Os dados confidenciais estão protegidos contra vazamentos pelo agente? | | |
| **Detectar** | Temos como identificar se o agente está fazendo algo incomum ou errado? | | |
| | Há alguém/algo monitorando o comportamento regularmente? | | |
| **Responder** | Se algo der errado, temos um plano para consertar rapidamente? | | |
| | Sabemos quem notificar e como comunicar o problema? | | |
| **Recuperar** | Poderíamos recuperar dados ou serviços se o agente causasse um problema? | | |
| | Temos um plano para melhorar o agente após um incidente? | | |

> **T2/T3:** acrescente as extensões agênticas de `references/nist-csf-checklist.md`
> (permissões de ferramentas, ações irreversíveis, prompt injection, memória, multi-agente).

## 3. Ameaças aplicáveis (OWASP / MITRE ATLAS / SAIF)
[Só as que se aplicam. Tabela: ameaça (ID) · vetor neste projeto · mitigação. Ver `threat-library.md`.]

| Ameaça | Por que se aplica aqui | Mitigação |
|---|---|---|
| | | |

## 4. Transparência & legal (EU AI Act lite)
[Usa IA? Rotula saída de IA (Art. 50)? Toca prática proibida (Art. 5)? Alto risco (Anexo III)?
Para T1 normalmente risco mínimo/transparência — sinalize só o que aplica.]

## 5. Recomendações priorizadas
**Quick wins (baixo esforço, alto retorno):**
- [...]

**Estruturais (planejar):**
- [...]

## 5b. Modo injeção (*só quando o modo injeção rodou*)
**Mapa (Rule of Two por fluxo):**

| Fluxo | [A] entrada de fora | [B] dado privado | [C] muda estado ou sai | Humano antes de C? | Veredito |
|---|---|---|---|---|---|
| | | | | | |

**Camadas:**

| Camada | Situação | Portão | Prova |
|---|---|---|---|
| C1 Regra escrita | | mole | |
| C2 Aviso do runtime (P13) | | reforço | |
| C3 Ação e memória | | duro | |

**Teste plantado (`scripts/injecao_plantada.py`):**

| Caso | Antes | Depois | Observação |
|---|---|---|---|
| md-acao | | | |
| email-memoria | | | |
| html-exfil | | | |
| codigo-commit | | | |
| transcricao-desvio | | | |

**Mudanças aplicadas:** [uma por linha, com o arquivo e o commit se o dono já fez, senão "pendente de commit"]
**Risco aceito:** [o que ficou aberto, por quê e quem decidiu]

## 6. Memo à liderança (250–500 palavras) — *opcional*
[Voz de negócio. Onde estamos fortes · onde estamos expostos · quem envolver · especialistas ·
treinamentos · procedimentos de emergência · próximo passo sugerido.]

## 7. Apêndice — Declaração de uso de IA — *se for entregável acadêmico/externo*
- **Ferramenta:** [ex.: Claude Code / Opus 4.8, Anthropic] · **Data:** [...] · **URL:** [...]
- **Como foi usada:** [estruturou a análise a partir de fatos verificáveis do projeto].
- **Verificação e responsabilidade:** afirmações checadas contra o código/config; revisão e edição
  finais são do autor, que assume integralmente o conteúdo.
- **Citação (APA):** [...] · **Guia:** MIT Libraries — https://libguides.mit.edu/cite-AI-tools
