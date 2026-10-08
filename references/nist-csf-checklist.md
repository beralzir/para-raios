# Checklist NIST CSF + extensões agênticas

As 12 perguntas-base vêm da Atividade 4 do MIT (modeladas no NIST Cybersecurity Framework). As
extensões agênticas são para T2/T3 (produtos com LLM/agente real). Responda cada uma com **Sim / Não /
Não tenho certeza** + **Observação ancorada em fato do projeto**.

## Como responder (calibração honesta)
- **Sim** = existe um controle real e verificável. Cite o artefato (arquivo, config, processo).
- **Não** = a coisa genuinamente não existe. É um gap — diga o impacto.
- **Não tenho certeza** = existe parcialmente, ou não deu para confirmar. Diga o que falta checar.
- **Evite o viés do "Sim"**: um plano todo verde é inútil. O valor está nos Nãos e Incertezas — é o
  que a liderança precisa decidir. Mire um mix realista.
- **Não invente.** Se o projeto não tem aquilo, não escreva que tem. Leia o repo/projeto e confirme.

## 12 perguntas-base

### Identificar
1. Sabemos quais sistemas, dados e ferramentas o agente pode acessar?
2. Pensamos em como esse agente se encaixa no ambiente da organização?
3. Consideramos os riscos de dar a esse agente acesso a tarefas confidenciais?

### Proteger
4. Podemos controlar com quem o agente fala e o que ele pode ver ou fazer?
5. As pessoas foram treinadas sobre o que o agente pode e não pode fazer?
6. Os dados confidenciais estão protegidos contra vazamentos pelo agente?

### Detectar
7. Temos como identificar se o agente está fazendo algo incomum ou errado?
8. Há alguém/algo monitorando o comportamento regularmente?

### Responder
9. Se algo der errado, temos um plano para consertar rapidamente?
10. Sabemos quem notificar e como comunicar o problema?

### Recuperar
11. Poderíamos recuperar dados ou serviços se o agente causasse um problema?
12. Temos um plano para melhorar o agente após um incidente?

## Extensões agênticas (T2/T3 — projetos com LLM/agente real)
Acrescente as que se aplicam; mapeiam para ameaças em `threat-library.md`.

### Identificar
- O agente tem **permissões/escopo de ferramentas** documentados (que tools, com que credenciais)?
- Mapeamos **ações irreversíveis** que ele pode tomar (deletar, transferir, publicar, gastar)?

### Proteger
- Há **least-privilege** nas ferramentas e **aprovação humana** para ações sensíveis? (OWASP LLM06/ASI02/ASI03)
- Algum fluxo junta entrada não confiável, dado privado e saída para fora sem humano no meio
  (Rule of Two)? E o que vem de fora pode virar memória sem o dono confirmar? (LLM01/ASI01/ASI06,
  ver `prompt-injection.md` §1. Envenenamento de base de dados e RAG segue em LLM04)
- A **saída do modelo** é validada antes de ser usada (evita XSS/exec)? (LLM05/ASI05)
- Há **limite de consumo/custo** (rate limit, budget)? (LLM10)

### Detectar
- Há **logging** das ações do agente e **observabilidade** de comportamento anômalo? (ASI08 cascading)

### Responder
- Existe **kill switch**/revogação de credenciais para conter um **agente desonesto**? (ASI10)

### Recuperar
- Estado e ações são **versionados/reversíveis** (rollback, audit trail)?

> Para um **sistema autônomo sem LLM** (ex.: pipeline CI/CD), reinterprete "agente" como esse sistema:
> "ferramentas" = APIs/deploy que ele aciona; "prompt injection" ≈ dados de entrada não confiáveis;
> "ações irreversíveis" = deploy/escrita em produção. As 12 perguntas-base funcionam direto.
