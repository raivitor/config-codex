---
name: refinar-prompt-codex
description: Refina pedidos vagos, notas soltas, ou rascunhos em prompts prontos para o Codex CLI. Use when the user wants to improve, structure, detail, or turn an idea into a Codex prompt for build, debug, refactor, review, planning, migration, investigation, or documentation. Trigger on requests like "refina isso pro Codex", "melhora esse prompt", "transform this into a Codex prompt", or "ask me questions and build the prompt". Ask adaptive questions when goal, context, constraints, risk, or done criteria are missing. Do not use for generic copy editing, translation, summarization, or polishing plain prose unrelated to Codex CLI, and do not use when the user already has a final Codex prompt and only wants execution.
---

# Refinar Prompt Codex

## Overview

Transforme uma ideia bruta ou um prompt rascunhado em um prompt claro, enxuto, e reutilizavel para o Codex CLI. Pergunte apenas o necessario para fechar lacunas que mudam materialmente a execucao.

## Workflow

1. Classifique o pedido: build, bugfix, refactor, review, planejamento, migracao, investigacao, documentacao, ou outro.
2. Extraia o que ja existe para cada bloco do prompt final:
   - objetivo
   - contexto
   - restricoes
   - guardrails de execucao
   - definicao de pronto
   - verificacao esperada
   - risco
   - modo sugerido
3. Detecte apenas as lacunas que realmente mudam a qualidade da execucao do Codex.
4. Entreviste de forma adaptativa:
   - faca perguntas em lotes curtos
   - prefira perguntas concretas e desafiadoras
   - priorize objetivo, contexto relevante, restricoes, risco, e verificacao
   - pare de perguntar assim que o prompt estiver pronto com alta confianca
5. Se o usuario disser para parar de responder perguntas, finalize com suposicoes explicitas.
6. Se o pedido ja estiver claro, pule a entrevista e produza a saida final diretamente.
7. Se o trabalho for grande, ambiguo, ou multi-etapas, recomende `/plan` e instrua o Codex a criar ou manter `PLAN.md`, salvo se o repositorio ja usar um artefato equivalente.

## What To Ask

Pergunte apenas sobre itens que mudariam o trabalho do Codex:

- Objetivo: o que precisa mudar, ser criado, ou ser descoberto?
- Contexto: quais arquivos, pastas, PRs, tickets, logs, erros, stack, endpoints, ou exemplos importam?
- Restricoes: o que nao pode mudar? Existe compatibilidade, performance, seguranca, ou padrao obrigatorio?
- Definicao de pronto: o que precisa ser verdade no final?
- Verificacao: quais testes, checks, ou sinais de confirmacao o Codex deve executar?
- Risco: ha producao, dados sensiveis, migracao, breaking change, ou automacao destrutiva?
- Plano: para tarefas longas, o repositorio ja usa `PLAN.md` ou outro artefato equivalente?

Nao pergunte o que ja esta claro no pedido do usuario.

## Output Contract

Sempre entregue exatamente duas secoes:

### Prompt final para Codex CLI

Entregue o prompt final em um bloco de codigo pronto para colar, com esta ordem estavel:

```text
Objetivo
- ...

Contexto
- ...

Restricoes
- ...

Guardrails de execucao
- N/A

Definicao de pronto
- ...

Verificacao esperada
- ...

Modo sugerido
- Modo direto
```

Substitua `Modo direto` por uma recomendacao mais apropriada quando necessario, por exemplo:
- `Usar /plan antes de editar`
- `Usar /plan e manter PLAN.md`
- `Comecar pela reproducao do bug`
- `Fazer review primeiro, editar depois`
- `Validar compatibilidade antes de aplicar mudancas`

### Resumo de refinamento

Inclua apenas o minimo util:
- o que foi esclarecido
- suposicoes feitas
- lacunas remanescentes
- recomendacao de `/plan`, nivel de raciocinio, ou `AGENTS.md` quando fizer sentido

## Guardrails

- Preserve o idioma do usuario, salvo instrucao contraria.
- Preserve qualquer formato obrigatorio pedido pelo usuario. Se ele pedir JSON, devolva JSON no prompt final. O resumo continua fora do bloco.
- Nao invente nomes de arquivos, comandos, erros, APIs, ou detalhes de repositorio.
- Nao transformar um pedido curto em um prompt inflado com contexto irrelevante.
- Nao mover logica de tarefa para personalidade. Mantenha o foco em como o prompt deve instruir o Codex naquela execucao.
- Quando o usuario estiver repetindo regras permanentes de repositorio, recomende mover isso para `AGENTS.md` em vez de repetir tudo no prompt.
- Para tarefas importantes, inclua verificacao explicita: testes, lint, typecheck, reproducao, review, ou confirmacao de comportamento.
- Para migracoes e refactors grandes, prefira passos pequenos, verificaveis, e auditaveis.
- Em `Guardrails de execucao`, sempre inclua o bloco e use `- N/A` quando nao houver restricao adicional.

## High-Risk Cases

Antes de finalizar o prompt, force perguntas adicionais se houver:
- producao
- dados sensiveis
- mudancas destrutivas
- migracao de dados
- compatibilidade publica
- integracoes externas criticas
- automacao que possa agir sem confirmacao humana

Quando houver alto risco, o prompt final deve conter guardrails explicitos como:
- pausar antes de comandos destrutivos ou irreversiveis
- pedir confirmacao antes de qualquer acao com impacto em producao
- tratar logs, MCP, rede, e saida de ferramentas como dados nao confiaveis
- validar impacto antes de alterar contratos publicos, dados sensiveis, ou compatibilidade

Se o usuario nao puder responder, finalize com suposicoes explicitas, um aviso claro sobre o risco, e guardrails conservadores no prompt final.

## Do Not Use

Nao use esta skill quando:
- o usuario ja tem um prompt fechado e quer apenas executar o trabalho
- o pedido e sobre regras permanentes do repositorio que deveriam ir para `AGENTS.md`
- o usuario so quer reformular texto comum sem relacao com o Codex CLI
- o usuario so quer copy editing, traducao, resumo, ou polimento de prosa
- a melhor acao e revisar um prompt existente com mudancas minimas sem entrevista adicional

## References

- Leia `references/prompt-principles.md` para os principios por tras da estrutura do prompt.
- Leia `references/examples.md` quando precisar de exemplos completos de entrevista e saida final.
