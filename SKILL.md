---
name: para-raios
description: >-
  MANUAL-ONLY skill: NÃO auto-invocar. Gera um plano de risco e segurança de IA para um
  projeto/produto do Bera: mapeia o sistema (incl. agentes e pipelines autônomos), preenche um
  checklist NIST Cybersecurity Framework, cruza com biblioteca de ameaças (OWASP Top 10 for
  LLM/Agentic, MITRE ATLAS, Google SAIF), faz checagem de transparência do EU AI Act, e entrega
  tabela + memo à liderança + recomendações priorizadas, escalado ao tamanho do projeto (solo →
  equipe → enterprise). Acionar EXCLUSIVAMENTE quando o Bera pedir de forma explícita e nominal, via
  `/para-raios` ou frase como "usa o para-raios", "chama o para-raios", "manda o para-raios fazer o
  plano de risco", "joga o para-raios nesse projeto". Pedidos genéricos sobre risco, segurança,
  NIST, OWASP, ameaças de IA, cibersegurança ou "analisa a segurança do meu projeto" NÃO são
  gatilhos válidos para esta skill; nesses casos, responder normalmente sem invocá-la (no máximo,
  sugerir em texto que o Bera pode chamá-la). Em dúvida, NÃO invoque.
---

# para-raios — plano de risco & segurança de IA

> Aterra o risco antes de virar incidente. Pega qualquer projeto/produto e produz um **plano de risco
> e segurança de IA** acionável, honesto e escalado ao tamanho — usando o **NIST CSF** como moldura e
> uma biblioteca de frameworks de IA (NIST AI RMF, OWASP, MITRE ATLAS, SAIF, EU AI Act) como conteúdo.
> Nasceu da Atividade 4 do MIT (IA Agêntica) + pesquisa comparativa de frameworks.

## Quando isto roda
Só sob invocação nominal (ver `description`). Quando roda, o objetivo é entregar um plano que o Bera
possa **usar com C-level/mídia** ou **submeter como exercício** — não um relatório genérico.

## Princípios (o que faz a diferença)
1. **Não inventar.** Toda observação/risco se ancora em **fato real do projeto** (código, config,
   deploy, dados). Se algo é desconhecido, escreva "Não tenho certeza" e diga o que faltou checar — é
   mais útil (e honesto) que um "Sim" otimista. Um plano todo verde não serve a ninguém.
2. **"O agente" pode não ser um LLM.** Muitos projetos do Bera não têm LLM em runtime, mas têm um
   **sistema autônomo** (pipeline CI/CD que ingere dados, decide e faz deploy sem humano). Esse é um
   "agente" legítimo e o objeto natural do plano. Identifique o que age sozinho sobre produção.
3. **Escalar ao tamanho.** Um site solo não precisa de ISO 42001. Escolha o tier (abaixo) e ajuste a
   profundidade. Excesso de framework é tão ruim quanto falta.
4. **Honestidade calibrada.** Aponte os controles reais que existem E os gaps reais. O valor do plano
   está nos gaps — é o que a liderança precisa decidir.
5. **Verificar antes de afirmar.** Leia o repo/projeto direto. Se um subagente mapear, reconfira os
   fatos que você vai escrever (versões, frequências, existência de gates).

## Tiers (escolha 1 — pergunte ao Bera se ambíguo)
- **T1 · Solo/pequeno** — site estático, projeto pessoal, pipeline automatizado, 0–1 dev.
  Backbone: NIST CSF (12 perguntas) + ~5 ameaças OWASP aplicáveis + checagem de transparência.
- **T2 · Equipe/produto** — produto com usuários reais, equipe pequena.
  + papéis/treinamento, runbook de incidente, monitoramento ativo, mais OWASP/MITRE, SAIF.
- **T3 · Enterprise/regulado** — escala, dados sensíveis, exposição regulatória.
  + ISO/IEC 42001 (AIMS, certificação), EU AI Act completo, MITRE ATLAS red-team, governança formal.

## Workflow
Execute em ordem; pule o que não se aplica (diga que pulou e por quê).

### 1. Mapear o projeto e definir "o agente"
Inventarie, lendo o projeto direto: o que o sistema/agente **acessa** (APIs, dados, ferramentas,
credenciais, deploy), o que **decide e faz sozinho**, onde vivem **secrets**, qual a **superfície**
(inputs, endpoints públicos, conteúdo gerado) e como **publica** (CI/CD). Defina explicitamente o que
conta como "o agente" — se não há LLM, é o sistema autônomo.

### 2. Escolher o tier
Pelo inventário, classifique T1/T2/T3. Se ambíguo, pergunte. O tier define a profundidade dos passos.

### 3. Preencher o checklist NIST CSF
Use `references/nist-csf-checklist.md` — as 12 perguntas-base (Identificar/Proteger/Detectar/Responder/
Recuperar) + extensões agênticas (T2/T3). Para cada: **Sim / Não / Não tenho certeza** + **Observação
ancorada em fato**. Cite o arquivo quando aplicável.

### 4. Cruzar com a biblioteca de ameaças
Use `references/threat-library.md` (OWASP Top 10 LLM/Agentic + MITRE ATLAS + SAIF). Filtre o que **se
aplica** ao projeto; para cada ameaça aplicável, registre o **vetor** e a **mitigação**. Não liste o
catálogo inteiro — só o relevante, com o porquê.

### 5. Checagem de transparência & legal (EU AI Act lite)
Use `references/frameworks.md` §EU AI Act. Pergunte: usa IA? Precisa **rotular saída de IA** (Art. 50)?
Toca **prática proibida** (Art. 5)? É **alto risco** (Anexo III)? Para T1 normalmente é risco mínimo/
transparência; sinalize só o que aplica.

### 6. Sintetizar o plano
Monte o entregável com `assets/template-plano.md`: mapa → tabela NIST CSF → ameaças aplicáveis →
transparência → **recomendações priorizadas** (quick wins vs estruturais) → memo à liderança (250–500
palavras, se pedido) → disclosure de uso de IA (se for entregável acadêmico/externo).

### 7. Renderizar
Entregue **Markdown** sempre (fonte). Se pedirem **PDF/Word**, use `assets/print-template.html` +
headless Chrome (comando no topo do arquivo). Cor-com-função na tabela (Sim=verde, Não=vermelho,
Incerteza=âmbar) — sem decoração gratuita.

## Regras de ouro
- Nunca copie um valor de secret/token para o entregável — mencione que existe e onde, não o valor.
- Voz do Bera: business-side, framing de valor; C-level e mídia entendem sem jargão.
- Se for submissão acadêmica (ex.: MIT), inclua o disclosure de IA e lembre que o autor verifica/edita.
- Frameworks evoluem; `references/frameworks.md` tem data da pesquisa — reconfira versões em material
  público.

## Arquivos
- `references/nist-csf-checklist.md` — perguntas NIST CSF (base + agênticas) e como respondê-las.
- `references/threat-library.md` — OWASP/MITRE/SAIF: ameaças aplicáveis + mitigações.
- `references/frameworks.md` — os 6 frameworks (o que é, quando usar, fontes).
- `assets/template-plano.md` — template do entregável.
- `assets/print-template.html` — esqueleto de print-CSS + comando de PDF.
- `SPEC.md` — design, escopo e proveniência da skill.
