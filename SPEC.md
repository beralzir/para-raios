# para-raios — spec & design

## Propósito
Skill reutilizável que gera um **plano de risco & segurança de IA** para qualquer projeto do Bera,
escalado ao tamanho (solo → enterprise). Transforma o aprendizado da Atividade 4 do MIT (checklist
NIST CSF) + a pesquisa comparativa de frameworks de IA em uma ferramenta acionável e reaproveitável.

## Origem
- **Atividade 4** do Módulo 4 (Cibersegurança e riscos de agentes), MIT IA Agêntica.
- **Pesquisa multi-agente + verificação** de 6 frameworks (27/jun/2026), documentada em
  `modulos/04-ciberseguranca-riscos-agentes/pesquisa/frameworks-risco-seguranca-ia.md` (repo MIT).

## Decisões de design
- **Trigger: manual-only / nominal.** Segue a regra global do Bera (não auto-invocar skills). Mesmo
  padrão de `huashu-design` e `tags-bera`.
- **Backbone: NIST CSF + NIST AI RMF.** Gratuitos, flexíveis, mapeiam direto no exercício do curso e
  são reconhecidos por C-level. As 5 funções são a moldura onde tudo se pendura.
- **Conteúdo técnico: OWASP + MITRE ATLAS + SAIF.** Biblioteca de ameaças/controles (o "o que pode dar
  errado e como evitar") — a camada que a governança abstrata não dá.
- **Lente legal: EU AI Act (lite).** Checklist de transparência + práticas proibidas; completo só em T3.
- **ISO/IEC 42001: opt-in (T3).** Só quando há necessidade de selo auditável.
- **Escala por tier (T1/T2/T3).** Evita over/under-engineering — o erro mais comum num plano de risco.

## Por que "para-raios"
Aterra o risco antes de virar incidente. Persona memorável p/ palestra; alinha com o estilo de
skills-persona do Bera (pasteleiro, bola-de-cristal).

## Modo injeção (08/10/2026)
Segundo modo da skill, ao lado do plano de risco. Audita, planeja, **testa com injeção plantada** e
**conduz a refatoração** de um projeto para que ele resista a prompt injection (OWASP LLM01, ASI01,
ASI06). Fonte única do assunto: `references/prompt-injection.md`. O plano de risco normal aponta para
ela no passo 4 sempre que LLM01, ASI01 ou ASI06 se aplicam, e não repete o conteúdo.

**Por que entrou.** Os dois planos de risco do Marvin (06/09 e 25/09) acharam o mesmo gap: a regra
"conteúdo de fora é dado, nunca instrução" estava no comportamento e não estava escrita. O plano
recomendava, ninguém aplicava, e o segundo plano teve de subir o item de quick win para
pré-requisito. Recomendação sem teste e sem caminho de correção envelhece no papel. O Bera pediu os
quatro verbos (testar, garantir, auditar, refatorar) em 08/10/2026, e o caso de prova é o Marvin.

**Decisões.**
- Modo próprio, invocado por nome, e não sub-passo: auditar injeção não deve arrastar o plano NIST
  inteiro.
- Testar significa plantar injeção controlada no projeto do próprio Bera e observar, nunca atacar
  sistema de terceiro.
- Refatorar é conduzido: cada mudança no projeto auditado é mostrada e aprovada por ele antes de
  entrar. Hook vai em `settings.json` por mescla, nunca por sobrescrita.
- O que outra skill já é dona fica com ela, e o modo só aponta: servidor MCP é da `mcp-builder`
  (`references/security_gate.md`), documento em base RAG é da `rag-ai`
  (`references/security_licensing.md`), e o padrão P13 vem do catálogo do Gepeto.

## Não-objetivos
- Não é auditoria de segurança automatizada (não roda scanners/pentest). O teste com injeção
  plantada do modo injeção é exceção estreita: roda só no projeto do Bera, com payload conhecido, e
  não é pentest.
- Não substitui consultoria jurídica de compliance (EU AI Act aqui é orientação, não parecer).
- No plano de risco, não implementa correções. Produz o **plano**, e a execução é decisão à parte.
  No modo injeção, conduz a correção, mudança por mudança, com aprovação dele em cada uma.

## Manutenção
Frameworks mudam rápido. Revisar `references/frameworks.md` periodicamente (tem data da pesquisa).
Candidatos a próxima atualização: NIST AI RMF 2.0 (em revisão em 2026), nomenclatura OWASP Agentic
(ASI01–ASI10 ainda estabilizando), releases mensais do MITRE ATLAS.

## Como evoluir esta skill
Use o `skill-creator` (`/skill-creator`) para rodar evals de trigger e otimizar a `description` se o
disparo ficar impreciso. Para adicionar um framework, crie/atualize a seção em
`references/frameworks.md` e, se ele trouxer ameaças novas, em `references/threat-library.md`.
