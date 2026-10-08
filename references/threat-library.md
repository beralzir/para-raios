# Biblioteca de ameaças — OWASP · MITRE ATLAS · SAIF

Lookup para o Passo 4. **Filtre o que se aplica** ao projeto; para cada ameaça aplicável registre
*vetor neste projeto* + *mitigação*. Não despeje o catálogo — só o relevante, com o porquê.
Verificado em 27/jun/2026 (nomenclaturas evoluem; conferir fonte oficial em material público).

## OWASP Top 10 for LLM Applications 2025
Aplica-se a qualquer app que use LLM (chatbot, RAG, geração de conteúdo).

| ID | Ameaça | Aplica quando… | Mitigação |
|---|---|---|---|
| LLM01 | Prompt Injection | há input de usuário ou conteúdo externo no prompt | não há prevenção infalível (OWASP). Limitar o que o agente faz depois de ler: privilégio mínimo, aprovação humana para ação de risco, conteúdo externo segregado e marcado, teste adversarial. Instrução de sistema ajuda e não basta. Detalhe e teste: `prompt-injection.md` |
| LLM02 | Sensitive Information Disclosure | o modelo vê dados sensíveis/PII | minimizar dados no contexto; filtrar saída; mascarar secrets |
| LLM03 | Supply Chain | usa modelos/plugins/datasets de terceiros | fixar e verificar versões; proveniência; revisar dependências |
| LLM04 | Data & Model Poisoning | há fine-tuning ou RAG com fontes abertas | validar fontes; curar dados; detectar anomalias |
| LLM05 | Improper Output Handling | a saída da IA é injetada em HTML/SQL/shell | tratar saída como não confiável; escapar/validar (anti-XSS/inj.) |
| LLM06 | Excessive Agency | o LLM aciona ferramentas/ações | least-privilege; aprovação humana p/ ações sensíveis; limitar escopo |
| LLM07 | System Prompt Leakage | o system prompt guarda segredo/lógica | não pôr segredo no prompt; assumir que vaza |
| LLM08 | Vector & Embedding Weaknesses | usa RAG/embeddings | controlar acesso ao vector store; validar o que entra no índice |
| LLM09 | Misinformation | a saída é apresentada como fato | human-in-the-loop; citar fontes; sinalizar incerteza |
| LLM10 | Unbounded Consumption | API de IA exposta a uso aberto | rate limit; budget/quota; timeouts |

## OWASP Top 10 for Agentic Applications 2026 (ASI)
Aplica-se a agentes autônomos / multi-agente. Nomes de ASI01 e ASI06 conferidos no anúncio oficial
de 09/12/2025 em 08/10/2026. Os demais seguem a pesquisa de 27/jun.

| ID | Ameaça | Aplica quando… | Mitigação |
|---|---|---|---|
| ASI01 | Agent Goal Hijack | o agente persegue objetivos a partir de input | conteúdo externo como dado; ferramentas com escopo; confirmação humana em ação de risco. Ver `prompt-injection.md` |
| ASI02 | Tool Misuse | o agente usa ferramentas/APIs | least-privilege; allowlist de tools; sandbox |
| ASI03 | Identity & Privilege Abuse | o agente tem credenciais próprias | escopo mínimo; rotação; separar identidade do agente |
| ASI04 | Agentic Supply Chain | usa tools/plugins/modelos de terceiros | proveniência; verificação; pinning |
| ASI05 | Unexpected Code Execution (RCE) | o agente executa código | sandbox; sem exec arbitrário; isolar |
| ASI06 | Memory & Context Poisoning | o agente tem memória persistente | nada de fora entra na memória sem confirmação do dono; gravar com origem; isolar contexto por sessão. Ver `prompt-injection.md` |
| ASI07 | Insecure Inter-Agent Communication | há múltiplos agentes | autenticar/assinar mensagens; canal seguro |
| ASI08 | Cascading Failures | cadeia/orquestração de agentes | circuit breakers; limites; observabilidade |
| ASI09 | Human-Agent Trust Exploitation | usuários confiam no agente | transparência; rotular como IA; limites claros |
| ASI10 | Rogue Agents | agente autônomo em produção | kill switch; revogação de credenciais; monitoramento |

## MITRE ATLAS — usar como checklist de ameaça adversarial
Base estilo ATT&CK (16 táticas, ~170 técnicas). Não percorra tudo — marque o plausível e adote a
mitigação (AML.M) correspondente. Táticas: Reconnaissance · Resource Development · Initial Access ·
AI Model Access · Execution · Persistence · Privilege Escalation · Defense Evasion · Credential Access ·
Discovery · Lateral Movement · Collection · AI Attack Staging · Command and Control · Exfiltration ·
Impact. Para projeto pequeno, os vetores típicos: prompt injection, RAG/data poisoning, AI supply-chain
compromise, exfiltração via saída do modelo. Fonte: atlas.mitre.org.

## Google SAIF — secure-by-default (controles)
Riscos nativos de IA cobertos: prompt injection, data poisoning, model source tampering, rogue actions,
memory poisoning. Para projeto pequeno, o aproveitável é o **Risk Assessment interativo** (saif.google)
como triagem + as fundações secure-by-default que todo projeto já deveria ter: **secrets fora do repo,
least-privilege no CI/CD, dependências assinadas/verificadas**. Workstreams de supply chain de ML pesada
só quando houver IA própria sendo treinada/servida.

## Atalho por tipo de projeto
- **Site estático + pipeline autônomo (sem LLM):** foco em LLM03/ASI04 (supply chain), least-privilege
  no deploy (ASI02/ASI03), validação de dados de entrada (≈LLM04), saída em HTML (LLM05/XSS), custo (LLM10).
- **App com LLM (chatbot/RAG):** LLM01, LLM02, LLM05, LLM06, LLM08, LLM10 + transparência (ASI09/Art. 50).
- **Agente que age (deploy/PRs/compras):** + ASI01, ASI02, ASI03, ASI05, ASI10 + kill switch + aprovação humana.
