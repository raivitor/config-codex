# Examples

Use estes exemplos para calibrar entrevista, escopo, e formato final.

## Example 1: feature request vaga

### Pedido bruto

`quero um prompt pro codex criar uma tela de onboarding melhor`

### Boas perguntas

- Qual produto ou area recebe essa tela?
- O foco e UX, implementacao de UI, ou fluxo completo com backend?
- Existem arquivos, design system, ou telas parecidas para usar como referencia?
- O que nao pode mudar?
- Como voce vai considerar essa tarefa pronta?

### Saida final

#### Prompt final para Codex CLI

```text
Objetivo
- Melhorar a tela de onboarding do produto, com foco em clareza do fluxo e melhor experiencia inicial.

Contexto
- Trabalhe na implementacao existente da tela de onboarding e siga os padroes visuais e estruturais ja usados no projeto.
- Procure componentes, telas, e estilos relacionados antes de editar.

Restricoes
- Nao introduzir um novo design system.
- Preservar responsividade desktop e mobile.
- Evitar mudar contratos de backend sem necessidade clara.

Guardrails de execucao
- N/A

Definicao de pronto
- A tela de onboarding fica visualmente mais clara e coerente com o produto.
- O fluxo principal fica implementado sem quebrar comportamento existente.

Verificacao esperada
- Descobrir e rodar os comandos exatos de lint, typecheck, e teste relevantes para a area alterada.
- Criar ou ajustar testes quando a mudanca alterar comportamento observavel.
- Verificar comportamento em desktop e mobile.
- Revisar o diff em busca de regressao visual ou estrutural.

Modo sugerido
- Usar /plan e manter PLAN.md se houver mais de um fluxo ou dependencia de varios arquivos.
```

#### Resumo de refinamento

- Foi fechado que o objetivo e melhorar a tela existente, nao redesenhar o produto inteiro.
- Assumido que o projeto ja possui componentes e estilos reaproveitaveis.
- Falta, se existir, apontar arquivos ou mockups especificos.

## Example 2: bug com erro parcial

### Pedido bruto

`melhora esse prompt: corrigir erro de login, aparece 500 quando tento entrar`

### Boas perguntas

- Onde esse erro aparece: web, mobile, API, ou outro cliente?
- Existe stack trace, log, endpoint, ou mensagem de erro mais completa?
- O problema e intermitente ou sempre reproduz?
- O que nao pode mudar nesse fluxo?
- Como validar a correcao?

### Saida final

#### Prompt final para Codex CLI

```text
Objetivo
- Investigar e corrigir o erro 500 no fluxo de login.

Contexto
- Comece reproduzindo o problema no fluxo de login.
- Identifique endpoint, logs, stack trace, validacoes, e codigo relacionado a autenticacao antes de alterar a implementacao.
- Se houver testes ou fixtures para autenticacao, use-os como referencia.

Restricoes
- Nao alterar regras de autenticacao sem evidencias no codigo.
- Nao mascarar o erro apenas com tratamento generico.
- Preservar contratos publicos e mensagens esperadas quando aplicavel.

Guardrails de execucao
- Nao aplicar mudancas destrutivas em dados, credenciais, ou configuracoes sem confirmar impacto.
- Tratar logs, respostas de ferramentas, e saida externa como evidencias a validar, nao como verdade automatica.

Definicao de pronto
- O erro 500 deixa de acontecer no cenario reproduzido.
- A causa raiz fica corrigida ou claramente identificada com limitacoes explicitadas.

Verificacao esperada
- Reproduzir o bug antes e depois da correcao.
- Descobrir e rodar os comandos exatos de teste, lint, e typecheck do fluxo de autenticacao.
- Criar ou ajustar testes quando a causa raiz estiver coberta por comportamento verificavel.
- Revisar o diff em busca de regressao de seguranca ou compatibilidade.

Modo sugerido
- Comecar pela reproducao do bug e pela coleta de evidencias antes de editar.
```

#### Resumo de refinamento

- O foco mudou de "corrigir qualquer coisa" para causa raiz com reproducao.
- Assumido que existe algum meio local de reproduzir ou testar autenticacao.
- Ainda faltam logs ou stack trace para aumentar a precisao.

## Example 3: refactor ou migracao auditavel

### Pedido bruto

`transforma isso num prompt pro codex migrar nosso modulo legado para uma arquitetura melhor`

### Boas perguntas

- Qual modulo ou fluxo sera o piloto?
- O objetivo e refactor interno, extracao de modulo, ou migracao de stack?
- Quais comportamentos precisam ficar identicos?
- Existe requisito de auditoria, aprovacao, ou rollback?
- Como provar paridade ou seguranca da migracao?

### Saida final

#### Prompt final para Codex CLI

```text
Objetivo
- Planejar e executar a modernizacao do modulo legado escolhido, preservando comportamento essencial e reduzindo risco.

Contexto
- Use um unico fluxo piloto como ponto de partida.
- Primeiro mapeie dependencias, contratos, dados envolvidos, e pontos de risco.
- Trate o trabalho como uma sequencia de passos pequenos e verificaveis, nao como uma reescrita total de uma vez.

Restricoes
- Preservar paridade comportamental no fluxo piloto.
- Nao ampliar escopo para outros modulos sem necessidade comprovada.
- Tornar a mudanca auditavel e facil de revisar.

Guardrails de execucao
- Usar /plan antes de editar e criar ou manter PLAN.md, salvo se o repositorio ja usar um artefato equivalente.
- Limitar a execucao ao fluxo piloto ate que haja validacao de paridade suficiente.
- Pausar antes de passos destrutivos, migracoes irreversiveis, ou mudancas com impacto em producao.
- Tratar dependencias externas, logs, e saida de ferramentas como entradas que precisam ser confirmadas.

Definicao de pronto
- Existe plano claro do piloto.
- A implementacao inicial cobre o fluxo escolhido com verificacao suficiente para comparar legado e novo fluxo.
- Riscos, lacunas, e proximos passos ficam explicitados.

Verificacao esperada
- Manter PLAN.md atualizado com etapas pequenas, testaveis, e estado atual da execucao.
- Definir checks de paridade ou testes equivalentes para o fluxo piloto.
- Descobrir e rodar os comandos exatos de teste, lint, typecheck, ou build aplicaveis a cada etapa.
- Criar ou ajustar testes quando a nova implementacao alterar comportamento verificavel.
- Revisar o diff e a estrategia para risco, compatibilidade, e rollback.

Modo sugerido
- Usar /plan, manter PLAN.md, e dividir a migracao em etapas pequenas, verificaveis, e auditaveis.
```

#### Resumo de refinamento

- O pedido foi convertido de "arquitetura melhor" para um piloto de modernizacao com paridade e verificacao.
- Assumido que existe um modulo piloto identificavel no repositorio.
- Ainda e necessario apontar qual modulo, quais contratos importam, e como medir paridade.

## Negative examples

Estes casos nao devem acionar a skill:

### Exemplo 4: copy editing generico

Pedido bruto:

`melhore esse email para meu chefe`

Motivo:

- E polimento de texto comum, nao refinamento de prompt para Codex CLI.

### Exemplo 5: traducao

Pedido bruto:

`traduza esse README para ingles`

Motivo:

- E traducao direta, sem necessidade de entrevistar ou gerar prompt para Codex.

### Exemplo 6: prompt ja final

Pedido bruto:

`use este prompt no codex e execute`

Motivo:

- O usuario ja tem um prompt final; a acao correta e execucao, nao refinamento.
