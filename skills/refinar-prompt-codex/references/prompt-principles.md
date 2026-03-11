# Prompt Principles

Este arquivo resume os principios que guiam a skill.

## Core shape

Use um scaffold estavel sempre que possivel:

1. `Objetivo`
2. `Contexto`
3. `Restricoes`
4. `Guardrails de execucao`
5. `Definicao de pronto`
6. `Verificacao esperada`
7. `Modo sugerido`

Esse formato vem de praticas do Codex para reduzir ambiguidade e dar ao agente um alvo verificavel.

## What makes a good Codex prompt

- Diga claramente o que precisa mudar ou ser descoberto.
- Cite contexto realmente util: arquivos, pastas, erros, exemplos, ou sistemas envolvidos.
- Liste restricoes explicitas: compatibilidade, seguranca, arquitetura, ou "nao tocar".
- Diga o que define conclusao. "Done when" importa tanto quanto o pedido principal.
- Inclua como validar: testes, lint, review, reproducao, ou checks especificos.
- Para risco alto, explicite guardrails operacionais no proprio prompt e nao apenas no texto explicativo fora dele.

## When to interview

Pergunte quando faltar algo que mudaria o comportamento do Codex:

- o alvo esta vago
- faltam arquivos ou sinais de contexto
- nao esta claro o que nao pode ser alterado
- nao ha criterio de aceite
- existe risco operacional ou tecnico alto

Se o pedido ja estiver bom, nao entreviste so para seguir um ritual.

## When to recommend /plan

Recomende `/plan` quando houver:

- trabalho multi-etapas
- escopo ambiguo
- migracao ou refactor amplo
- dependencia entre varias partes do sistema
- risco alto de regressao

Nao use `/plan` em tarefas pequenas e bem delimitadas.

Para tarefas longas, prefira orientar o Codex a criar ou manter `PLAN.md`, salvo se o repositorio ja usar um artefato equivalente.

## Keep durable guidance out of the prompt

Se o usuario estiver repetindo as mesmas regras de repositorio toda hora, isso provavelmente pertence a `AGENTS.md`, nao ao prompt de uma unica execucao.

## Separate personality from task controls

Nao misture tom geral com requisitos do artefato. Controle de saida deve ser especifico:

- idioma
- formato
- tamanho
- canal
- registro

A personalidade nao deve sobrescrever requisitos concretos do pedido.

## Prefer explicit verification

Sempre que fizer sentido, diga ao Codex para:

- criar ou atualizar testes
- descobrir e rodar os comandos exatos de teste, lint, typecheck, ou build
- confirmar a mudanca observavel
- revisar o diff em busca de regressao

## Keep the prompt reusable

Mantenha o prefixo estrutural da saida estavel e coloque a variacao no conteudo. Isso melhora previsibilidade e reaproveitamento.

Nao transforme isso em um fluxo centrado em API ou em prompt caching. Para esta skill, basta manter a ordem dos blocos estavel e empurrar detalhes volateis do pedido para o fim.

## Large refactors and migrations

Para refactors e migracoes:

- preferir `/plan` com `PLAN.md`
- trabalhar com um escopo piloto antes de ampliar
- dividir em passos pequenos
- explicitar riscos
- pedir validacao por etapa
- preservar paridade comportamental quando aplicavel
