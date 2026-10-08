# para-raios

> Claude Code skill — gera um **plano de risco e segurança de IA** acionável, honesto e escalado ao tamanho do projeto, usando o **NIST Cybersecurity Framework** como moldura e uma biblioteca de frameworks de IA (NIST AI RMF, OWASP Top 10 for LLM/Agentic, MITRE ATLAS, Google SAIF, EU AI Act) como conteúdo.

> Aterra o risco antes de virar incidente. Nasceu da Atividade 4 do MIT (IA Agêntica) + pesquisa comparativa de frameworks.

## O que esta skill faz

Quando acionada sobre um projeto/produto, ela:

- **Mapeia o sistema** — o que ele acessa, decide e faz sozinho; onde vivem secrets; a superfície (inputs, endpoints, conteúdo gerado); como publica (CI/CD). Trata pipelines autônomos como "agente" mesmo sem LLM em runtime.
- **Escala ao tamanho** — escolhe um tier (T1 solo · T2 equipe/produto · T3 enterprise/regulado) e ajusta a profundidade. Excesso de framework é tão ruim quanto falta.
- **Preenche um checklist NIST CSF** — Identificar / Proteger / Detectar / Responder / Recuperar, com Sim / Não / Não tenho certeza + observação ancorada em fato real do projeto.
- **Cruza com biblioteca de ameaças** — OWASP Top 10 for LLM/Agentic, MITRE ATLAS, Google SAIF: só o que se aplica, com vetor e mitigação.
- **Faz checagem de transparência (EU AI Act lite)** — rotulagem de saída de IA (Art. 50), práticas proibidas (Art. 5), alto risco (Anexo III).
- **Entrega** — mapa → tabela NIST CSF → ameaças aplicáveis → transparência → recomendações priorizadas (quick wins vs estruturais) → memo à liderança → disclosure de uso de IA. Markdown sempre; PDF/Word sob demanda.

**Modo injeção** (`/para-raios injeção`): audita um projeto contra prompt injection pela Rule of Two, confere quatro camadas (regra escrita, aviso do runtime, portão de ação e memória, teste), roda uma bateria de injeção plantada com canário (`scripts/injecao_plantada.py`) e conduz a refatoração, uma mudança por vez com aprovação. Só em projeto próprio, com payload inofensivo. Fonte única: `references/prompt-injection.md`.

Princípio central: **não inventar**. Toda observação se ancora em fato real; o que é desconhecido vira "Não tenho certeza" com o que faltou checar. Um plano todo verde não serve a ninguém — o valor está nos gaps reais.

## Como invocar (depois de instalada)

Esta é uma skill **manual-only**: ela **nunca** auto-invoca. Aciona-se apenas de forma explícita e nominal:

- **Slash command:** `/para-raios [seu projeto/pedido]` ou `/para-raios injeção [projeto]`
- **Frase de invocação:** "usa o para-raios", "chama o para-raios", "manda o para-raios fazer o plano de risco", "joga o para-raios nesse projeto".

Pedidos genéricos sobre risco, segurança, NIST, OWASP ou "analisa a segurança do meu projeto" **não** acionam a skill — por design.

## Instalação

Copie a pasta para o diretório de skills do Claude Code:

```bash
git clone https://github.com/beralzir/para-raios.git ~/.claude/skills/para-raios
```

Para uma instalação por projeto, use `.claude/skills/para-raios` dentro do repo.

## Arquivos

- `SKILL.md` — a skill: princípios, tiers e workflow de 7 passos.
- `SPEC.md` — design, escopo e proveniência.
- `references/nist-csf-checklist.md` — perguntas NIST CSF (base + agênticas) e como respondê-las.
- `references/threat-library.md` — OWASP / MITRE ATLAS / SAIF: ameaças aplicáveis + mitigações.
- `references/frameworks.md` — os frameworks (o que é, quando usar, fontes).
- `references/prompt-injection.md`: modo injeção: premissa, Rule of Two, camadas, bateria plantada, refatoração.
- `scripts/injecao_plantada.py`: bateria de injeção plantada (só stdlib).
- `assets/hook-p13.py`: hook do aviso de origem externa.
- `assets/template-plano.md` — template do entregável.
- `assets/print-template.html` — esqueleto de print-CSS + comando de PDF.

## Nota

Frameworks de segurança de IA evoluem. `references/frameworks.md` traz a data da pesquisa — reconfira versões em material público antes de usar como referência canônica.

## Licença

MIT © 2026 Renato Beralzir
